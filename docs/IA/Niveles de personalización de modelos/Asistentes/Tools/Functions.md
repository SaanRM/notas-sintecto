---
title: Functions (Funciones)
---

# Functions (Funciones)

Las **llamadas a funciones** permiten que el modelo devuelva, en lugar de un texto libre, un objeto JSON con los argumentos necesarios para invocar un procedimiento externo (por ejemplo, obtener el clima, realizar una suma, consultar una base de datos, etc.).



## Funcionamiento general

1. **Definición de la función**  
   Cada función se describe con un objeto que incluye:  
   - **name**: identificador único (sin espacios ni caracteres especiales).  
   - **description**: breve explicación de su finalidad.  
   - **parameters**: esquema JSON Schema que define:
     - Tipos de datos (`string`, `number`, `boolean`, `object`, `array`).
     - Restricciones (`enum`, `minimum`, `maxLength`, etc.).
     - Campos obligatorios (`required`).
     - Prohibición de propiedades adicionales (`additionalProperties: false`).

2. **Detección automática**  
   Cuando el modelo detecta en la conversación la intención adecuada, en lugar de responder con texto natural, devuelve un mensaje con la llamada a la función:
   ```json
   {
     "name": "get_weather",
     "arguments": {
       "location": "Bogotá, Colombia",
       "unit": "c"
     }
   }
   ```

3. **Ejecución externa y retorno**  
   - El backend recibe ese JSON, invoca realmente la función (p.ej. llama a una API de clima).  
   - Luego envía de vuelta al modelo un mensaje con rol `function`, conteniendo el resultado:
     ```json
     {
       "role": "function",
       "name": "get_weather",
       "content": "{ \"temp\": 18, \"condition\": \"nublado\" }"
     }
     ```
   - El modelo integra ese contenido en la conversación y devuelve un mensaje de texto al usuario.



## Ejemplo: función para sumar dos números

1. **Definición de la función**  
   ```json
   {
     "name": "add_numbers",
     "description": "Suma dos números y devuelve el resultado",
     "parameters": {
       "type": "object",
       "properties": {
         "a": {
           "type": "number",
           "description": "Primer sumando"
         },
         "b": {
           "type": "number",
           "description": "Segundo sumando"
         }
       },
       "required": ["a", "b"],
       "additionalProperties": false
     }
   }
   ```

2. **Petición al modelo**  
   ```json
   {
     "model": "gpt-3.5-turbo-0613",
     "messages": [
       { "role": "user", "content": "¿Cuánto es 4 más 7?" }
     ],
     "functions": [
       /* definición de la función add_numbers aquí */
     ],
     "function_call": "auto"
   }
   ```

3. **Respuesta del modelo (function_call)**  
   ```json
   {
     "role": "assistant",
     "content": null,
     "function_call": {
       "name": "add_numbers",
       "arguments": "{\"a\":4,\"b\":7}"
     }
   }
   ```
:::note
**Orquestación en el backend**  
Tras la respuesta de la función, el backend debe:  
- Comprobar si el mensaje del modelo incluye `function_call`.  
- Extraer `name` y `arguments`, ejecutar internamente la lógica correspondiente (p. ej. `add_numbers`).  
- Enviar una segunda petición al modelo, añadiendo al historial un mensaje de rol `function` con el resultado JSON.  
- Recibir el texto final del modelo, que integra automáticamente el resultado de la función.
:::

4. **Ejecución en el backend**  
   ```js
   // Ejemplo en JavaScript
   const args = JSON.parse(call.arguments);       // { a: 4, b: 7 }
   const result = args.a + args.b;                // 11
   ```

5. **Reenvío al modelo**  
   ```json
   {
     "role": "function",
     "name": "add_numbers",
     "content": "{\"result\":11}"
   }
   ```

6. **Respuesta final del modelo**  
   ```json
   {
     "role": "assistant",
     "content": "El resultado de sumar 4 y 7 es 11."
   }
   ```

## Ejemplos habituales de funciones

- **get_news**: obtiene titulares y resúmenes de noticias.  
- **translate_text**: traduce fragmentos de texto.  
- **create_calendar_event**: añade eventos a un calendario.  
- **query_database**: ejecuta consultas SQL.  
- **process_payment**: inicia transacciones financieras.  
- **generate_image**: coordina la generación de imágenes.  

Cada una se define mediante su propio esquema para que el modelo entienda cuándo y cómo invocarla.



## Flujo de interacción con la API

1. Envío de la petición a `/v1/chat/completions`, incluyendo:
   - Mensajes de usuario.
   - Array de descripciones de funciones.
   - `"function_call": "auto"`.
2. Recepción de un mensaje con `"function_call"` (nombre + argumentos).
3. Ejecución de la función en el sistema propio.
4. Reenvío de la respuesta de la función como mensaje de rol `function`.
5. Continuación de la conversación, integrando el resultado obtenido.



Con este mecanismo, el modelo puede “enchufarse” a cualquier servicio externo definido como función, garantizando una comunicación estructurada y fácil de procesar.