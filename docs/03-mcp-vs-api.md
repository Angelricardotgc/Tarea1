# 3. MCP frente a una API 
 
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

