# 7. Casos de uso

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
