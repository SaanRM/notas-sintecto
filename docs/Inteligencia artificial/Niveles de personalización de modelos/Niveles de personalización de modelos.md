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
