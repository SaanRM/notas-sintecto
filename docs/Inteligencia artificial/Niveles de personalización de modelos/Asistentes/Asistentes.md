---
title: 2. Asistentes (Estructurada)
sidebar_position: 2
---


**API de asistentes**

La API de asistentes permite crear asistentes de IA configurables, integrándolos dentro de tus aplicaciones. Cada asistente tiene instrucciones iniciales, puede usar modelos de OpenAI y acceder a herramientas como **intérprete de código**, **búsqueda de archivos** y **llamada a funciones**. 

En esencia, un asistente funciona como un flujo normal de prompts, pero facilita la programación al centralizar instrucciones, herramientas y archivos, reduciendo la necesidad de repetir contexto manualmente en cada solicitud. Esto agiliza el desarrollo, aunque no cambia las capacidades del modelo en sí: simplemente organiza mejor los flujos.

El costo de uso sigue siendo el mismo que el de prompts normales (tokens input/output del modelo), aunque integrar herramientas puede incrementar el costo total de una interacción.

El manejo del contexto se realiza mediante **hilos persistentes** ("threads"): sesiones de conversación donde se almacenan automáticamente los mensajes y se ajusta su longitud cuando crecen demasiado, evitando la pérdida de continuidad y facilitando interacciones más naturales.
