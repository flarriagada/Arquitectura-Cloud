# Arquitectura-Cloud

# 1. Necesidad de negocio, usuarios y alcance

## 1.1. Necesidad de negocio

Los call centers generan grabaciones de las conversaciones entre sus agentes y clientes, las cuales contienen información potencialmente útil para analizar las interacciones, identificar motivos de contacto y reconocer problemas recurrentes. Sin embargo, esta información se encuentra almacenada principalmente en archivos de audio, por lo que requiere un procesamiento previo para transformarse en datos organizados y consultables.

Para obtener estos resultados, las empresas necesitan contar con mecanismos de almacenamiento, transcripción, procesamiento y análisis de datos, lo que implica disponer de infraestructura tecnológica, capacidad de cómputo y recursos para su operación y mantenimiento. Además, procesar las grabaciones de manera individual dificulta consolidar la información y reconocer patrones presentes en múltiples conversaciones.

En este contexto, se identifica la necesidad de contar con un servicio externo que permita delegar el procesamiento de las grabaciones y obtener transcripciones y métricas analíticas de manera estructurada. Esto permitiría que los supervisores y analistas de cada empresa puedan consultar información sobre los motivos de contacto, reclamos y temas recurrentes, sin necesidad de desarrollar y administrar internamente toda la infraestructura necesaria para generar estos resultados.

## 1.2. Usuarios del sistema

La plataforma está orientada a un modelo de negocio B2B (*Business to Business*), en el cual distintas empresas que operan call centers pueden utilizar un mismo servicio de procesamiento y análisis de grabaciones.

Se identifican los siguientes usuarios:

- **Cliente empresarial:** empresas que operan call centers y requieren procesar las grabaciones de sus llamadas. Son quienes contratan el servicio y proporcionan los archivos de audio.

- **Usuarios principales:** supervisores, analistas de datos y analistas de calidad de las empresas clientes. Utilizan las transcripciones y métricas generadas para consultar información, identificar patrones, comparar períodos y realizar análisis según las necesidades de su organización.

- **Usuarios técnicos:** personal responsable de administrar y supervisar el funcionamiento de la plataforma, incluyendo el seguimiento de trabajos de procesamiento, detección de errores y mantenimiento operacional.

Debido a que la plataforma está diseñada para atender a múltiples empresas, cada cliente deberá acceder únicamente a sus propias grabaciones, transcripciones y resultados. La separación de información entre empresas constituye un requisito fundamental del sistema.

## 1.3. Propuesta de valor

La propuesta consiste en ofrecer una plataforma cloud de procesamiento posterior a las llamadas (*post-call processing*) que permita a las empresas externalizar el almacenamiento, la transcripción y el análisis de sus grabaciones.

A diferencia de un servicio limitado a convertir audio en texto, la plataforma buscará transformar las conversaciones en información estructurada mediante la identificación de tipos de interacción, términos relevantes, temas recurrentes y métricas descriptivas. Los resultados podrán consultarse por empresa y período, proporcionando información que cada cliente podrá utilizar para sus propios análisis y decisiones.

El valor del servicio se encuentra tanto en facilitar el acceso a información obtenida de las conversaciones como en permitir que las empresas deleguen la infraestructura y operación tecnológica necesarias para procesarlas.

## 1.4. Alcance del proyecto

El proyecto contempla el diseño de una plataforma B2B capaz de recibir grabaciones de llamadas finalizadas de distintas empresas, procesarlas de manera asíncrona y generar transcripciones junto con resultados analíticos asociados a su contenido.

El alcance inicial considera las siguientes funcionalidades:

1. Recepción y almacenamiento de archivos de audio previamente grabados.
2. Procesamiento asíncrono de las grabaciones.
3. Generación de transcripciones automáticas.
4. Extracción de métricas descriptivas y términos relevantes.
5. Clasificación estimada de las conversaciones según el tipo de interacción: consulta, reclamo o solicitud.
6. Identificación de temas recurrentes mediante categorías y vocabularios definidos.
7. Consolidación de resultados analíticos por empresa y período.
8. Disponibilidad de transcripciones, métricas y resultados para su consulta.
9. Registro del estado de procesamiento y de posibles errores.
10. Separación de información y accesos entre las distintas empresas clientes.

Se considera un procesamiento por lotes (*batch*), realizado después de que las llamadas hayan finalizado. La plataforma no participa directamente en las conversaciones ni realiza su análisis en tiempo real.

La clasificación del contenido será una estimación automática, por lo que deberá contemplar resultados inciertos y mecanismos de evaluación de su calidad. La técnica específica de clasificación se definirá posteriormente, considerando la viabilidad del proyecto y las pruebas disponibles.

### Funcionalidades fuera del alcance

El proyecto no contempla el desarrollo de una central telefónica, un sistema de grabación de llamadas, un CRM, chatbots, asistentes de atención en tiempo real ni mecanismos para responder automáticamente a los clientes.

Asimismo, se excluye del alcance inicial la evaluación automática de la calidad de atención de los agentes, como el cumplimiento de protocolos, la efectividad de las respuestas o la resolución definitiva de problemas.

La plataforma se enfocará en caracterizar el contenido de las conversaciones y no en evaluar individualmente el desempeño de los trabajadores.

La generación de recomendaciones de negocio también queda fuera del alcance. La plataforma proporcionará información analítica, mientras que cada empresa será responsable de interpretar los resultados y decidir las acciones que considere pertinentes.

---

# 2. Resultados entregados por la plataforma

## 2.1. Descripción general

La plataforma entregará a cada empresa sus transcripciones y un conjunto de métricas obtenidas mediante el procesamiento y consolidación de las llamadas. Los resultados se organizarán en dos niveles: información individual por conversación e indicadores agregados por empresa y período.

El objetivo es que los analistas y supervisores puedan acceder tanto al contenido de una llamada específica como a información que describa patrones presentes en el conjunto de conversaciones procesadas.

Para ello, se consideran tres grupos de resultados: transcripciones individuales, métricas analíticas sobre el contenido y métricas operacionales del procesamiento.

## 2.2. Transcripciones individuales

Cada grabación procesada contará con una transcripción asociada a su identificador de llamada y a la empresa correspondiente.

Junto con la transcripción se conservarán metadatos como fecha, duración y estado de procesamiento, además de los resultados analíticos individuales que puedan obtenerse de la conversación.

Las transcripciones permitirán que los usuarios autorizados consulten el contenido y revisen el contexto de las clasificaciones y términos identificados. Debido a que el reconocimiento automático de voz puede contener errores, estas transcripciones no se considerarán representaciones necesariamente exactas de todo lo expresado durante la llamada.

## 2.3. Métricas analíticas sobre el contenido

Estas métricas constituyen el principal valor analítico de la plataforma, ya que buscan transformar las conversaciones en información que permita comprender qué temas y tipos de interacción aparecen entre los clientes de una empresa.

### A. Clasificación del tipo de interacción

La plataforma buscará clasificar las conversaciones según tres tipos generales:

- **Consulta:** interacción en la que el cliente busca información, orientación o aclaraciones.
- **Reclamo:** interacción en la que el cliente manifiesta una disconformidad respecto de un producto, servicio o situación.
- **Solicitud:** interacción en la que el cliente requiere que la empresa realice una acción, gestión o trámite.

Estas categorías se proponen como una clasificación general aplicable a distintos tipos de call centers, independientemente del sector al que pertenezcan.

La plataforma permitirá obtener la cantidad y proporción de llamadas asociadas a cada tipo de interacción y comparar su distribución entre diferentes períodos.

Se deberá contemplar que una conversación puede incluir más de una intención. Por ello, la asignación de categorías múltiples, la selección de una categoría predominante y el tratamiento de casos indeterminados deberán definirse en las reglas de clasificación.

### B. Identificación de términos relevantes

Se identificarán palabras y expresiones relevantes presentes en las transcripciones para conocer qué conceptos aparecen con mayor frecuencia en las conversaciones.

El análisis permitirá distinguir entre la cantidad total de apariciones de un término y el número de llamadas diferentes en las que se menciona. Esto evita interpretar la repetición de una palabra dentro de una misma llamada como evidencia de que está presente en muchas conversaciones.

El conjunto de términos relevantes podrá considerar vocabularios configurables según las necesidades de cada empresa. Asimismo, se deberán establecer criterios para excluir palabras de escaso valor analítico y evitar exponer información personal.

### C. Identificación de temas recurrentes

A partir del contenido de las transcripciones, la plataforma buscará identificar temas que aparezcan repetidamente en las conversaciones de una empresa.

A diferencia del tipo de interacción, que describe la naturaleza de la conversación, el tema representa el asunto tratado. Por ejemplo, una llamada puede clasificarse como reclamo y estar asociada al tema de facturación.

Para mantener la plataforma aplicable a diferentes empresas, se propone utilizar categorías temáticas configurables según el contexto de cada cliente. La identificación inicial podrá apoyarse en términos o reglas asociadas a esas categorías, cuya calidad deberá evaluarse.

Se podrán generar indicadores sobre la frecuencia de estos temas, considerando la cantidad de llamadas en las que aparecen.

### D. Evolución de tipos de interacción y temas

Los resultados se consolidarán por empresa y período, permitiendo observar cómo varía la frecuencia de determinadas categorías, términos y temas a lo largo del tiempo.

De esta manera, los analistas podrán comparar la presencia de distintos motivos de contacto entre períodos, sin que la plataforma tenga que interpretar automáticamente las causas de sus variaciones ni recomendar acciones específicas.

## 2.4. Métricas operacionales

De manera complementaria al análisis del contenido, la plataforma proporcionará métricas descriptivas sobre las grabaciones y su procesamiento.

Se consideran inicialmente:

| Métrica | Descripción |
|---|---|
| Cantidad de llamadas procesadas | Número de grabaciones cuyo procesamiento finalizó correctamente durante el período considerado. |
| Horas de audio procesado | Duración total del audio correspondiente a las llamadas procesadas. |
| Duración promedio | Promedio de duración de las grabaciones incluidas en el análisis. |
| Tiempo de procesamiento | Tiempo transcurrido durante el procesamiento de una grabación, según los puntos de inicio y término que se definan. |
| Tasa de trabajos fallidos | Proporción de trabajos que no finalizaron correctamente, según los criterios que se establezcan. |

Estas métricas permitirán conocer el volumen de información procesada y el funcionamiento del servicio. No se utilizarán por sí solas como indicadores de la calidad de atención de los agentes.

## 2.5. Consulta y utilización de resultados

Los resultados estarán organizados por empresa, permitiendo realizar consultas sobre llamadas individuales y obtener indicadores agregados correspondientes a períodos específicos.

Los usuarios autorizados podrán consultar las transcripciones y los resultados analíticos de su empresa, manteniendo la separación de información respecto de los demás clientes de la plataforma.

La entrega de información se enfocará inicialmente en disponer de datos estructurados y consultas analíticas. El desarrollo de un dashboard completo no se considera un requisito del alcance inicial.

La plataforma no determinará qué decisiones debe tomar cada empresa a partir de los resultados obtenidos. Su responsabilidad será generar información consultable, trazable y acompañada de las limitaciones correspondientes.

## 2.6. Consideraciones y limitaciones

La clasificación automática de las conversaciones y la identificación de temas recurrentes constituyen capacidades propuestas para el sistema, cuya precisión y viabilidad técnica deberán evaluarse durante el desarrollo.

Los resultados podrían verse afectados por errores de transcripción, expresiones ambiguas, diferencias de vocabulario y características particulares de cada empresa.

Por ello, el sistema deberá contemplar categorías indeterminadas, mantener referencias a las transcripciones y permitir que los resultados puedan ser contrastados con su contenido original.

Las definiciones exactas de cálculo, reglas de clasificación, períodos de agregación, tratamiento de duplicados y criterios de evaluación se desarrollarán en la siguiente etapa de especificación de métricas.


# 3. Especificación de métricas y reglas de análisis

## 3.1. Criterios generales

Las métricas generadas por la plataforma se calcularán a partir de las grabaciones procesadas y sus respectivas transcripciones, manteniendo la identificación de la empresa a la que pertenece cada llamada.

Para evitar duplicidades, cada llamada deberá contar con un identificador único dentro de su empresa. Los reintentos de procesamiento no deberán generar registros adicionales en los resultados analíticos.

Se distinguirán dos grupos de indicadores: métricas relacionadas con el contenido de las conversaciones y métricas operacionales asociadas al volumen de grabaciones y al funcionamiento de la plataforma.

Los indicadores analíticos utilizarán como referencia la fecha original de cada llamada, permitiendo comparar los resultados entre períodos. Las métricas de funcionamiento utilizarán los registros de ejecución del procesamiento.

Los resultados agregados incluirán únicamente llamadas cuyo procesamiento haya finalizado correctamente, salvo los indicadores destinados específicamente a medir errores. Las llamadas con fallos, pendientes o sin información suficiente se identificarán de manera diferenciada.

## 3.2. Métricas analíticas del contenido

### Distribución de tipos de interacción

Se calculará la cantidad y proporción de llamadas clasificadas según su tipo de interacción. Inicialmente se consideran las categorías consulta, reclamo y solicitud, además de categorías para conversaciones mixtas o indeterminadas.

La proporción de cada categoría se calculará dividiendo la cantidad de llamadas asociadas a ella por el total de llamadas procesadas correctamente durante el período considerado.

Los criterios para asignar estas categorías se definirán en las reglas de clasificación, evitando que conversaciones ambiguas sean asignadas arbitrariamente.

### Frecuencia de temas recurrentes

Se calculará la cantidad de llamadas asociadas a cada tema identificado en las transcripciones.

Los temas podrán variar según el contexto de cada empresa. Una conversación podrá asociarse a más de un tema cuando su contenido lo justifique.

La frecuencia de un tema se calculará considerando el número de llamadas distintas en las que fue identificado, evitando que las menciones repetidas dentro de una misma conversación incrementen artificialmente el número de llamadas asociadas.

### Frecuencia de términos relevantes

Se identificarán las apariciones de palabras y expresiones relevantes dentro de las transcripciones.

Para cada término se distinguirán dos medidas: su frecuencia total de aparición y la cantidad de llamadas distintas en las que se encuentra presente.

Se establecerán criterios de normalización y exclusión de palabras comunes, además de mecanismos para evitar que información personal sea presentada como parte de los términos frecuentes.

### Evolución temporal de indicadores

Los indicadores anteriores podrán agruparse por períodos para analizar sus variaciones.

Se podrán comparar cantidades y proporciones de tipos de interacción, frecuencia de temas y presencia de términos relevantes entre períodos.

Estas comparaciones describirán cambios observados en las conversaciones procesadas, sin atribuir automáticamente sus causas ni emitir recomendaciones de negocio.

## 3.3. Métricas operacionales

De forma complementaria, la plataforma calculará indicadores que permitan conocer el volumen de grabaciones procesadas y el funcionamiento del servicio.

Se consideran la cantidad de llamadas procesadas correctamente, el volumen total de audio en horas, la duración promedio de las grabaciones, el tiempo de procesamiento y la tasa de trabajos fallidos.

Estos indicadores se calcularán a partir de los metadatos de las llamadas y los registros de procesamiento. Su finalidad será describir la operación del servicio, sin utilizarlos como medidas directas de la calidad de atención de los agentes.

## 3.4. Consideraciones sobre los resultados

Las métricas obtenidas mediante la transcripción y clasificación automática estarán sujetas a posibles errores de reconocimiento e interpretación.

Por ello, las clasificaciones deberán contemplar resultados inciertos y conservar referencias a las transcripciones originales para permitir su revisión.

La selección del método de clasificación y los criterios de evaluación de su calidad se desarrollarán posteriormente, considerando las características de las conversaciones y la viabilidad técnica de la plataforma.
