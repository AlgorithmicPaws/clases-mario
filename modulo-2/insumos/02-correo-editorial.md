# Insumo 2 — Correo de la editorial + cotización original

**Ejercicio:** "Responder a una editorial que pide bajar costos" (Tema 2 · Prompt engineering).

Tienes el correo entrante de un cliente y la cotización que le enviaste. El ejercicio compara
un **prompt vago** ("redacta una respuesta") con un **prompt dirigido** (rol + el "por qué" +
3 alternativas concretas + formato).

---

## A) Correo entrante del cliente

> **De:** Paula Errázuriz — Editorial Hoja de Roble
> **Asunto:** RE: Cotización "Cuentos del Sur" — necesitamos ajustar
>
> Hola, equipo de Castro & MacDonald:
>
> Gracias por la cotización. El problema es que se nos va bastante por encima del presupuesto:
> teníamos contemplado cerca de **$4.500.000** para esta primera edición y la cotización quedó
> en **$6.180.000**. Nos encanta trabajar con ustedes y no queremos cambiar de imprenta, pero
> necesitamos llegar a una cifra más cercana a lo que tenemos.
>
> ¿Hay forma de ajustar sin que el libro pierda calidad? Es un libro infantil ilustrado, así
> que el color y el papel importan. Quedo atenta a lo que puedan proponer.
>
> Saludos, Paula.

## B) Cotización original (resumen)

| Concepto | Detalle |
|----------|---------|
| Título | "Cuentos del Sur" (infantil ilustrado) |
| Tiraje | 2.000 ejemplares |
| Formato | 21 × 21 cm |
| Páginas | 48 páginas interiores, full color |
| Papel interior | Couché brillante 150 g/m² |
| Tapa | Cartulina 300 g/m², tapa dura, plastificado brillante |
| Encuadernación | Cosido y encolado |
| **Total cotizado** | **$6.180.000** (≈ $3.090 por ejemplar) |
| Presupuesto del cliente | ~$4.500.000 |

## C) Palancas reales para bajar el costo (datos para que tú o el modelo propongan)

- Bajar tiraje de 2.000 → 1.500 ejemplares reduce el total de forma proporcional al papel y
  la impresión, aunque sube el costo por unidad.
- Couché brillante 150 g → couché mate 130 g: ahorro de papel sin perder calidad de color.
- Tapa dura → tapa blanda con solapas: ahorro relevante en encuadernación y materiales.
- Plastificado brillante → mate: costo similar, decisión estética.
- Mantener full color en interiores (no se toca: es un infantil ilustrado).

---

## Prompts del ejercicio

**Intento 1 (vago):**
```
Redacta una respuesta a este cliente.
[pega el correo A]
```

**Intento 2 (dirigido):**
```
Eres asesor comercial de la imprenta Castro & MacDonald. Tu objetivo es CONSERVAR a esta
clienta (editorial pequeña, relación de largo plazo), no solo cerrar esta venta.

Con el correo y la cotización de abajo, redacta una respuesta que:
- Reconozca su restricción de presupuesto con cercanía, sin sonar a vendedor.
- Proponga 3 alternativas CONCRETAS para acercarse a $4.500.000, indicando qué se gana y qué
  se cede en cada una (calidad, durabilidad, percepción).
- Deje claro que el color full se mantiene (es un infantil ilustrado).
- Cierre invitando a una llamada corta para decidir.

Formato: correo cálido y profesional, máximo 180 palabras, sin tecnicismos innecesarios.

<correo>{pega el correo A}</correo>
<cotizacion>{pega la tabla B}</cotizacion>
```

**Qué comparar:** el intento 2 debería salir casi listo para enviar, con alternativas
accionables; el intento 1, genérico y sin números.
