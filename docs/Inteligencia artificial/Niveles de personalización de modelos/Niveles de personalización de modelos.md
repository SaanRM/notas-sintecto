---
title: 🎭 Niveles de personalización de modelos
---

Existen tres niveles de personalización para la interacción con modelos de IA:

1. **Prompt normal**  
   - Cada solicitud envía explícitamente el rol, el contexto y la definición de funciones (“tools”) de forma manual. Es flexible y permite controlar cada petición de manera precisa, pero requiere repetir constantemente las instrucciones. Solo se paga el coste base de tokens (entrada y salida), aunque si se utilizan herramientas, el coste de la interacción puede aumentar.

2. **Assistants API**  
   - Permite definir de forma persistente un conjunto de instrucciones, contexto, herramientas y archivos asociados a un asistente configurado una sola vez mediante dashboard o API. Funciona igual que los prompts normales a nivel técnico, pero facilita el desarrollo al centralizar y automatizar la gestión de contexto y funciones. El coste es el mismo que en prompts normales, con la posibilidad de aumento si se utilizan herramientas adicionales.

3. **Fine-tuning**  
   - Consiste en reentrenar el modelo con ejemplos personalizados para que adopte de forma permanente un comportamiento específico, sin necesidad de enviar prompts de contexto en cada solicitud. Este método implica un coste inicial por el entrenamiento y, posteriormente, tarifas de uso diferenciadas (input, output, cache) que son más elevadas que las del modelo base.