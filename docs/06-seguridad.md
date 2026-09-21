# 6. Seguridad

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
