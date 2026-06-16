# Insumo 5 — Reclamo por diferencia de color + notas técnicas

**Ejercicio:** "La disculpa por una diferencia de color" (Tema 5 · Evaluar la respuesta).

El modelo redacta una respuesta al reclamo. Tu trabajo es **evaluarla** con los 5 criterios y
volver a preguntar **en neutro** para evitar la adulación. Las notas técnicas del final son tu
referencia para verificar si la explicación del modelo es correcta.

---

## A) Correo de reclamo del cliente

> **De:** Diego Tapia — Estudio Norte (agencia)
> **Asunto:** Problema con el color de los folletos
>
> Hola:
>
> Recibimos los folletos y el azul del fondo se ve mucho más apagado y verdoso que en el
> archivo que les mandamos. En mi pantalla se veía un azul vivo, casi eléctrico, y lo impreso
> parece otro color. El cliente final lo va a notar. ¿Qué pasó y cómo lo solucionamos?
>
> Diego.

## B) Lo que sabes del trabajo (contexto interno)

- El archivo llegó en **RGB**, no en CMYK.
- El azul del diseño era un RGB muy saturado (cercano a #1B3CFF).
- Se imprimió en **offset CMYK** sobre couché mate, sin prueba de color física previa (el
  cliente la omitió para ganar tiempo).

## C) Prompt del ejercicio

```
Eres del equipo de Castro & MacDonald. Redacta una respuesta al reclamo de abajo: explica con
claridad y sin tecnicismos por qué el color cambió y propón cómo resolverlo. Tono profesional y
resolutivo.
[pega el correo A + el contexto B]
```

---

## D) Notas técnicas para VERIFICAR la respuesta (referencia del facilitador)

La explicación del modelo debería ser coherente con esto:

- **RGB vs CMYK.** Las pantallas usan RGB (luz); la impresión usa CMYK (tinta). El espacio CMYK
  es **más pequeño**: hay colores RGB —sobre todo azules y verdes muy saturados— que
  **no existen** en CMYK y se reemplazan por el más cercano, que se ve más apagado.
- **Gamut.** A ese conjunto de colores reproducibles se le llama *gamut*. El azul eléctrico del
  archivo está **fuera del gamut CMYK**: por eso vira a un azul más opaco/verdoso.
- **Papel.** El couché **mate** absorbe y refleja distinto que el brillante; tiende a verse
  menos saturado que una pantalla retroiluminada.
- **Prueba de color.** Una prueba física previa habría anticipado el cambio. Es el control que
  evita esta sorpresa.
- **Solución realista.** No se puede "igualar la pantalla", pero sí buscar el azul CMYK más
  cercano aceptable (o un Pantone si el presupuesto lo permite), hacer una prueba y reimprimir.

**Errores típicos a cazar en la respuesta del modelo:** decir que "se puede reproducir
exactamente el color de pantalla", confundir RGB con CMYK, prometer una corrección imposible,
o inventar un perfil/estándar que no aplica. 

**Pregunta en neutro (paso 2 del ejercicio):**
*"Encuentra los errores técnicos o las promesas imposibles de esta explicación sobre color."*
— en vez de *"¿está bien esta respuesta?"*.
