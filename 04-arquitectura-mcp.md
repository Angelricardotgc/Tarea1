# 4. Arquitectura de MCP

* **Modelo host / cliente / servidor**

1. Host
Es la aplicación con la que interactúa la persona usuaria; la que contiene al modelo de lenguaje y coordina todo. El host es responsable de gestionar el ciclo de vida de las conexiones, pedir consentimiento al usuario antes de ejecutar una herramienta, y aplicar las políticas de seguridad (por ejemplo, qué servidores están permitidos).

Con mi ejemplo: Claude Desktop es el Host. Es la aplicación de escritorio que ejecutas, la que contiene al modelo (Claude) y la que te muestra el diálogo de "¿permitir esta acción?" cada vez que el modelo quiere usar una herramienta.

2. Cliente (Client)
Vive dentro del host y mantiene una conexión 1 a 1 con un servidor MCP específico. Su trabajo es hablar el protocolo JSON-RPC 2.0 con ese servidor: enviarle peticiones, recibir sus respuestas, y traducir eso a un formato que el modelo pueda usar. Si te conectas a tres servidores distintos, el host internamente instancia tres clientes, uno por servidor.

Con mi ejemplo: el componente cliente MCP integrado en Claude Desktop. No es algo que tú veas o configures por separado —está embebido dentro de la aplicación—, pero es la pieza que efectivamente abre el proceso del servidor y le manda los mensajes JSON-RPC.

3. Servidor (Server)
Es un programa externo, separado del host, que expone un catálogo de capacidades (herramientas, recursos, plantillas de prompt) sobre un recurso o sistema en particular. El servidor no sabe nada del modelo de lenguaje ni de cómo se usa su salida; solo responde a las peticiones del protocolo.

Con mi ejemplo: @modelcontextprotocol/server-filesystem, el proceso que se lanza vía npx y que expone las herramientas list_directory, read_file, write_file, etc., limitadas al directorio que configuraste.

*  **Versión de la especificación que consultaron y su fecha**

Documento redactado con base en la especificación del Model Context Protocol, revisión 2025-11-25, publicada por Anthropic el 25 de noviembre de 2025. Se eligió esta versión porque describe el modelo de conexión persistente (con handshake initialize) que implementan actualmente las herramientas usadas en esta práctica (servidor @modelcontextprotocol/server-filesystem, y los clientes Claude Desktop / VS Code). El 28 de julio de 2026 se publicó una revisión posterior (2026-07-28) que rediseña el protocolo hacia un núcleo sin estado y declara obsoletas las primitivas Roots, Sampling y Logging; dicha revisión aún no era la implementada por el software utilizado al momento de esta entrega.

* **Primitivas del lado del servidor:**

Un servidor MCP expone su funcionalidad a través de tres primitivas:

**Tools (herramientas)**
Son funciones ejecutables que el modelo puede invocar para realizar una acción o cálculo. Cada tool se anuncia mediante tools/list con un nombre, una descripción en lenguaje natural y un esquema JSON de sus parámetros de entrada. El modelo decide, en tiempo de ejecución, cuál invocar según la petición del usuario, y el resultado se obtiene mediante tools/call. En nuestra implementación, el servidor de sistema de archivos expone tools como read_file, write_file, list_directory, move_file y search_files.

**Resources (recursos)**
Son datos identificados por una URI que el cliente puede leer y anexar al contexto de la conversación, sin que esto implique una acción o efecto secundario sobre el sistema. Se descubren mediante resources/list y se obtienen con resources/read. La diferencia conceptual con una tool es clara: un resource se lee, una tool se ejecuta.

**Prompts (plantillas de prompt)**
Son plantillas de mensajes reutilizables y parametrizables que el servidor pone a disposición para guiar interacciones comunes. A diferencia de las tools —que el modelo invoca por su cuenta cuando lo considera necesario—, los prompts normalmente los selecciona explícitamente la persona usuaria desde la interfaz del cliente (por ejemplo, mediante un comando de barra /).

* **Primitivas del lado del usuario:**

**Roots**
El cliente comunica al servidor cuáles directorios o ubicaciones son relevantes para la sesión actual (por ejemplo, la carpeta de proyecto abierta en el editor). Es importante aclarar que un root comunica una intención de alcance, pero no impone por sí mismo una restricción de seguridad: la validación real de qué se puede leer o escribir la debe implementar el propio servidor, como hace server-filesystem al restringir sus operaciones al directorio configurado explícitamente.

**Elicitation**
Permite que el servidor, a mitad de una operación, solicite al cliente que recabe información adicional de la persona usuaria (por ejemplo, una preferencia o un dato faltante para completar una tarea), sin necesidad de que toda la información se proporcione por adelantado.

* **Transportes:**

MCP define dos mecanismos de transporte para el intercambio de mensajes JSON-RPC 2.0:

- stdio: usado para servidores locales. El cliente lanza el servidor como un proceso hijo en la misma máquina, y ambos se comunican escribiendo y leyendo mensajes JSON-RPC por la entrada/salida estándar (stdin/stdout). Es el transporte que usa nuestro servidor de filesystem, invocado mediante npx.
- Streamable HTTP: usado para servidores remotos. El cliente se conecta a una URL vía HTTP, y el servidor puede responder tanto con una respuesta HTTP simple como con un flujo de eventos (Server-Sent Events) cuando la operación lo amerita. Sustituyó al transporte anterior basado únicamente en SSE de versiones previas a 2025-03-26.
