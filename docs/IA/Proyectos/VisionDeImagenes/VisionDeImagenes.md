---
title: Visión de imágenes
---

# Visión de Imágenes

Las pruebas se realizaron enviando distintas imágenes junto con prompts específicos. Se implementó un botón funcional: 
- **Analizar firma**: Al presionarlo se envía la imágen ingresada en el selector de archivos y se envía junto con el prompt: 

    > *“Analiza la imagen y determina si la firma fue hecha a mano alzada o digitalmente.”*

## Contexto de los ejemplos

Se utilizó la misma firma en ambos análisis, en su respectivo formato digital y a mano alzada. 

## Firma digital realizada a mano alzada

### Imagen utilizada:



### Resultado 1 – Análisis general:


### Resultado 2 – Descripción de la imagen:


### Conclusiones:

* Los modelos de visión de imágenes suelen interpretar mejor imágenes con fondo uniforme, ya que esto facilita la identificación de los elementos presentes.
* En imágenes PNG con fondo transparente y elementos oscuros (como firmas negras), algunos modelos pueden interpretar el fondo como negro, haciendo que el contenido se mezcle y sea indetectable.
* Agregar un fondo a las imágenes mejora significativamente la precisión del análisis, al generar el contraste necesario para diferenciar los elementos.
* Además del contenido visual, el modelo puede tener en cuenta metadatos implícitos (como resolución, formato o paleta de colores), lo que contribuye a generar respuestas más detalladas y precisas.

## Firma realizada en papel



### Contexto:

En este caso, se utilizó una imagen de una firma realizada con bolígrafo sobre papel blanco. La claridad del fondo y la nitidez del trazo facilitan el reconocimiento y análisis por parte del modelo de visión.

