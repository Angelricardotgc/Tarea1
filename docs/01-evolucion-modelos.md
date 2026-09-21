# 1. Evolución de los modelos 

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

