---
title: 🎭 Niveles de personalización de modelos
sidebar_position: 1
---

### Existen tres niveles de personalización principales para la interacción con modelos de IA:

1. **Flujo de prompts**  
   - Consiste en enviar en cada llamada el rol, el contexto y las herramientas de forma manual; proporciona control total sobre cada interacción, a costa de repetir las mismas instrucciones en cada petición.

2. **Assistants (Asistentes)**  

   - Permite crear un asistente único que almacena de forma persistente sistema, contexto, herramientas y archivos; simplifica la integración al gestionar internamente el estado y los metadatos necesarios en cada llamada.

3. **Fine-tuning (Ajuste fino)**  
   - Implica reentrenar el modelo con datos de ejemplo para incorporar comportamientos o estilos específicos de forma permanente, de modo que no sea necesario volver a enviar contexto ni instrucciones adicionales en cada solicitud.

:::info

Se realizó una prueba desde el **[playground de la plataforma de OpenAI](https://platform.openai.com/playground)** con el fin de medir la cantidad total de tokens consumidos (entrada y salida) bajo las mismas condiciones iniciales en las tres categorías. Se inició un chat solicitando asistencia básica y se interrumpió la conversación cuando el uso aproximado alcanzó los 1 000 tokens.

De esta manera podemos comparar de forma directa qué tipo de personalización es más o menos eficiente en el consumo de tokens. En cada pestaña de esta sección se incluye la conversación completa utilizada, y los resultados finales se presentan al final de la misma.

En la página de cada tipo de personalización se incluye una explicación más detallada de cómo funciona cada método, la conversación realizada y un resumen de los datos.

En la página **[✅ Resultados y comparación de la prueba](./Resultados%20y%20comparación.md)** se encuentra un resumen y una conclusión de todos los datos obtenidos.

:::
