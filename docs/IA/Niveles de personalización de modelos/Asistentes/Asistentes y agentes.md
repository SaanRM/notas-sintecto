---
title: Diferencia entre agentes y asistentes
---

Aunque en la documentación de OpenAI se pueden ver ambos términos, **"agentes"** y **"asistentes"** no son exactamente lo mismo, aunque están estrechamente relacionados:

### **Asistentes (`assistants`)**
Es un recurso específico de la **Assistants API**. Un "asistente" en este contexto es una configuración persistente que define:

- Un modelo (por ejemplo, `gpt-4-turbo`)
- Un `system prompt` (personalidad o instrucciones)
- Herramientas disponibles (funciones, búsqueda, archivos, código)
- Configuración predeterminada

Este asistente puede ser reutilizado en múltiples sesiones (o "threads").

### **Agentes**
"Agente" es un concepto más general que se refiere a un sistema que **razona, planifica y actúa** de forma autónoma, posiblemente a través de múltiples pasos, invocando herramientas y manteniendo contexto.

> **En OpenAI**, los asistentes creados con la **Assistants API**, junto con los threads y tools, **pueden considerarse agentes**, porque permiten:
> - Planificación multietapa
> - Uso automático de herramientas
> - Seguimiento de contexto
> - Razonamiento estructurado