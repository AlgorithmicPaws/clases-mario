# Insumo 2 — Tarifas, costos y márgenes

> **Uso:** Ejercicio 3 (verificar, no solo confiar). Pega este bloque y pide primero el total
> "en el chat", luego con **ejecución de código**. Compara si la aritmética cuadra.

---

## Datos del pedido (Andes Verde)

- Tirada: **5.000 ejemplares**
- Formato: A5, **32 páginas interiores** + portada (4 caras)
- IVA aplicable: **19 %**
- Margen mínimo de política: **22 % sobre el costo total**

## Costos base (por ejemplar, ejemplo)

| Concepto | Opción A · Couché reciclado FSC | Opción B · Offset ecológico FSC |
|----------|--------------------------------:|--------------------------------:|
| Papel interiores (32 págs.) | $0,86 | $1,12 |
| Papel + laminado portada | $0,24 | $0,31 |
| Impresión y tinta | $0,58 | $0,58 |
| Encuadernado (grapa) | $0,14 | $0,14 |
| **Costo unitario** | **$1,82** | **$2,15** |

## Costos fijos del trabajo (una vez, no por ejemplar)

- Preparación de planchas y arranque de máquina: **$320**
- Control de calidad y embalaje: **$140**

---

## Lo que hay que calcular (y verificar)

1. **Costo total** de cada opción = (costo unitario × 5.000) + costos fijos.
2. **Precio con margen** = costo total × (1 + 0,22).
3. **Precio final con IVA** = precio con margen × (1 + 0,19).
4. Precio **por ejemplar** al cliente, en cada opción.

> **Trampa a propósito:** es fácil equivocarse aplicando el IVA sobre el costo en vez de sobre el
> precio con margen, u olvidar los costos fijos. Ese es justo el tipo de error que la *ejecución
> de código* evita y la aritmética "a ojo" del modelo puede colar. Aplica la **prueba de la
> defensa**: ¿sabrías explicar cada cifra al cliente?
