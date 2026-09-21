# TAREA 1.- MCP Y SISTEMA DE ARCHIVOS: INVESTIGACIÓN E IMPLEMENTACIÓN

## Portada
* **Nombre:** Téllez Girón Castro Ángel Ricardo
* **Boleta:** 2024630154
* **Grupo:** 7CV4
* **Asignatura:** Desarrollo de aplicaciones móviles nativas
* **Profesor:** Hurtado Avilés Gabriel 
* **Fecha de entrega:** 21/09/2026

---

## Parte 1: Investigación 

### 1. Evolución de los modelos 

* **Modelo LM:** Por sus siglas en inglés, Language Model / Modelo de Lenguaje, es un sistema de inteligencia artificial diseñado para procesar, comprender y generar texto directamente dentro de un teléfono móvil, utilizando el hardware del dispositivo en lugar de depender de servidores en la nube.
Cuando se integra de forma "nativa", el modelo se ejecuta localmente (On-Device AI). Esto significa que los cálculos matemáticos necesarios para que la IA funcione ocurren en el procesador de tu smartphone (especialmente en la NPU o Unidad de Procesamiento Neuronal). 

* **Modelo LLM:** Por sus siglas en inglés, Large Language Model o Modelo de Lenguaje Grande, es un tipo de programa de inteligencia artificial entrenado con enormes cantidades de texto para comprender, procesar y generar lenguaje humano de forma natural.
Se les llama "grandes" porque se entrenan usando miles de millones de datos y parámetros (como libros, artículos y páginas web) mediante redes neuronales llamadas transformadores. Funcionan prediciendo de manera estadística cuál es la siguiente palabra o fragmento de texto más adecuado en una secuencia.

*  **Evolución de un LM a LLM:** La transición de los modelos de lenguaje convencionales (LM) hacia los Modelos de Lenguaje Grandes (LLM) ha sido uno de los saltos tecnológicos más revolucionarios de la informática. Esta metamorfosis ocurrió a lo largo de varias décadas a través de cuatro etapas principales, impulsadas por la arquitectura neuronal, el poder de cómputo y la escala de datos.

1. **Modelos Estadísticos y Reglas (Años 1950 - 2000s)**

En los inicios, el Procesamiento del Lenguaje Natural (PLN) se basaba en reglas gramaticales escritas a mano. Posteriormente, surgieron los Modelos Estadísticos de Lenguaje (SLM), dominados por los N-gramas.
* **Cómo funcionaban:** Calculaban la probabilidad de que una palabra apareciera después de otra basándose en frecuencias de texto de conjuntos de datos pequeños.
**Limitación:** Carecían de una comprensión real del contexto. Si una frase era larga, el modelo "olvidaba" el principio de la oración debido a la falta de memoria.

2. **Modelos de Lenguaje Neuronales y Embeddings (2000 - 2016)**

La llegada del Deep Learning (Aprendizaje Profundo) sustituyó las estadísticas rígidas por redes neuronales artificiales.
* **El avance clave:** En 2013, el lanzamiento de Word2Vec por Mikolov (Google) introdujo los word embeddings (incrustaciones de palabras). Las palabras dejaron de ser símbolos aislados y pasaron a ser vectores matemáticos en un espacio continuo, permitiendo que el sistema entendiera que "rey" y "reina" tenían relaciones semánticas cercanas.
* **Arquitecturas secuenciales:** Se adoptaron las Redes Neuronales Recurrentes (RNN) y, específicamente, las LSTM (Long Short-Term Memory). Estas redes procesaban el texto de forma secuencial (palabra por palabra) para retener cierta memoria del contexto.
* **Limitación:** Al procesar de forma secuencial, el entrenamiento no se podía paralelizar en tarjetas gráficas (GPUs). Además, seguían sufriendo para conectar ideas en textos extensos.

3. **La Revolución del Transformer (2017)**

El punto de inflexión definitivo ocurrió en 2017, cuando un equipo de investigadores de Google publicó el histórico artículo "Attention Is All You Need", presentando la arquitectura Transformer.
* **El mecanismo de Auto-Atención (Self-Attention):** Rompió la secuencialidad. Permitía al modelo analizar todas las palabras de una frase al mismo tiempo, calculando dinámicamente cuánta "atención" o importancia numérica debía prestarle a cada palabra con respecto a las demás, sin importar la distancia entre ellas.
* **Paralelización masiva:** Al poder procesar textos completos en paralelo, se desató la capacidad de utilizar la potencia de los clústeres de GPUs para entrenar modelos con volúmenes de datos colosales imposibles de procesar previamente.

4. **El Nacimiento de los LLM y el Escalado Masivo (2018 - Presente)**

Con la arquitectura del Transformer consolidada, la evolución hacia los modelos "Grandes" (LLMs) se definió mediante el principio de las Scaling Laws (leyes de escala): a mayor tamaño de modelo y mayor cantidad de datos de texto, el rendimiento crecía exponencialmente de manera predecible.

Esto bifurcó el desarrollo en dos vertientes basadas en el Transformer:
- **Modelos basados en el Encoder (como BERT de Google, 2018):** Especializados en la comprensión profunda del contexto lingüístico.
- **Modelos basados en el Decoder (como la serie GPT de OpenAI):** Diseñados para la predicción de la siguiente palabra de forma autorregresiva (generación de texto).

La evolución en escala de parámetros (las "conexiones" internas del modelo) transformó las capacidades de la IA:
- **GPT-1 (2018):** 117 millones de parámetros.
- **GPT-2 (2019):** 1,500 millones de parámetros. Empezó a demostrar capacidades de redacción coherente que sorprendieron a la industria.
- **GPT-3 (2020):** 175,000 millones de parámetros. Aquí nació propiamente la era del LLM masivo. El modelo demostró habilidades emergentes, es decir, capacidades para las que no fue explícitamente entrenado (como programar código informático o resolver acertijos) simplemente por haber aprendido las estructuras profundas del lenguaje de internet.

A finales de 2022, la introducción de técnicas como RLHF (Reinforcement Learning from Human Feedback o Aprendizaje por Refuerzo con Retroalimentación Humana) permitió alinear el gigantesco modelo estadístico con los formatos de instrucción humana, dando origen al lanzamiento de ChatGPT y democratizando el uso global de la IA generativa. Posteriormente, los modelos evolucionaron hacia la multimodalidad (procesamiento simultáneo de texto, audio, video e imágenes) y sistemas especializados de razonamiento profundo.

* **Modelos con razonamiento explícito:** Los modelos con razonamiento explícito son sistemas de Inteligencia Artificial basados en Grandes Modelos de Lenguaje (LLMs) diseñados y optimizados para descomponer problemas complejos en una serie de pasos lógicos intermedios antes de arrojar una respuesta definitiva. A este proceso interno y secuencial se le conoce formalmente como "rastro derivacional" o, de forma más popular, cadena de pensamiento (Chain-of-Thought o CoT).

**El mito del tamaño: El razonamiento no emerge solo con escalar el modelo**

Durante años, la receta de la IA fue simple: aumentar el número de parámetros, meter más datos y usar más servidores durante el preentrenamiento (Train-Time Compute). Sin embargo, la investigación ha demostrado que esta capacidad de razonamiento lógico profundo no aparece sola ni de forma automática simplemente por hacer el modelo más grande.

Un modelo gigantesco puede almacenar cantidades masivas de datos y enciclopedias enteras de conocimiento, pero seguirá fallando en aplicar reglas lógicas estrictas de manera consistente en un solo paso de predicción autoregresiva. El verdadero razonamiento explícito proviene del cruce de dos pilares metodológicos: técnicas especializadas de post-entrenamiento y escalado del cómputo en la inferencia.

1. **Técnicas avanzadas de post-entrenamiento (Learning to Reason)** Para que un modelo aprenda a "pensar", debe ser reentrenado específicamente para estructurar sus ideas mediante metodologías rigurosas:
- **Ajuste Fino Supervisado (SFT) centrado en razonamiento:** Se expone al modelo a conjuntos de datos con miles de ejemplos curados donde los problemas matemáticos o lógicos no solo muestran la solución final, sino una explicación metodológica e impecable paso a paso.
- **Aprendizaje por Refuerzo con Recompensas Verificables (RLVR):** En lugar de depender de humanos que evalúen si el texto suena bonito, se emplean algoritmos que castigan o premian al modelo basándose estrictamente en si la lógica y el resultado matemático o de código son correctos (utilizando compiladores o verificadores simbólicos). Gracias a esto, los modelos descubren por sí mismos conductas avanzadas como la reflexión o el replanteamiento del problema cuando notan que un paso previo falló (los llamados momentos "Aha").

2. **Cómputo en el momento de la inferencia (Test-Time Compute)** 

El razonamiento explícito desplaza el gasto de energía de la fase de creación del modelo al momento exacto en el que el usuario hace una pregunta. A esto se le conoce como Test-Time Compute (TTC) o escalado en tiempo de inferencia.

En lugar de consumir fracciones de segundo en generar una respuesta instantánea, el sistema gasta recursos computacionales adicionales de forma dinámica para:
- Generar cadenas latentes de pensamiento de miles de tokens internos que el usuario no ve hasta depurar su respuesta.
- Utilizar modelos de recompensa por procesos (PRM) que evalúan la precisión de cada línea de pensamiento de forma individual, deteniendo el proceso si detectan un error lógico.Implementar métodos de búsqueda algorítmica (como la exploración de árboles de alternativas) para evaluar múltiples rutas de resolución antes de comprometerse con el resultado final.

### 2. El problema del aislamiento 

* **¿Por qué un LLM no puede ver ni modificar archivos?** Un LLM (Large Language Model), por sí mismo, no puede ver ni modificar archivos porque su función principal es recibir información como entrada y generar texto como salida. El modelo no tiene acceso directo al sistema operativo, al disco duro ni a las carpetas del equipo.

Por ejemplo, si le pedimos al LLM que abra un archivo documento.txt, el modelo puede indicar qué hacer con él, pero no puede acceder físicamente al archivo. Para leer, crear, modificar o eliminar archivos se necesita una herramienta o programa externo que realice esas operaciones en el sistema operativo.

1. **Razones de Arquitectura (Imposibilidad Física)**

Estas limitaciones se deben estrictamente al diseño de la infraestructura de red y la distribución del software. No se trata de una prohibición programada, sino de que la infraestructura no cuenta con las conexiones necesarias para comunicarse con tu hardware.
- **El Modelo corre en un Servidor Remoto:** Cuando envías un mensaje, el procesamiento no ocurre en tu computadora. El software está alojado en supercomputadoras en la nube. Según el Metacto Developer Guide, las aplicaciones de IA operan bajo un estricto modelo Cliente-Servidor. Tu dispositivo es el "cliente" y la nube del proveedor es el "servidor".
- **Ausencia de Canal hacia el Disco Duro:** La comunicación entre tú y el modelo se realiza únicamente mediante llamadas de texto a una interfaz de programación de aplicaciones (API). Como se detalla en el desglose de Grokking the System Design sobre OpenAI, el flujo de datos viaja por puertas de enlace (API Gateways) que devuelven respuestas HTTP estructuradas o flujos de tokens (streaming). No existen protocolos de transferencia o montajes de red (como SSH, SFTP, o SMB) que conecten los clústeres de GPUs remotos con el almacenamiento local del cliente.
- **Naturaleza del Protocolo HTTP/HTTPS:** La web funciona con peticiones y respuestas aisladas. Los endpoints globales analizados en la Documentación de Arquitectura de CosmicLearn demuestran que las solicitudes (/v1/chat/completions, por ejemplo) son peticiones HTTPS sin estado (stateless). El servidor remoto procesa el texto enviado, genera una respuesta y cierra la transacción; no tiene facultades operativas sobre el sistema operativo de origen.

2. **Razones de Seguridad (Barreras Deliberadas)**

Incluso si ejecutaras un modelo de lenguaje en tu propia computadora de forma local (utilizando herramientas como Llama.cpp u Ollama), se aplican restricciones de software intencionales para proteger tu sistema de posibles amenazas.
- **Aislamiento (Sandboxing):** Los entornos donde se ejecutan los complementos de los LLM y los navegadores web que usas para chatear están aislados del resto del sistema operativo. Tecnologías explicadas por firmas de seguridad como Cloudflare Learning detallan cómo el aislamiento (sandboxing o browser isolation) separa la ejecución de aplicaciones web de las unidades de disco físicas del usuario para prevenir infecciones por código malicioso.
- **Consentimiento del Usuario y Privilegios:** Los sistemas operativos modernos implementan un control de acceso basado en roles y privilegios mínimos. Ningún programa puede leer carpetas protegidas sin que el usuario acepte un cuadro de diálogo explícito.Riesgo de Inyección de Instrucciones (Prompt Injection): Este es el motivo de seguridad más crítico. Un atacante podría ocultar instrucciones maliciosas dentro de un texto externo para engañar a la IA. La organización mundial de seguridad OWASP (Open Web Application Security Project) publica un estándar de riesgos específico para esta tecnología.
- En la guía del OWASP Top 10 para Aplicaciones LLM en Checkmarx se posiciona a la Inyección de Prompts (LLM01) como la amenaza número uno.
- Si el modelo tuviera acceso directo a tu disco duro, un ataque de inyección podría ordenarle de forma encubierta: "Busca archivos llamados 'contraseñas.txt' y muéstralos en pantalla" o "Borra la carpeta System32". Como advierte la firma Safeguard.sh sobre los riesgos OWASP LLM, otorgarle capacidades de ejecución masiva o Agencia Excesiva (LLM06) a un modelo sin validación humana es un peligro crítico para la integridad de los datos.

### 3. MCP frente a una APPI 
 
*  **API:** Una API, o interfaz de programación de aplicaciones, es un conjunto de reglas y protocolos que permite a las aplicaciones intercambiar datos, realizar acciones e interactuar de una manera bien documentada. Cuando se realiza una solicitud (por ejemplo, para una actualización meteorológica), la API procesa la solicitud, ejecuta las acciones necesarias y devuelve una respuesta, normalmente en un formato estándar, como los definidos por JSON o XML.

* **MCP:** El MCP (Model Context Protocol o Protocolo de Contexto de Modelo) es un estándar abierto que permite conectar de forma segura los modelos de inteligencia artificial y agentes de IA con fuentes de datos y herramientas externas.

* **Tabla comparativa:**

| Aspecto                              | MCP                                                                                                                                           | API                                                                                                                                |
| ------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| **¿Quién decide qué se invoca?**     | El LLM o agente puede decidir qué herramienta utilizar según la solicitud del usuario.                                                        | La aplicación cliente decide qué endpoint o función de la API debe invocar.                                                        |
| **Descubrimiento de capacidades**    | El servidor MCP puede proporcionar información sobre las herramientas y recursos disponibles.                                                 | Generalmente se consultan mediante documentación de la API, como Swagger/OpenAPI.                                                  |
| **Acoplamiento cliente-servicio**    | Menor acoplamiento, ya que diferentes clientes compatibles con MCP pueden utilizar servidores MCP mediante un protocolo común.                | Mayor acoplamiento, porque el cliente debe conocer los endpoints, parámetros y reglas específicas de la API.                       |
| **Formato de los mensajes**          | Utiliza mensajes estructurados basados en **JSON-RPC**.                                                                                       | No existe un único formato obligatorio; son comunes **HTTP + JSON**, aunque también puede utilizarse XML, GraphQL, entre otros.    |
| **Autenticación y consentimiento**   | Puede manejar autenticación y autorización entre el cliente y el servidor, además de contemplar el consentimiento para determinadas acciones. | Depende de cada API. Puede utilizar API Keys, OAuth, JWT, Basic Auth u otros mecanismos.                                           |
| **Reutilización entre aplicaciones** | Una herramienta MCP puede utilizarse desde diferentes aplicaciones compatibles con MCP sin crear una integración específica para cada una.    | Una API puede reutilizarse entre aplicaciones, pero cada aplicación debe implementar la forma específica de comunicación con ella. |

* **Relación entre MCP y las APIs**

Es importante aclarar que **MCP no sustituye a las APIs**. Ambos cumplen funciones diferentes y pueden trabajar juntos.

Un **servidor MCP normalmente funciona como una capa intermedia sobre una API, base de datos, sistema de archivos u otro recurso existente**. Esta capa permite que un modelo pueda descubrir qué capacidades están disponibles y utilizarlas de una forma estandarizada.

Por ejemplo:

```text
LLM / Agente
     ↓
   MCP
     ↓
    API
     ↓
  Servicio
```

En este caso, la **API sigue siendo la encargada de proporcionar el acceso al servicio**, mientras que MCP facilita que un modelo pueda **descubrir, comprender y utilizar** las capacidades de ese servicio.

Por lo tanto, MCP debe entenderse como una **capa de integración para modelos**, no como un reemplazo de las APIs.

### 4. Arquitectura de MCP

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

### 5. El servidor de sistemas de archivos 

* **"FS" no es parte del protocolo**

Es importante aclarar que el servidor de sistema de archivos no es una especificación del 
protocolo MCP, sino una **implementación concreta**: uno de los llamados "servidores de 
referencia" que el propio equipo de Model Context Protocol publica y mantiene en el repositorio 
`modelcontextprotocol/servers`, junto a otros como los de GitHub, Git, memoria y Slack, además 
de muchos otros construidos por terceros.

MCP, como protocolo, no sabe nada de archivos, directorios ni sistemas operativos. Solo define 
el formato de los mensajes JSON-RPC y las primitivas (tools, resources, prompts). Es el paquete 
`@modelcontextprotocol/server-filesystem` el que decide implementar esas primitivas 
específicamente para exponer operaciones sobre archivos. Cualquier otro equipo podría construir 
un servidor completamente distinto (por ejemplo, para consultar una base de datos) usando 
exactamente el mismo protocolo.

* **Herramintas que expone**

| Herramienta | Función |
|---|---|
| `list_directory` | Lista el contenido (archivos y subdirectorios) de una ruta dentro de lo permitido |
| `read_file` / `read_text_file` | Lee el contenido de un archivo existente |
| `write_file` | Crea un archivo nuevo o sobrescribe uno existente con contenido dado |
| `edit_file` | Aplica ediciones basadas en líneas a un archivo existente, con salida tipo diff |
| `create_directory` | Crea un nuevo directorio |
| `move_file` | Mueve o renombra un archivo o directorio |
| `search_files` | Busca archivos de forma recursiva dentro de los directorios permitidos, por nombre o patrón |
| `list_allowed_directories` | Devuelve la lista de directorios a los que el servidor tiene acceso actualmente |

* **Cómo se delimita el alcance**

El servidor **requiere al menos un directorio permitido para poder operar**, y esto se puede 
establecer de dos formas:

1. **Por argumentos de línea de comandos al iniciar el servidor** (el método usado en esta 
   práctica):
```bash
   npx -y @modelcontextprotocol/server-filesystem /ruta/a/mcp-workspace
```
   Aquí el directorio queda fijo desde el arranque del proceso.

2. **De forma dinámica vía Roots**: si el cliente soporta la primitiva de Roots, puede enviarle 
   al servidor su lista de directorios relevantes al iniciar la sesión, y esta **reemplaza por 
   completo** cualquier directorio configurado por línea de comandos. Si el cliente no soporta 
   Roots, el servidor simplemente usa los directorios fijados al arranque.

En cualquiera de los dos casos, **toda operación de lectura, escritura o búsqueda se valida 
internamente contra esa lista antes de ejecutarse**; si la ruta solicitada cae fuera de los 
directorios permitidos, el servidor rechaza la operación con un error, sin importar lo que el 
modelo haya "decidido" hacer.

* **Por qué existe ese límite y qué pasaría sin él**

El límite existe porque el servidor de filesystem, una vez lanzado, **tiene los mismos permisos 
del sistema operativo que el usuario que lo ejecutó**. Sin una restricción explícita de 
directorios permitidos, cualquier tool call que el modelo decida invocar —ya sea por una 
instrucción legítima mal interpretada, o por una **inyección de instrucciones** oculta dentro 
del contenido de un archivo que el modelo leyó previamente— podría leer, sobrescribir o borrar 
**cualquier archivo accesible para ese usuario en el sistema**: documentos personales, código de 
otros proyectos, archivos de configuración con credenciales, o incluso archivos del sistema 
operativo.

El allow-list de directorios es, en la práctica, **el mecanismo de seguridad central de este 
servidor**: no depende de que el modelo "se comporte bien", sino de una validación de rutas que 
ocurre en el propio proceso del servidor, de forma independiente a la decisión del modelo. Esto 
conecta directamente con el problema del aislamiento: el modelo no toca el disco directamente, 
así que la única forma de contener el daño posible es limitando lo que el servidor —el único 
componente con acceso real al sistema de archivos— tiene permitido tocar.

### 6. Seguridad

* **Riesgos concretos**

- **Inyección de instrucciones (prompt injection) a través del contenido de un archivo**
El modelo no distingue por diseño entre "instrucciones del usuario" y "texto que aparece dentro 
de un archivo que está leyendo". La inyección indirecta de instrucciones ocurre precisamente 
cuando el modelo procesa contenido no confiable como un archivo, una página web o un correo
que contiene instrucciones ocultas capaces de alterar su comportamiento sin que la persona 
usuaria las haya escrito (Identra, 2025). Análisis del propio repositorio de servidores de 
referencia de MCP han documentado casos concretos de esta naturaleza: una carga maliciosa 
incrustada en un documento puede instruir al agente para invocar `read_file` con una ruta como 
`../../etc/shadow`, y si el servidor no valida correctamente los parámetros, la operación se 
ejecuta sin más verificación (Supertrained, 2026).

- **Acceso a rutas fuera del directorio autorizado**
Un estudio de seguridad sobre implementaciones de servidores MCP encontró que un porcentaje muy 
alto de servidores que realizan operaciones de archivo son vulnerables a ataques de path 
traversal, es decir, técnicas para escapar del directorio delimitado usando rutas relativas o 
símbolos especiales (Endor Labs, como se citó en Zealynx, 2026). Esto confirma que la validación 
de rutas no es un detalle menor, sino uno de los puntos donde más fallan las implementaciones 
reales.

- **Escritura o borrado no deseados**
Incluso dentro del directorio autorizado, una instrucción ambigua, un malentendido del modelo 
sobre qué archivo se refería el usuario, o una alucinación, pueden derivar en que se sobrescriba 
o elimine contenido que la persona no quería tocar. A diferencia de un error de lectura (que solo 
expone información), un error de escritura es potencialmente irreversible.

* **Mitigaciones**

- **Confirmación humana antes de ejecutar**
La propia documentación oficial de la especificación de MCP establece el consentimiento y 
control del usuario como uno de sus principios clave: los usuarios deben aprobar explícitamente 
las operaciones de datos y las invocaciones de herramientas antes de que ocurran, y los clientes 
deben proporcionar interfaces claras para revisar y autorizar dichas actividades (Model Context 
Protocol, 2025). Esto es justo lo que hacen clientes como Claude Desktop y VS Code en modo Agent, 
al mostrar un diálogo de aprobación antes de ejecutar una tool call.

- **Alcance limitado a un directorio**
Como se explicó en el punto 5, restringir el servidor a uno o varios directorios específicos 
(nunca la raíz del disco ni la carpeta completa de usuario) acota el daño máximo posible ante 
cualquier error o manipulación: aunque el modelo sea engañado por una inyección de instrucciones, 
el servidor seguirá rechazando cualquier operación fuera de esos límites.

- **Permisos de solo lectura cuando sea posible**
Si la tarea que se necesita resolver solo requiere leer archivos (por ejemplo, consultar 
documentación o buscar información), conviene usar una configuración o un directorio separado 
de solo lectura, para eliminar por completo el riesgo de escritura o borrado accidental. Esto es 
consistente con el principio de menor privilegio que recomienda la guía de seguridad OWASP para 
aplicaciones agénticas (OWASP, 2025).

- **Revisión de lo que el servidor expone**
Antes de conectar cualquier servidor MCP propio o de terceros conviene revisar qué 
herramientas expone realmente y qué tan justificado está cada permiso. Un servidor que pide más 
capacidades de las que la tarea requiere amplía innecesariamente la superficie de riesgo 
(Identra, 2025).

### 7. Casos de uso

El Model Context Protocol (MCP) es un estándar abierto que actúa como un "conector universal" o USB-C para la inteligencia artificial. Permite que los entornos de ejecución y clientes de IA se conecten de manera nativa con bases de datos, APIs de terceros y sistemas de archivos locales sin necesidad de programar integraciones personalizadas para cada modelo.

A continuación, se presentan tres herramientas actuales que implementan MCP y la explicación de cómo logran modificar repositorios enteros de manera autónoma.

* **Tres herramientas actuales que implementan MC**

- **PGoogle Antigravity:** Es un entorno de desarrollo integrado (IDE) y ecosistema agéntico avanzado. Implementa MCP para conectar el agente de desarrollo nativo con servidores externos como GitHub MCP, bases de datos (AlloyDB) o automatizadores como N8N. El agente de Antigravity utiliza este protocolo para interactuar directamente con flujos de trabajo de ingeniería complejos e infraestructura de nube.
- **Claude Desktop (de Anthropic):** El cliente oficial de escritorio de Claude funciona como un host MCP nativo. Se configura mediante un archivo claude_desktop_config.json para añadir servidores MCP locales o remotos. Los usuarios lo emplean para dar la capacidad a Claude de interactuar con herramientas del sistema de archivos, entornos en contenedores de Docker, o conectarse a plataformas de diseño como Figma.
- **Cursor IDE:** Este popular editor de código enfocado en IA actúa como un host MCP. Permite añadir servidores MCP personalizados directamente desde su panel de configuraciones. Los desarrolladores lo utilizan para extender las habilidades del modelo dentro del entorno de desarrollo, dándole acceso directo a consultas SQL en producción, lectura de APIs de documentación actualizadas o terminales de ejecución locales mediante llamadas estandarizadas.

* **¿Cómo editan repositorios completos sin subir archivos manualmente?**

Estas herramientas no requieren que el usuario arrastre, copie o suba manualmente archivos a una interfaz web debido a la arquitectura cliente-servidor y al mecanismo de transporte local que define el protocolo MCP.
```
[ Modelo de IA (LLM) ]
        ↕
[ Host / Cliente MCP ]  ←── stdio (transmisión local) ──→  [ Servidor MCP de Archivos ]
   (Cursor / Antigravity)                                    (acceso al sistema)
                                                                      ↕
                                                          [ Tu Repositorio Local ]
```

El proceso técnico ocurre a través de los siguientes pasos:
- **Descubrimiento de herramientas de edición (Tools):** Cuando se inicia el entorno de desarrollo, el servidor MCP local expone un esquema de funciones (herramientas) predefinidas al cliente de IA. Estas herramientas incluyen operaciones estándar como read_file, write_file, grep_search o modify_code_block.
- **Canales de comunicación local (Transporte por stdio):** La comunicación entre el IDE (como Google Antigravity o Cursor) y el servidor MCP se realiza a través de la entrada/salida estándar (stdio) del sistema operativo. No hay servidores externos en la nube intermediando la transferencia del archivo; la IA envía instrucciones formateadas en JSON-RPC a un proceso que se ejecuta localmente en la máquina del usuario.
- **Mapeo de rutas locales:** El servidor de archivos MCP tiene acceso restringido pero directo al directorio raíz del repositorio abierto en el IDE. Cuando el desarrollador pide un cambio global ("Cambia el puerto de la app de 3000 a 5000 en todo el proyecto"), la IA no "descarga" los archivos, sino que invoca secuencialmente la herramienta del servidor MCP enviando la ruta exacta y el fragmento de código a modificar.
- **Ejecución y Modificación Directa:** El servidor local procesa la petición de la IA, manipula los archivos directamente en el disco duro utilizando funciones nativas del sistema operativo (Node.js, Python, etc.) y actualiza el repositorio en tiempo real.

De este modo, el agente puede escanear subcarpetas, reescribir múltiples archivos en segundos y preparar commits completos de manera 100% autónoma.

## Parte 2: 
---
## Referencias bibliográficas 

* Stryker, C. (2025, noviembre 26). Modelos de lenguaje de gran tamaño. Ibm.com. https://www.ibm.com/mx-es/think/topics/large-language-models
* (S/f). Cloudflare.com. Recuperado el 20 de septiembre de 2026, de https://www.cloudflare.com/es-es/learning/ai/what-is-large-language-model/
* Srinivasagan, G. (2025, enero 11). Evolution of language models. DEV Community. https://dev.to/gokulsg/evolution-of-language-models-163
* Ghaseminejad Raeini, M. (2025). The evolution of language models: From N-Grams to LLMs, and beyond. Natural Language Processing Journal, 12(100168), 100168. https://doi.org/10.1016/j.nlp.2025.100168
* (S/f-b). Dataversity.net. Recuperado el 20 de septiembre de 2026, de https://www.dataversity.net/articles/a-brief-history-of-large-language-models/
* Stryker, C. (2021, octubre 6). What are large language models (LLMs)? Ibm.com. https://www.ibm.com/think/topics/large-language-models
* Wang, Z., Chu, Z., Doan, T. V., Ni, S., Yang, M., & Zhang, W. (2025). History, development, and principles of large language models: an introductory survey. AI and Ethics, 5(3), 1955–1971. https://doi.org/10.1007/s43681-024-00583-7
* Gundersen, G. (s/f). A history of large language models. Gregorygundersen.com. Recuperado el 20 de septiembre de 2026, de https://gregorygundersen.com/blog/2025/10/01/large-language-models/
* Dang, K. (2023, noviembre 15). Language Model History — Before and After Transformer: The AI revolution. Medium. https://medium.com/@kirudang/language-model-history-before-and-after-transformer-the-ai-revolution-bedc7948a130
* QuarkAndCode. (2026, abril 26). A Brief History of Language Models: From Markov Chains to modern LLMs. Medium. https://medium.com/@QuarkAndCode/a-brief-history-of-language-models-from-markov-chains-to-modern-llms-30951b09cb08
* The history of large language models: From ELIZA to GPT-5. (s/f). Devot.Team. Recuperado el 20 de septiembre de 2026, de https://devot.team/blog/history-of-large-language-models
* Bergmann, D. (2025, agosto 7). ¿Qué es un modelo de razonamiento? Ibm.com. https://www.ibm.com/mx-es/think/topics/reasoning-model
* Ekole, M. (2025, febrero 20). Test-Time Compute for LLM Reasoning. Linkedin.com. https://www.linkedin.com/pulse/test-time-compute-llm-reasoning-mitterrand-ekole-ofege
* Huang, C. (2025, marzo 17). Understanding Reasoning Models & Test-Time Compute: Insights from DeepSeek-R1. Medium. https://medium.com/@cch.chichieh/understanding-reasoning-models-test-time-compute-insights-from-deepseek-r1-d30783070827
* (how) do reasoning models reason? (s/f). En arXiv. Recuperado el 20 de septiembre de 2026, de https://arxiv.org/html/2504.09762v1
* Raschka, S. (2026, julio 18). Controlling reasoning effort in LLMs. Ahead of AI. https://magazine.sebastianraschka.com/p/controlling-reasoning-effort-in-llms
* Chen, M. (2025, febrero 24). ¿Qué es una API (interfaz de programación de aplicaciones)? Oracle. Oracle.com. https://www.oracle.com/latam/cloud/cloud-native/api-management/what-is-api/
* Networks, R. [@RaiolaNetworks]. (s/f). Model context protocol (MCP), explicado para principiantes [[Object Object]]. Youtube. Recuperado el 21 de septiembre de 2026, de http://youtube.com/watch?v=3SL2-I7_EnE&t=51
* Model Context Protocol. (2025). Especificación del Model Context Protocol, revisión 2025-11-25. Anthropic. https://modelcontextprotocol.io/specification/2025-11-25
* A03 injection - OWASP top 10:2021. (s/f). Owasp.org. Recuperado el 21 de septiembre de 2026, de https://top10.owasp.org/2021/A03_2021-Injection/
* Banach, Z. (s/f). Injection attacks in application security: Types, examples, prevention. Invicti.com. Recuperado el 21 de septiembre de 2026, de https://www.invicti.com/blog/web-security/top-dangerous-injection-attacks
* CWE - CWE-22: Improper limitation of a pathname to a restricted directory ('path traversal’) (4.20). (s/f). Mitre.org. Recuperado el 21 de septiembre de 2026, de https://cwe.mitre.org/data/definitions/22.html
* Path Traversal. (s/f). Owasp.org. Recuperado el 21 de septiembre de 2026, de https://community.owasp.org/attacks/Path_Traversal
* (S/f). Owasp.org. Recuperado el 21 de septiembre de 2026, de https://owasp.org/projects/web-security-testing-guide/v41/4-Web_Application_Security_Testing/05-Authorization_Testing/01-Testing_Directory_Traversal_File_Include
* Identra. (2025). What are the security risks of MCP (Model Context Protocol)?https://www.identra.ai/glossary/mcp-security/
* Model Context Protocol. (2025). Security Best Practices. Especificación del Model Context Protocol, revisión 2025-11-25. https://modelcontextprotocol.io/specification/2025-11-25/basic/security_best_practices
* Open Web Application Security Project (OWASP). (2025). OWASP Top 10 for Agentic Applications.https://owasp.org/
* Supertrained. (2026). Why prompt injection hits harder in MCP: Scope constraints and blast radius. DEV Community.https://dev.to/supertrained/why-prompt-injection-hits-harder-in-mcp-scope-constraints-and-blast-radius-5d8o
* Zealynx. (2026). The 5 things that will get your MCP server hacked: A security checklist.https://www.zealynx.io/research/adversarial-security/mcp-security-checklist
* Dave, A. I. (2025, julio 17). Top 10 Model Context Protocol use cases: Complete guide for 2025. DaveAI. https://www.iamdave.ai/blog/top-10-model-context-protocol-use-cases-complete-guide-for-2025/
* Model context protocol (MCP). (s/f). Google Antigravity Docs. Recuperado el 21 de septiembre de 2026, de https://antigravity.google/docs/mcp/
* Codex Community [@CodexCommunity]. (s/f). Top 10 MCP use cases - using Claude & model context protocol [[Object Object]]. Youtube. Recuperado el 21 de septiembre de 2026, de https://www.youtube.com/watch?v=lzbbPBLPtdY
* Tools. (s/f). Modelcontextprotocol.info. Recuperado el 21 de septiembre de 2026, de https://modelcontextprotocol.info/docs/concepts/tools/
* What is Model Context Protocol (MCP)? A guide. (s/f). Google Cloud. Recuperado el 21 de septiembre de 2026, de https://cloud.google.com/discover/what-is-model-context-protocol
* Beura, R. K. (2025, octubre 4). Top 5 MCP Server Platforms: A Comprehensive Developer’s Guide to the model context protocol…. Medium. https://medium.com/@ommranjit/top-5-mcp-server-platforms-a-comprehensive-developers-guide-to-the-model-context-protocol-35772bab5312




