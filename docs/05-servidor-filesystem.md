# 5. El servidor de sistemas de archivos 

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
