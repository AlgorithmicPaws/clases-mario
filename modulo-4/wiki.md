# Módulo 4 — Metodologías de desarrollo con IA
### Fundamentos de IA Productiva

---

## Tabla de Contenidos

1. [De usar la IA a construir con ella](#1-de-usar-la-ia-a-construir-con-ella)
   - 1.1 [El salto: de la respuesta al entregable](#11-el-salto-de-la-respuesta-al-entregable)
   - 1.2 [Qué es una "metodología" y por qué la necesitas](#12-qué-es-una-metodología-y-por-qué-la-necesitas)
2. [Specdocs: pensar antes de pedir](#2-specdocs-pensar-antes-de-pedir)
   - 2.1 [Qué es un specdoc](#21-qué-es-un-specdoc)
   - 2.2 [Cuándo escribir uno (y cuándo no)](#22-cuándo-escribir-uno-y-cuándo-no)
   - 2.3 [Cómo estructurarlo: las siete piezas](#23-cómo-estructurarlo-las-siete-piezas)
   - 2.4 [Plantilla y ejemplo](#24-plantilla-y-ejemplo)
3. [El flujo iterativo: draft → revisión → refinamiento](#3-el-flujo-iterativo-draft--revisión--refinamiento)
   - 3.1 [Por qué el primer intento no es el entregable](#31-por-qué-el-primer-intento-no-es-el-entregable)
   - 3.2 [El ciclo, paso a paso](#32-el-ciclo-paso-a-paso)
   - 3.3 [Dirigir y verificar: tu trabajo real](#33-dirigir-y-verificar-tu-trabajo-real)
   - 3.4 [Cuándo dejar de iterar](#34-cuándo-dejar-de-iterar)
4. [Proyectos largos: coherencia entre sesiones](#4-proyectos-largos-coherencia-entre-sesiones)
   - 4.1 [El problema del colaborador amnésico](#41-el-problema-del-colaborador-amnésico)
   - 4.2 [El documento de estado](#42-el-documento-de-estado)
   - 4.3 [El handoff: cerrar y abrir sesión](#43-el-handoff-cerrar-y-abrir-sesión)
   - 4.4 [Trocear el trabajo en hitos](#44-trocear-el-trabajo-en-hitos)
5. [Memoria y contexto persistente](#5-memoria-y-contexto-persistente)
   - 5.1 [Las tres capas de memoria](#51-las-tres-capas-de-memoria)
   - 5.2 [Qué persistir y qué no](#52-qué-persistir-y-qué-no)
   - 5.3 [El riesgo de la memoria desactualizada](#53-el-riesgo-de-la-memoria-desactualizada)
6. [Cuándo la IA acelera y cuándo mete deuda](#6-cuándo-la-ia-acelera-y-cuándo-mete-deuda)
   - 6.1 [Deuda técnica y deuda conceptual](#61-deuda-técnica-y-deuda-conceptual)
   - 6.2 [Señales de alarma](#62-señales-de-alarma)
   - 6.3 [La regla del "lo entiendo lo suficiente para defenderlo"](#63-la-regla-del-lo-entiendo-lo-suficiente-para-defenderlo)
7. [Glosario del Módulo](#7-glosario-del-módulo)
8. [Práctica guiada (segunda hora)](#8-práctica-guiada-segunda-hora)
9. [Preguntas de repaso](#9-preguntas-de-repaso)
10. [Recursos extra](#10-recursos-extra)

---

## 1. De usar la IA a construir con ella

Los tres primeros módulos fueron subiendo por una escalera. El **Módulo 1** explicó *cómo
piensa* el modelo; el **Módulo 2**, *cómo hablarle*; el **Módulo 3**, *qué producto lo
envuelve* (proyectos, herramientas, connectors). Todo eso comparte algo: eran técnicas para
**una petición**. Escribes un buen prompt, obtienes una buena respuesta, y listo.

Este módulo cambia la unidad de trabajo. Ya no es "una respuesta": es un **entregable que se
construye a lo largo del tiempo** —una propuesta comercial, un manual, un flujo de trabajo, un
informe de varias semanas—. Y cuando el trabajo dura más que un mensaje, el prompt deja de ser
suficiente: hace falta un **método**.

> **La idea que atraviesa todo el módulo:** un prompt bueno resuelve una tarea; una
> **metodología** buena resuelve un proyecto. La diferencia entre quien "le pide cosas a la IA"
> y quien la usa para producir trabajo serio no está en saber prompts más ingeniosos, sino en
> tener un **proceso repetible** para especificar, iterar, mantener coherencia y saber cuándo
> desconfiar.

---

### 1.1 El salto: de la respuesta al entregable

Piensa en la diferencia entre pedirle a alguien *"dime la capital de Francia"* y encargarle
*"prepárame la propuesta para el cliente Andes Verde"*. La primera es una consulta: hay una
respuesta y se acabó. La segunda es un **proyecto**: tiene requisitos, restricciones,
revisiones, cambios de opinión a mitad de camino y un criterio de "esto ya está listo".

Con la IA pasa igual. Para la consulta, un buen prompt basta. Para el proyecto necesitas
gestionar cuatro cosas que un solo mensaje no cubre:

- **Especificación** — qué es exactamente lo que quieres (antes de pedirlo).
- **Iteración** — cómo pasas de un borrador tosco a algo pulido.
- **Continuidad** — cómo mantienes la coherencia cuando el trabajo cruza varias sesiones.
- **Criterio** — cómo distingues cuándo la IA te está ayudando de cuándo te está metiendo
  problemas que pagarás después.

Esas cuatro cosas son, exactamente, las cuatro secciones de este módulo.

---

### 1.2 Qué es una "metodología" y por qué la necesitas

Una **metodología** de trabajo con IA no es nada esotérico: es un **conjunto de hábitos
repetibles** que hacen que el resultado no dependa de la suerte de un buen prompt. Es la
diferencia entre cocinar "a ojo" cada vez y tener una receta: la receta no te quita
creatividad, te quita la varianza.

Sin método, el trabajo con IA en proyectos largos tiende a degradarse de formas predecibles:

| Sin metodología | Con metodología |
|-----------------|-----------------|
| Pides sin haber pensado qué quieres; corriges diez veces | Escribes un **specdoc** breve y el primer borrador ya apunta bien |
| Aceptas el primer resultado o lo rehaces desde cero | **Iteras** sobre el borrador con ajustes concretos |
| Cada sesión nueva empieza de cero y se contradice con la anterior | Un **documento de estado** mantiene la coherencia |
| Aceptas lo que suena bien sin entenderlo | Reconoces cuándo la IA **acelera** y cuándo mete **deuda** |

> **Por qué importa ahora y no antes.** En el Módulo 2 vimos el ciclo *borrador → revisión →
> refinamiento* como una técnica de prompting. Aquí lo elevamos a **columna vertebral de un
> proyecto**. La técnica era para un texto; la metodología es para un entregable que vive
> semanas y cruza muchas conversaciones.

---

## 2. Specdocs: pensar antes de pedir

### 2.1 Qué es un specdoc

Un **specdoc** (documento de especificación, de *specification document*) es un texto **breve**
que describe *qué* quieres construir **antes** de pedirle a la IA que lo construya. No es un
contrato legal ni un documento técnico de cincuenta páginas: en su forma más útil cabe en media
página. Su propósito es sencillo pero poderoso: **obligarte a ti a pensar** qué quieres, y darle
al modelo un **blanco claro** al que apuntar.

Es la evolución natural de dos ideas que ya conoces. En el **Módulo 2** aprendiste que un prompt
claro —con rol, contexto, restricciones y formato— rinde mucho más que uno vago. El specdoc es
eso mismo, pero **escrito una vez, guardado, y reutilizado** a lo largo de todo un proyecto en
lugar de reconstruirlo en cada mensaje. Y en el **Módulo 3**, las *instrucciones del proyecto*
hacían algo parecido a nivel de comportamiento; el specdoc lo hace a nivel de **entregable
concreto**.

> **La analogía del plano.** Nadie construye una casa poniendo ladrillos y viendo qué sale.
> Primero hay un plano: cuántas habitaciones, para qué se usan, qué presupuesto, qué **no** va a
> tener. El specdoc es el plano de tu entregable. Cuesta veinte minutos y te ahorra tres horas
> de "no, así no era".

---

### 2.2 Cuándo escribir uno (y cuándo no)

El specdoc es una herramienta, no un ritual obligatorio. Aplicar el criterio de "cuándo NO" es
tan importante como saber usarlo.

**Escribe un specdoc cuando:**

- El entregable es **grande o de varios pasos** (una propuesta, un informe, un plan, una campaña).
- Vas a **iterar mucho** sobre él, o lo retomarás en varias sesiones.
- Hay **restricciones que no se pueden violar** (presupuesto, tono de marca, plazos, formato legal).
- Otra persona tiene que **entender o aprobar** lo que pediste.
- Ya has intentado pedirlo "a lo bruto" y el resultado se va por las ramas.

**NO escribas un specdoc para:**

- Una consulta puntual ("resúmeme este correo", "¿cómo se dice X en inglés?").
- Algo que harás una sola vez y desecharás.
- Tareas donde el propio prompt del Módulo 2 ya es suficientemente claro.

> **La trampa de la sobre-especificación.** Escribir un specdoc de tres páginas para redactar un
> correo es el error inverso: gastas más en el plano que en la casa. Regla práctica: si el
> specdoc te toma **más tiempo que hacer un primer intento y corregirlo**, no lo necesitabas.

---

### 2.3 Cómo estructurarlo: las siete piezas

Un specdoc útil casi siempre contiene estas piezas. No todas hacen falta siempre, pero cada una
que omites es una decisión que el modelo tomará por ti (y puede que no como querías).

| Pieza | Pregunta que responde | Ejemplo (imprenta) |
|-------|----------------------|--------------------|
| **1. Objetivo** | ¿Qué quiero conseguir, en una frase? | "Una propuesta de impresión para Andes Verde que gane el pedido sin sacrificar margen." |
| **2. Contexto** | ¿Qué información de fondo hace falta? | Cliente nuevo, sector orgánico, pidió catálogo de 32 págs., 5.000 unidades. |
| **3. Restricciones** | ¿Qué NO se puede violar? | Margen mínimo 22%, papel certificado FSC, entrega en 15 días hábiles. |
| **4. Criterios de aceptación** | ¿Cómo sé que está "listo"? | Precio desglosado, 2 opciones de papel, tono cercano pero profesional, 1 página. |
| **5. No-objetivos** | ¿Qué deliberadamente NO quiero? | No incluir servicios de diseño; no prometer plazos sin confirmar planta. |
| **6. Formato de salida** | ¿En qué forma lo quiero? | Documento de 1 página, encabezados claros, tabla de precios al final. |
| **7. Ejemplos / referencias** | ¿Hay un modelo a imitar? | La propuesta ganadora de "Café del Valle" (adjunta) como referencia de tono. |

De todas, dos son las que más gente olvida y más valen:

- **Criterios de aceptación.** Sin ellos, "listo" es una opinión. Con ellos, es una lista que
  puedes verificar (enlaza con la evaluación de respuestas del Módulo 2: *no basta con que suene
  bien*).
- **No-objetivos.** Decir qué *no* quieres evita que el modelo "ayude de más" añadiendo cosas
  que tendrás que borrar. Delimitar es la mitad de especificar.

> **El specdoc es un documento vivo.** No lo escribes perfecto de una vez. Empiezas con lo que
> sabes, y a medida que iteras (sección 3) descubres restricciones que no habías visto y las
> añades. Un specdoc que se actualiza es señal de un proyecto que se entiende cada vez mejor.

---

### 2.4 Plantilla y ejemplo

Una plantilla mínima que puedes copiar y pegar al inicio de cualquier proyecto:

```
# Specdoc — [nombre del entregable]

Objetivo:        [una frase: qué quiero conseguir]
Contexto:        [3-5 líneas de información de fondo relevante]
Restricciones:   [lo que NO se puede violar; una por línea]
Criterios de
aceptación:      [cómo sabré que está listo; lista verificable]
No-objetivos:    [lo que deliberadamente dejo fuera]
Formato:         [longitud, estructura, tono]
Referencias:     [ejemplos o modelos a imitar, si los hay]
```

La forma de usarlo con el modelo es directa: **pega el specdoc primero y la petición después**
(el patrón *contexto arriba, instrucción abajo* del Módulo 2). O, mejor aún en un flujo largo,
guárdalo en el **knowledge del Proyecto** (Módulo 3) para que todas las conversaciones lo vean
sin volver a pegarlo.

> **Un truco que funciona muy bien:** antes de construir nada, pídele al modelo que **te ayude a
> escribir el specdoc**. "Voy a preparar una propuesta para este cliente; hazme cinco preguntas
> que debería responder antes de empezar." El modelo es excelente sacando a la luz las
> restricciones que tú das por obvias — y así el plano queda mejor.

---

## 3. El flujo iterativo: draft → revisión → refinamiento

### 3.1 Por qué el primer intento no es el entregable

Hay una tentación muy humana con la IA: como responde rápido y suena seguro, uno espera que
**acierte a la primera**. Y cuando no lo hace del todo, la reacción típica es rehacer el prompt
entero desde cero, una y otra vez, buscando el "prompt mágico" que lo clave de un tiro.

Ese enfoque es un error de método. El primer resultado del modelo **no es el entregable: es el
primer borrador**. Y un borrador no se tira, se **refina**. Igual que un buen escritor no espera
que su primer párrafo sea el definitivo, tú no deberías esperar que la primera respuesta lo sea.

> **Enlace con el Módulo 1.** El modelo genera *la continuación más probable*, no *la respuesta
> perfecta para tu caso concreto*, que él no puede conocer del todo. La iteración es cómo cierras
> esa brecha: cada ronda le das información que no tenía, y el resultado converge hacia lo que
> quieres.

---

### 3.2 El ciclo, paso a paso

El flujo iterativo es un bucle de tres movimientos que repites hasta que el entregable cumple tus
criterios de aceptación:

```
   ┌──────────────────────────────────────────────────────────┐
   │                                                          │
   ▼                                                          │
DRAFT  ──────────►  REVISIÓN  ──────────►  REFINAMIENTO  ─────┘
(genera un        (tú lees y juzgas      (pides ajustes
 borrador con     contra los            concretos; el
 el specdoc)      criterios)            borrador mejora)

        … hasta que cumple los criterios de aceptación.
```

- **Draft (borrador).** Le das el specdoc y pides un primer intento. No busques perfección:
  buscas **algo concreto sobre lo que reaccionar**. Un Artifact (Módulo 3) es el lugar ideal para
  que ese borrador viva y se reescriba.
- **Revisión.** Aquí trabajas **tú**. Lees el borrador con los criterios de aceptación al lado y
  anotas qué falla: "el segundo párrafo es genérico", "el precio no cuadra", "el tono es
  demasiado frío". Es el mismo ojo crítico de la *evaluación de respuestas* del Módulo 2.
- **Refinamiento.** Devuelves observaciones **concretas y accionables**, no un "no me gusta,
  hazlo otra vez". Cuanto más específico el feedback, mejor la siguiente versión.

**La diferencia entre feedback vago y feedback útil:**

| Vago (poco rinde) | Concreto (rinde mucho) |
|-------------------|------------------------|
| "Hazlo mejor" | "El párrafo de apertura no menciona el sector orgánico del cliente; añádelo" |
| "Muy largo" | "Recórtalo a una página; quita la sección de historia de la empresa" |
| "No me convence el precio" | "El total no incluye el IVA; recalcúlalo con IVA desglosado" |
| "Más formal" | "Cambia el tuteo por trato de usted y quita las exclamaciones" |

---

### 3.3 Dirigir y verificar: tu trabajo real

En el flujo iterativo tu papel no es *ejecutar* —eso lo hace el modelo— sino **dirigir y
verificar**. Es el principio que viene del Módulo 2 y que aquí se vuelve el eje de todo el
trabajo:

- **Dirigir** = decidir qué se hace, marcar el rumbo, dar el feedback concreto que mueve el
  borrador hacia el objetivo. Tú tienes el criterio y el contexto que el modelo no tiene.
- **Verificar** = comprobar que cada versión de verdad cumple, sobre todo donde el modelo es
  débil: números que deben cuadrar (usa ejecución de código, Módulo 3), datos que deben ser
  ciertos (pide citas, Módulo 1), afirmaciones que suenan bien pero podrían ser inventadas.

> **La trampa de la fluidez.** El modelo escribe con tanta soltura que da pereza revisar; todo
> "suena profesional". Pero *sonar bien* y *estar bien* no son lo mismo (Módulo 2). El coste de
> saltarte la verificación no lo pagas ahora: lo paga tu cliente cuando el precio estaba mal, o
> tú cuando alguien detecta el dato inventado. Dirigir es agradable; verificar es el trabajo.

---

### 3.4 Cuándo dejar de iterar

Iterar tiene rendimientos decrecientes. Las primeras rondas mejoran mucho; a partir de cierto
punto, cada ronda cambia cosas sin mejorarlas —o incluso las empeora, porque el modelo
"sobre-corrige".

Señales de que es hora de parar:

- El borrador **cumple los criterios de aceptación** del specdoc. (Por eso los escribiste: son tu
  línea de meta objetiva, no una sensación.)
- Los cambios que pides ya son **cosméticos** y podrías hacerlos tú más rápido a mano.
- Notas que estás **dando vueltas**: pides A, luego B, y en la siguiente ronda vuelve algo
  parecido a A. Señal de que el criterio no está claro, no de que falte otra ronda.

> **Regla práctica:** cuando dudes entre "otra ronda con el modelo" y "lo remato yo en dos
> minutos", remátalo tú. La iteración es para saltos de calidad, no para pulir comas.

---

## 4. Proyectos largos: coherencia entre sesiones

### 4.1 El problema del colaborador amnésico

Aquí choca de frente uno de los límites que ya conoces. En el **Módulo 2** vimos que la **ventana
de contexto** es finita y que cada chat es una **ventana aislada**: no comparte nada con otros
chats, y lo que sale de la ventana, se olvida. En un proyecto de una tarde eso no importa. En uno
de tres semanas, sí: cada sesión nueva, el modelo es un **colaborador brillante pero amnésico**
que no recuerda nada de lo que decidieron ayer.

Los síntomas son reconocibles:

- La sesión de hoy **se contradice** con una decisión de la semana pasada.
- Vuelves a explicar el mismo contexto una y otra vez (gastando ventana y tu tiempo).
- El modelo "reabre" debates que ya habían cerrado, porque no sabe que se cerraron.
- Pierdes el hilo de **por qué** se tomó una decisión, y la repites o la deshaces sin querer.

La solución no es que el modelo "recuerde por arte de magia" —no puede—. La solución es
**metodológica**: crear artefactos que *transporten la memoria* de una sesión a la siguiente.

---

### 4.2 El documento de estado

La herramienta central para proyectos largos es un **documento de estado** (a veces llamado
*documento vivo*, *bitácora* o *state doc*): un único archivo que resume, en todo momento, **dónde
está el proyecto**. No es el entregable en sí; es el mapa del proyecto.

Un buen documento de estado suele tener:

| Sección | Qué contiene | Por qué |
|---------|-------------|---------|
| **Objetivo** | El specdoc resumido: qué construimos | Ancla cada sesión al mismo norte |
| **Decisiones tomadas** | Qué se decidió y **por qué** | Evita reabrir debates cerrados |
| **Estado actual** | Qué está hecho y qué falta | Permite retomar sin releer todo |
| **Pendientes / próximos pasos** | La lista de lo siguiente | Arranca la próxima sesión en marcha |
| **Cuestiones abiertas** | Dudas sin resolver | No se pierden entre sesiones |

> **La analogía del cuaderno de bitácora.** Un barco que cruza el océano no confía la ruta a la
> memoria del capitán: la anota en la bitácora. Cada turno de guardia lee dónde está el barco y
> qué se decidió, y escribe lo suyo. El documento de estado es tu bitácora: cualquier sesión
> (o cualquier persona del equipo) puede retomar el rumbo leyéndolo.

En la práctica: guardas el documento de estado en el **knowledge del Proyecto** (Módulo 3), y al
empezar cada sesión el modelo lo tiene disponible. Al terminar, le pides que **te ayude a
actualizarlo** con lo que se decidió hoy.

---

### 4.3 El handoff: cerrar y abrir sesión

El *handoff* (traspaso) es el ritual de dos minutos que sostiene la continuidad. Se hace al
cerrar una sesión y al abrir la siguiente.

**Al cerrar una sesión**, antes de irte, pídele al modelo un resumen de traspaso:

```
"Antes de terminar: resume en 8-10 líneas qué decidimos hoy, qué quedó
 a medias y cuáles son los tres próximos pasos. Voy a guardarlo para
 retomar mañana."
```

Ese resumen lo pegas en el documento de estado. Es la **memoria comprimida** de la sesión.

**Al abrir la siguiente sesión**, no empieces en frío. Dale el contexto de arranque:

```
"Retomamos el proyecto Andes Verde. Aquí está el documento de estado
 [pegado o en el knowledge]. Confírmame dónde nos quedamos y empecemos
 por el primer pendiente."
```

> **Por qué el resumen lo escribe el modelo y no tú.** El modelo acaba de tener todo el contexto
> de la sesión en su ventana: es el momento en que mejor puede comprimirlo. Tú, en cambio, lo
> habrás olvidado a medias mañana. Aprovechar ese resumen "en caliente" es una de las técnicas
> más rentables de todo el módulo.

---

### 4.4 Trocear el trabajo en hitos

Un proyecto grande no se ataca de una sola vez, ni con la IA ni sin ella. La misma lógica del
Módulo 2 —*dividir una tarea compleja en varios prompts*— se aplica a nivel de proyecto:
divídelo en **hitos** manejables, cada uno con su propio mini-ciclo de especificar → iterar →
verificar.

Para la propuesta de Andes Verde, por ejemplo:

1. **Hito 1:** análisis del pedido y opciones de papel viables (con sus costos).
2. **Hito 2:** estructura de precios y margen.
3. **Hito 3:** redacción de la propuesta en el tono adecuado.
4. **Hito 4:** revisión final y formato de entrega.

Cada hito cabe cómodamente en una ventana de contexto, produce un resultado verificable, y
alimenta al siguiente. Trocear también **protege contra el *context rot*** (Módulo 2): en lugar
de una conversación kilométrica donde todo se mezcla y el modelo empieza a perder el hilo, tienes
sesiones enfocadas cuyo resultado se guarda en el documento de estado.

> **Regla de oro de los proyectos largos:** la información importante **no debe vivir solo en la
> ventana de contexto**, porque la ventana es volátil. Debe vivir en un **artefacto persistente**
> —el specdoc, el documento de estado, el knowledge del Proyecto— del que cualquier sesión pueda
> beber. La ventana es la mesa de trabajo; el documento de estado es el archivador.

---

## 5. Memoria y contexto persistente

### 5.1 Las tres capas de memoria

"Memoria" es una palabra que se usa para cosas distintas. Separarlas evita muchos malentendidos.
Hay **tres capas**, de la más volátil a la más permanente:

| Capa | Qué es | Cuánto dura | Ejemplo |
|------|--------|-------------|---------|
| **1. Ventana de contexto** | Lo que el modelo "ve" en la conversación actual | Solo esta sesión | El correo que acabas de pegar |
| **2. Memoria de proyecto** | Knowledge e instrucciones compartidos (Módulo 3) | Mientras exista el Proyecto | El manual de marca, el specdoc, el documento de estado |
| **3. Memoria personal** | Datos que la app recuerda de ti entre proyectos | Persistente, transversal | "Trabajo en una imprenta", "prefiero respuestas concisas" |

- La **capa 1** ya la dominas desde el Módulo 2: es potente pero **efímera y limitada**.
- La **capa 2** la viste en el Módulo 3: es el corazón de los proyectos largos (secciones
  anteriores).
- La **capa 3** es la que muchas interfaces han añadido: una memoria que la aplicación mantiene
  sobre tus preferencias y tu contexto para no repetirlos en cada conversación.

> **La distinción clave.** La capa 1 la controla el **prompt**; la capa 2, el **Proyecto**; la
> capa 3, la **configuración de la app**. Cuando algo "se le olvida" al modelo, la pregunta útil
> es: *¿en qué capa debería haber estado guardado?* Un dato de proyecto que pusiste solo en el
> chat (capa 1) se pierde; por eso va en el documento de estado (capa 2).

---

### 5.2 Qué persistir y qué no

Que puedas guardar algo en memoria persistente no significa que debas. El mismo criterio de
**curación** del Módulo 3 (*"un proyecto, un objetivo"; curar, no acumular*) aplica aquí:

**Vale la pena persistir:**

- Contexto **estable y reutilizable**: tu rol, tu sector, tus preferencias de formato.
- Decisiones y su **porqué** (documento de estado).
- Material de referencia que consultas una y otra vez (manual de marca, tarifas, plantillas).

**NO conviene persistir:**

- Datos **efímeros** de una sola tarea (el correo de hoy no tiene que quedar en la memoria del
  proyecto para siempre).
- Información **que caduca rápido** sin un plan para actualizarla (una tarifa que cambia cada mes).
- Datos **sensibles** que no quieres que queden almacenados (esto se trata a fondo en el Módulo 7).

> **Menos y mejor, otra vez.** Es el mismo principio que el *context rot* (Módulo 2) y el knowledge
> curado (Módulo 3), ahora aplicado a la memoria persistente. Una memoria pequeña y precisa rinde
> más que una enorme y desordenada, porque el modelo recupera mejor de lo curado y se confunde con
> lo acumulado.

---

### 5.3 El riesgo de la memoria desactualizada

Hay un peligro específico de la memoria persistente que conviene entender bien, porque es
**contraintuitivo**: un dato viejo guardado es **peor** que no tener el dato.

Si el modelo no sabe algo, en el mejor de los casos lo dice o lo busca. Pero si tiene guardado un
dato **desactualizado** —una tarifa vieja, una decisión que ya cambió, un requisito que dejó de
aplicar—, lo usará con **total confianza** y sin avisar. El contexto persistente **amplifica**:
guarda lo correcto y ahorras trabajo; guarda lo caduco y propagas el error por todo el proyecto.

- **Versiona y limpia.** Cuando una decisión cambie, actualiza el documento de estado y borra la
  vieja. No dejes dos versiones conviviendo: el modelo no sabe cuál es la buena.
- **Fecha lo perecedero.** "Tarifa vigente a junio 2026" le dice al modelo (y a ti) cuándo
  desconfiar.
- **Para datos críticos, pide la fuente.** Que algo esté en memoria no garantiza que sea actual;
  pídele que **cite de dónde sale** (técnica del Módulo 1 y 3 contra las alucinaciones).

> **El principio, elevado:** la memoria persistente es una fortaleza que se convierte en trampa si
> no la mantienes. Trátala como tratarías el archivador de la oficina: útil mientras esté al día,
> peligroso cuando alguien archiva algo caduco y otro lo saca años después creyéndolo vigente.

---

## 6. Cuándo la IA acelera y cuándo mete deuda

### 6.1 Deuda técnica y deuda conceptual

Toda esta metodología sirve para un objetivo final: **usar la IA donde de verdad acelera, sin
acumular problemas que pagarás más caro después**. A ese "pagar después" lo llamamos **deuda**, y
tiene dos formas.

**Deuda técnica** — un resultado que *funciona hoy* pero está construido de forma frágil, y
mantenerlo o extenderlo cuesta cada vez más. Ejemplos fuera del código: una propuesta generada tan
rápido que nadie revisó los números y el error se descubre en facturación; una plantilla que el
modelo montó "a su manera" y que nadie del equipo entiende cómo modificar; un proceso que depende
de un prompt gigante que solo funciona si nadie lo toca.

**Deuda conceptual** — la más peligrosa y la más silenciosa: **aceptar algo que no entiendes**.
El modelo te entrega una propuesta, un análisis o una recomendación, suena impecable, y la usas
sin comprender por qué dice lo que dice. Funciona… hasta que un cliente te hace una pregunta, o
las circunstancias cambian, y no sabes defenderla ni ajustarla porque nunca fue realmente tuya.

| | Deuda técnica | Deuda conceptual |
|---|--------------|------------------|
| Qué es | Trabajo frágil que cuesta mantener | Aceptar lo que no entiendes |
| Cuándo se paga | Al modificar o escalar | Cuando te preguntan "¿por qué?" |
| Síntoma | "Funciona, pero nadie lo toca" | "Lo hizo la IA, no sé bien cómo" |
| Antídoto | Verificar y simplificar | Entenderlo antes de usarlo |

> **El enlace con todo el curso.** La deuda conceptual es exactamente el riesgo contra el que
> vienen avisando los Módulos 1 y 2: el modelo produce texto *plausible*, no necesariamente
> *correcto ni comprendido*. La velocidad de la IA es real, pero **no delegues el entendimiento**.
> Ese es el tema que el Módulo 7 llevará hasta el final.

---

### 6.2 Señales de alarma

Aprende a reconocer los momentos en que la IA está pasando de acelerar a endeudar:

- **Estás copiando sin leer.** Si pegas un resultado en tu entregable sin haberlo entendido,
  estás firmando algo que no es tuyo. Bandera roja de deuda conceptual.
- **No sabrías rehacerlo sin la IA.** Si el proceso solo funciona porque el modelo hace un paso
  mágico que no comprendes, dependes de una caja negra.
- **Aceleraste al principio pero ahora corriges sin parar.** A veces la IA te da un 80% en cinco
  minutos y luego te cuesta dos horas arreglar el 20% — cuando hacerlo a mano habrían sido 40
  minutos. Cuenta el tiempo total, no solo el arranque.
- **El resultado suena mejor de lo que sabes que es.** Cuando la calidad de la prosa supera a tu
  confianza en el contenido, desconfía: es la *trampa de la fluidez* (§3.3) operando.
- **Nadie en el equipo entiende el artefacto.** Si el entregable no se puede mantener sin volver a
  invocar a la IA, has creado una dependencia, no una capacidad.

---

### 6.3 La regla del "lo entiendo lo suficiente para defenderlo"

Toda la sección se resume en una prueba sencilla que puedes aplicar antes de aceptar cualquier
resultado de la IA como tuyo:

> **La prueba de la defensa.** ¿Podrías **explicar y defender** este resultado ante un cliente,
> tu jefe o un colega —sin la IA delante— si te preguntan *por qué* es así? Si la respuesta es
> sí, la IA te aceleró. Si es no, no tienes un entregable: tienes **deuda conceptual disfrazada
> de productividad**.

Esto no significa entender cada detalle de todo. Significa entender **lo suficiente** para hacerte
responsable de ello. La IA es un colaborador extraordinario para **acelerar** lo que ya sabes
dirigir y verificar; se vuelve peligrosa el momento en que la usas para **sustituir** el
entendimiento en vez de para amplificarlo.

**La regla que cierra el módulo:**

- Usa la IA para **hacer más rápido** lo que entiendes → aceleración pura.
- Usa la IA para **aprender** algo que quieres entender → aceleración con verificación.
- Usa la IA para **saltarte** el entender algo de lo que serás responsable → deuda.

---

## 7. Glosario del Módulo

| Término | Definición breve |
|---------|-----------------|
| **Metodología** | Conjunto de hábitos repetibles para trabajar con IA en proyectos, no en tareas sueltas |
| **Specdoc** | Documento breve que describe *qué* construir antes de pedirlo: objetivo, restricciones, criterios |
| **Criterios de aceptación** | Lista verificable de condiciones que definen cuándo un entregable está "listo" |
| **No-objetivos** | Lo que deliberadamente se deja fuera del alcance, para delimitar el trabajo |
| **Flujo iterativo** | Ciclo *draft → revisión → refinamiento* que se repite hasta cumplir los criterios |
| **Draft (borrador)** | Primer resultado del modelo; punto de partida para iterar, no entregable final |
| **Dirigir y verificar** | El papel del humano: marcar el rumbo y comprobar el resultado, en vez de ejecutar |
| **Trampa de la fluidez** | Confundir que algo *suene bien* con que *esté bien*, por lo pulido de la prosa del modelo |
| **Documento de estado** | Archivo vivo que resume objetivo, decisiones, estado y pendientes de un proyecto largo |
| **Handoff (traspaso)** | Resumen de cierre/apertura de sesión que transporta la memoria de una a otra |
| **Hito** | Trozo manejable de un proyecto grande, con su propio mini-ciclo de especificar-iterar-verificar |
| **Ventana de contexto** | Capa 1 de memoria: lo que el modelo ve en la sesión actual; potente pero efímera (Módulo 2) |
| **Memoria de proyecto** | Capa 2: knowledge e instrucciones compartidas y persistentes de un Proyecto (Módulo 3) |
| **Memoria personal** | Capa 3: datos que la app recuerda de ti entre proyectos (preferencias, contexto estable) |
| **Contexto persistente** | Información que sobrevive a una sola sesión, guardada en un artefacto o en la memoria de la app |
| **Deuda técnica** | Resultado que funciona hoy pero es frágil y cuesta mantener o escalar |
| **Deuda conceptual** | Aceptar y usar algo que no entiendes; se paga cuando cambian las circunstancias o te preguntan por qué |
| **Prueba de la defensa** | Test de criterio: ¿podrías explicar y defender este resultado sin la IA delante? |

---

## 8. Práctica guiada (segunda hora)

> Estos ejercicios se hacen en vivo con Claude abierto. El objetivo no es "terminar" un
> entregable, sino **sentir cómo el método cambia el resultado**. Usa los insumos de la carpeta
> `insumos/` (mundo de **Imprenta Castro & MacDonald**). Tras cada uno, comparte el resultado y
> comenta en grupo.

### Ejercicio 1 — Escribir un specdoc · 12 min
Con el insumo del pedido de **Andes Verde**:
1. **Sin specdoc:** pídele directamente "hazme una propuesta para este cliente" y guarda el
   resultado.
2. Ahora escribe un **specdoc** de media página con las siete piezas (§2.3). Si te atascas, pídele
   al modelo que te haga 5 preguntas para completarlo.
3. Pide la propuesta **con** el specdoc delante.
4. **Reflexión:** ¿qué cambió entre las dos versiones? ¿Cuánto tiempo te ahorró el plano?

### Ejercicio 2 — El ciclo iterativo con feedback concreto · 15 min
Toma el borrador de propuesta del ejercicio anterior (que debería vivir en un **Artifact**).
1. Haz **una** ronda de feedback **vago** ("mejóralo", "más profesional") y observa el resultado.
2. Haz **dos rondas** de feedback **concreto y accionable** (usa la tabla de §3.2 como guía).
3. **Reflexión:** ¿qué tipo de feedback movió más el resultado? ¿En qué momento notaste que ya no
   valía la pena otra ronda?

### Ejercicio 3 — Verificar, no solo confiar · 12 min
Con la tabla de precios de la propuesta:
1. Pídele al modelo que calcule el **total con IVA y margen** en el texto del chat.
2. Ahora pídele que lo recalcule con **ejecución de código** (Módulo 3) y compara.
3. Aplica la **prueba de la defensa** (§6.3): ¿podrías explicar de dónde sale cada cifra ante el
   cliente? **Reflexión:** ¿dónde apareció deuda si te hubieras fiado del primer total?

### Ejercicio 4 — Continuidad entre sesiones · 15 min
Simula un proyecto de dos días:
1. "Cierra" la sesión pidiendo un **resumen de traspaso** (§4.3) y pégalo en un **documento de
   estado** (§4.2) con sus secciones.
2. Abre un **chat nuevo** (simulando el día siguiente), dale solo el documento de estado y pídele
   retomar por el primer pendiente **sin volver a explicarle el proyecto**.
3. **Reflexión:** ¿mantuvo la coherencia? ¿Qué faltaba en el documento de estado que tuviste que
   añadir a mano?

### Ejercicio 5 — Cazar la deuda · 8 min
Sobre cualquiera de los entregables generados hoy:
1. Señala **una** cosa que aceptaste sin entender del todo (una cifra, una afirmación, una
   estructura).
2. Pídele al modelo que te la **explique** hasta que puedas defenderla tú.
3. **Reflexión:** ¿era deuda conceptual? ¿Cuántos de tus entregables "terminados" pasarían la
   prueba de la defensa?

> **Cierre de la práctica:** ¿qué pieza del método —specdoc, ciclo iterativo, documento de estado
> o la prueba de la defensa— vas a incorporar a tu próximo proyecto real, y qué problema concreto
> te va a evitar?

---

## 9. Preguntas de repaso

Estas preguntas consolidan los conceptos antes de pasar al Módulo 5. No buscan una respuesta "de
examen": el objetivo es razonar en voz alta.

1. Un compañero dice: "para qué voy a escribir un specdoc, si tardo lo mismo en pedirlo
   directamente". ¿En qué casos tiene razón y en cuáles no? Menciona dos de las siete piezas que
   más gente olvida y por qué importan.

2. Tienes un borrador que no te convence. Explica por qué "rehacer el prompt desde cero" suele ser
   peor que **iterar**, y da un ejemplo de feedback vago transformado en feedback concreto.

3. ¿Qué significa "dirigir y verificar" y por qué la parte de **verificar** es la que más se
   descuida? Relaciónalo con la *trampa de la fluidez*.

4. Un proyecto cruza tres sesiones y en la tercera el modelo se contradice con una decisión de la
   primera. ¿Qué falló a nivel de método y qué artefacto lo habría evitado?

5. Explica las **tres capas de memoria** con un ejemplo de la imprenta para cada una. Si un dato de
   proyecto "se pierde" entre sesiones, ¿en qué capa debería haber estado guardado?

6. ¿Por qué un dato **desactualizado** en la memoria persistente puede ser peor que no tener el
   dato? Da dos prácticas para mitigarlo.

7. Distingue **deuda técnica** de **deuda conceptual** con un ejemplo de cada una fuera del mundo
   del código. ¿Cuál es más difícil de detectar y por qué?

8. Aplica la **prueba de la defensa** a una situación real de tu trabajo: ¿qué entregable reciente
   pasaría la prueba y cuál no? ¿Qué harías distinto?

9. La IA te dio el 80% de un informe en cinco minutos, pero llevas dos horas corrigiendo el 20%
   restante. ¿Aceleró o endeudó? ¿Cómo lo decides?

---

## 10. Recursos extra

Recursos seleccionados para profundizar. La documentación oficial de Anthropic es la referencia
primaria; el resto aporta contexto o perspectiva sobre metodología de trabajo con IA.

**Especificar y estructurar el trabajo (referencia primaria)**
- [Prompt engineering overview — Anthropic](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/overview) — la base de la que nace el specdoc: ser explícito, dar contexto, restricciones y formato.
- [Be clear, direct, and detailed — Anthropic](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/be-clear-and-direct) — por qué un blanco claro (el corazón del specdoc) rinde tanto mejor.
- [Let Claude think (chain of thought) — Anthropic](https://docs.anthropic.com/en/docs/build-with-claude/prompt-engineering/chain-of-thought-prompting) — pedir razonamiento antes de la respuesta, útil al iterar sobre borradores complejos.

**Flujo iterativo y proyectos**
- [Collaborate with Claude on Projects — Anthropic](https://www.anthropic.com/news/projects) — dónde viven el specdoc y el documento de estado: knowledge e instrucciones compartidas.
- [What are projects? — Claude Help Center](https://support.claude.com/en/articles/9517075-what-are-projects) — guía práctica para persistir el contexto de un proyecto largo.
- [What are artifacts and how do I use them? — Claude Help Center](https://support.claude.com/en/articles/9487310-what-are-artifacts-and-how-do-i-use-them) — el lienzo donde iterar borradores sin perderlos.

**Criterio, verificación y uso sostenible**
- [Reducing hallucinations — Anthropic](https://docs.anthropic.com/en/docs/test-and-evaluate/strengthen-guardrails/reduce-hallucinations) — técnicas para verificar y pedir citas, base de la lucha contra la deuda conceptual.
- [Claude.ai — sitio y producto](https://claude.ai/) — la mejor forma de interiorizar el método es aplicarlo en un proyecto real.

---

*Anterior: [Módulo 3 — Interfaz y Ecosistema](./modulo-3-wiki.md)*
*Siguiente: [Módulo 5 — IA en Acción: Galería de Casos](./modulo-5-wiki.md)*

---

> Versión 1.0 — Módulo 4 de 7 | Curso: Fundamentos de IA Productiva
> Actualizado: julio 2026
