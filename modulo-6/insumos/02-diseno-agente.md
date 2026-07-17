# Insumo — Plantilla para diseñar un agente (sobre papel)

> **Uso:** Ejercicios 2, 3 y 5. Toma un proceso "candidato a agente" del insumo 1 y rellena esta
> plantilla. No se ejecuta nada: es un ejercicio de **diseño y criterio**.

---

## Diseño del agente: [nombre del agente]

### 1. Las cuatro piezas

**Objetivo** (como un mini-specdoc, M4: claro y acotado)
> _(Ej.: "Preparar un borrador de cotización para cada pedido sin confirmar del correo de hoy,
> dejarlos listos para que yo los revise. No enviar nada.")_

**Herramientas** (solo las necesarias — marca L = leer / A = actuar)
- [ ] …  (L / A)
- [ ] …  (L / A)
- [ ] …  (L / A)

**Memoria** (qué necesita recordar mientras trabaja)
> _(Ej.: qué pedidos ya procesó, qué tarifa aplicó a cada uno.)_

**Criterios de parada** (cuándo se detiene)
- Objetivo cumplido: …
- Punto que requiere humano: …
- Si se topa con un muro: … _(debe pedir ayuda, no inventar)_
- Límite: … _(máx. pasos / tiempo)_

---

### 2. El dial de autonomía (Ejercicio 3)

| Paso del agente | ¿Solo o pide confirmación? | Por qué (reversible / irreversible) |
|-----------------|----------------------------|-------------------------------------|
| … | | |
| … | | |
| … | | |

> **Regla del dial:** reversible y de bajo riesgo → más autonomía. Irreversible o costoso →
> checkpoint humano. ¿Dónde está la acción irreversible?

---

### 3. Análisis de riesgo (Ejercicio 5)

- **¿Dónde se compondría un error** si nadie revisa un paso intermedio?
  > …
- **Mayor riesgo de seguridad:** ¿lee fuentes no confiables? ¿puede enviar/borrar? ¿mínimo
  privilegio respetado?
  > …
- **Prueba de la defensa (versión agente):** si actúa solo y se equivoca, ¿puedo detectarlo y
  arreglarlo a tiempo, y responder por ello?
  > Sí / No — por qué:
- **Veredicto:** ¿subo su autonomía o no todavía?
  > …
