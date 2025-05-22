---
title: Google
sidebar_position: 1
---

## Precios de la API

### Cómo funcionan los límites de frecuencia
Los límites de frecuencia se miden en cuatro dimensiones:

### Número de solicitudes
- Solicitudes por minuto (RPM)
- Solicitudes por día (RPD)

### Número de tokens consumidos
- Tokens por minuto (TPM)
- Tokens por día (TPD)

### Tabla de precios por modelo en la capa gratuita

## Gemini 2.5
| Modelo                                            | Referencia | Solicitudes por minuto |  Solicitudes por dia | Solicitudes mensuales gratuitas (30 dias) | 
|--|--|--|--|--|
| Versión preliminar de Gemini 2.5 Flash (05/20)    | gemini-2.5-flash-preview-04-17            | 10 | 500    | 15.000  | 
| Versión preliminar de Gemini 2.5 Flash (04/17)    | gemini-2.5-flash-preview-05-20            | 10 | 500    | 15.000  | 

## Gemini 2.0
| Modelo                                            | Referencia | Solicitudes por minuto |  Solicitudes por dia | Solicitudes mensuales gratuitas (30 dias) | 
|--|--|--|--|--|
| Gemini 2.0 Flash                                  | gemini-2.0-flash                           | 15 | 1.000  | 30.000  | 
| Gemini 2.0 Flash-Lite                             | gemini-2.0-flash-lite                      | 30 | 1.500  | 45.000  | 
| gemini-2.0-flash-preview-image-generation         | gemini-2.0-flash-preview-image-generation  | 10 | 1.500  | 45.000  | 

## Gemini 1.5
| Modelo                                            | Referencia | Solicitudes por minuto |  Solicitudes por dia | Solicitudes mensuales gratuitas (30 dias) |
|--|--|--|--|--|
| Gemini 1.5 Flash                                  | gemini-1.5-flash                           | 15 | 500    | 15.000  |
| Gemini 1.5 Flash-8B                               | gemini-1.5-flash-8b                        | 15 | 500    | 15.000  |

## Gemma
| Modelo                                            | Referencia | Solicitudes por minuto |  Solicitudes por dia | Solicitudes mensuales gratuitas (30 dias) |
|--|--|--|--|--|
| Gemma 3 1B                                        | gemma-3-1b-it                              | 30 | 14.400 | 432.000 |
| Gemma 3 4B                                       | gemma-3-4b-it                              | 30 | 14.400 | 432.000 |  
| Gemma 3 12B                                       | gemma-3-12b-it                             | 30 | 14.400 | 432.000 |  
| Gemma 3 27B                                       | gemma-3-27b-it                             | 30 | 14.400 | 432.000 |  
| Gemma 3n E4B                                      | gemma-3n-e4b-it                            | 30 | '' '' | '' '' |  

### Uso real

Para utilizar al máximo la cuota diaria de **14 400 solicitudes** del modelo `gemma-3n-e4b-it` sin exceder el límite de **30 solicitudes por minuto**, se debe espaciar cada solicitud en **6 segundos**.

### Resumen:

* **Intervalo óptimo**: 1 solicitud cada **6 segundos**.

* **Solicitudes por minuto**: 10.

* **Solicitudes por día**: 10 (Solicitudes por minuto) × 1.440 minutos (24 horas) = **14 400 minutos**.

Este ritmo asegura el cumplimiento de ambos límites: el diario y el por minuto.

## Explicaciones modelos Gemma:

### https://deepmind.google/models/gemma/?hl=es-419

- gemma-3n-e4b-it está relacionado con gemma-3-4b-it, comparten las mismas estadisticas de uso
- gemma-3-1b-it, gemma-3-12b-it y gemma-3-27b-it son independientes entre si y de los modelos gemma de 4b-it

<br/>

1. Hay discrepancias entre los datos de:
    - https://aistudio.google.com/prompts/new_chat
    - https://ai.google.dev/gemini-api/docs/rate-limits?hl=es-419#free-tier

2. Hay discrepancias entre los datos de:
    - https://aistudio.google.com/prompts/new_chat
    - El uso en la consola de Google.

3. Los datos reales son los de la consola de Google.

