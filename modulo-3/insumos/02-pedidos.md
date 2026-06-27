# Lote de pedidos entrantes — bandeja de pedidos@castromacdonald.com

> Correos reales de pedidos llegados esta semana. Sirven para dos cosas:
> **(a) clasificar** por urgencia y tipo, y **(b) calcular** el costo de cada uno contra el
> tarifario (`01-tarifas.md`). Datos de ejemplo.

---

**Pedido #1041 — Corporación Andes Verde**
De: maria.soto@andesverde.org
Necesitamos **2 000 trípticos institucionales** en couché mate 150 g/m² (A4), con barniz
mate de máquina. Es para el congreso del mes que viene, tenemos tiempo. ¿Nos pasan
cotización con IVA?

---

**Pedido #1042 — Andes Verde / Dirección de Comunicaciones**
De: jorge.lillo@andesverde.org
URGENTE: se nos acabaron las **tarjetas de presentación** y el director viaja el viernes.
Necesitamos **300 tarjetas** (cartulina mate 300 g/m², 90×50 mm) con canto teñido Verde
Andes. ¿Llegan para el jueves?

---

**Pedido #1043 — Librería Pággina**
De: compras@paggina.cl
Hola, quería consultar si imprimen **separadores de libros**. Serían unos **5 000**, en
cartulina 250 g/m² con plastificado mate por ambas caras y troquelado. Sin apuro, es para
la feria de noviembre.

---

**Pedido #1044 — Andes Verde**
De: maria.soto@andesverde.org
Reenvío adjunto el arte del **folleto institucional** (100 unidades, couché mate 170 g/m²
interiores + portada 250 g/m², con barniz mate). Ojo: la última vez nos llegó en brillante
por error y hubo que reimprimir. Por favor confirmen el sustrato antes de entrar a máquina.

---

**Pedido #1045 — sin identificar**
De: info@eventosdelsur.com
Buenas, ¿cuánto saldría algo tipo flyer para un evento? No sé bien la cantidad todavía ni
el papel, lo estamos viendo. Avísenme rangos de precio así decidimos.

---

**Pedido #1046 — Andes Verde / Logística**
De: bodega@andesverde.org
Reposición de stock interno: **10 000 hojas de carta** bond 90 g/m² Carta, impresión a dos
tintas. Es stock, no corre prisa, pero necesitamos el presupuesto para la orden de compra
del trimestre.

---

**Pedido #1047 — Fundación Raíces (cliente nuevo)**
De: contacto@fundacionraices.org
URGENTE — tenemos una auditoría el lunes y nos pidieron **500 carpetas institucionales**
con plastificado mate. ¿Hay alguna forma de tenerlas para el viernes aunque sea pagando
recargo? Es crítico para nosotros.

---

> **Para los ejercicios:**
> - *Clasificación (few-shot):* etiqueta cada pedido por **urgencia** (ALTA / MEDIA / BAJA) y
>   por **tipo de pieza**. Pista: hay señales de tiempo y de bloqueo en el texto.
> - *Cálculo (ejecución de código):* toma los pedidos con datos completos (#1041, #1042, #1044,
>   #1046) y calcula el costo total con IVA usando `01-tarifas.md`. Compara el resultado del
>   modelo "a ojo" contra el de la ejecución de código.
> - *Datos incompletos:* #1045 no tiene cantidad ni papel; #1047 es cliente nuevo con plazo
>   crítico. ¿Qué falta para cotizar? ¿Qué NO deberías prometer sin verificar?
