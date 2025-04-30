---
title: Functions
---

# Functions (funciones)

## 1. Tabla Comparativa: Uso normal vs. Uso de Functions

| Aspecto | Sin Functions (prompt tradicional) | Con Functions (Assistant con funciones configuradas) |
|:---|:---|:---|
| **Modo de invocar APIs** | Manual: Incluir en el prompt instrucciones sobre llamadas API, interpretar texto de la respuesta manualmente | Automático: El modelo estructura la llamada, ejecuta la función y procesa su respuesta |
| **Costo adicional** | Solo tokens del prompt y respuesta | Solo tokens del prompt, más los tokens generados por la definición y ejecución de functions |
| **Complejidad** | Alta: requiere explicar la API al modelo | Baja: se define una vez la function, luego el modelo la usa automáticamente |
| **Eficiencia** | Menor: propenso a errores de interpretación | Mayor: llamada precisa y estructurada |
| **Ideal para** | Casos simples o donde no se pueda usar Assistants | Casos complejos o donde se requiere lógica integrada, workflows dinámicos |
| **Precios de tokens** | Igual | Igual (el único impacto es la cantidad de tokens, no un costo fijo extra) |

---

## 2. Costos detallados

- Tanto en prompts normales como usando Functions, el modelo cobra **por cantidad de tokens**, no por tipo de operación.
- **Functions no tienen costo adicional por su uso**, solo:
  - Tokens de definición de la función (normalmente pequeñas, unos 300–500 tokens).
  - Tokens de la llamada a la función (input/output, típicamente 100–300 tokens extra).
- **Ejemplo de impacto económico mínimo**:
  - Llamada a Function + su respuesta puede costar entre **$0.0005 y $0.002 USD** por llamada.

---

## 3. ¿Dónde se pueden usar Functions?

| Aspecto | Detalle |
|:---|:---|
| **En Assistants (API de Assistants)** | ✅ Sí, Functions están totalmente soportadas. |
| **En chat/completion API normal (sin Assistant)** | ⚠️ Parcial: solo algunos modelos permiten usar `function_calling` manualmente (por ejemplo, GPT-4-turbo vía `chat/completions`). |
| **Desde OpenAI Playground** | ✅ Sí, si se habilita `Function Calling` en las opciones avanzadas. |
| **Desde Dashboard en plataforma de Assistants** | ✅ Sí, mediante creación/configuración de Assistant. |

**Importante:**  
- Functions integradas de forma automática (sin necesidad de manejar `function_call` manualmente) **solo están completamente disponibles en la plataforma de Assistants**.
- Usar `functions` directamente en `chat/completions` API requiere más trabajo: se debe interpretar manualmente el `function_call` retornado y ejecutar la llamada.

---

## ✅ Resumen Final

> Usar **Functions** en Assistants de OpenAI no implica un costo directo adicional, sino únicamente un ligero incremento en tokens utilizados.  
>  
> Functions permiten automatizar llamadas a APIs de manera estructurada, más segura y más eficiente que instructing al modelo vía texto plano.  
>  
> Las Functions están diseñadas para ser usadas principalmente dentro de **Assistants**, pero también pueden ser utilizadas de manera manual en algunas APIs (chat/completions) que soporten `function_calling`.