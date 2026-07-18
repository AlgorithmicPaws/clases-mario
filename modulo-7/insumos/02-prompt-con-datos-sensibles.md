# Insumo — Un prompt que no debería enviarse así

> **Uso:** Ejercicio 4. Identifica todo lo que no debería salir de la empresa, reescribe el prompt
> anonimizado, y comprueba si la respuesta pierde calidad al quitar los datos personales.
>
> *(Datos ficticios, creados para el ejercicio.)*

---

## El prompt tal como lo escribió un compañero

> Necesito que me ayudes a decidir a qué clientes subirles el precio y a cuáles no. Te paso la
> cartera de Imprenta Castro & MacDonald con los datos de este año:
>
> 1. **Andes Verde S.A.** — NIT 900.417.882-3 — contacto: Lucía Fernández, lucia.fernandez@andesverde.com,
>    +57 310 447 2210. Facturación anual: $84.500. Margen medio: 19%. Paga a 45 días, casi siempre
>    tarde. Firmamos NDA en marzo.
> 2. **Editorial Cumbre** — NIT 901.220.145-7 — contacto: Marco Ruiz, m.ruiz@edcumbre.co,
>    +57 315 882 0043. Facturación anual: $132.000. Margen medio: 27%. Excelente pagador.
> 3. **Café del Valle** — NIT 900.885.331-2 — contacto: Ana Ospina, ana@cafedelvalle.com.
>    Facturación anual: $41.200. Margen medio: 31%.
>
> Datos internos: nuestro costo de papel subió 14% este semestre. La nómina del área comercial es
> de $18.400 mensuales (Ana Torres $3.200, Julián Pérez $2.800, resto del equipo el resardo).
> El acceso al ERP es usuario `admin_castro` / clave `Impr2026$`.
>
> También te cuento que Marco Ruiz nos comentó en confianza que Editorial Cumbre está negociando
> la compra de una imprenta pequeña y que podrían dejar de ser clientes en 2027.
>
> ¿A quién le subo precios y cuánto?

---

## Preguntas para el ejercicio

1. **Haz una lista** de todo lo que no debería haberse enviado. Clasifícalo:
   - Credenciales y secretos
   - Datos personales de terceros
   - Información sujeta a confidencialidad
   - Información interna sensible
2. **Reescribe el prompt** anonimizado, conservando **solo** lo que el modelo necesita para dar un
   buen consejo (¿de verdad necesita nombres, NIT y teléfonos para recomendar una política de
   precios?).
3. **Pruébalo:** envía tu versión limpia y compara. ¿La recomendación empeoró?
4. Aplica la **regla de la pantalla compartida** al prompt original: ¿lo habrías enviado si
   supieras que iba a proyectarse en una reunión con esos clientes delante?

> **Pista para el punto 3:** en la mayoría de los casos, sustituir por "Cliente A / B / C" y
> mantener facturación, margen y comportamiento de pago produce **exactamente el mismo análisis**.
> Ese es el argumento más convincente a favor de la minimización de datos: no cuesta calidad.

> **Nota sobre la credencial:** si algo así se envía por error, la clave debe considerarse
> **comprometida y rotarse de inmediato**. Borrar la conversación después no basta.
