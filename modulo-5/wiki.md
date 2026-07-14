# Módulo 5 — IA en Acción: Galería de Casos
### Fundamentos de IA Productiva

---

## Tabla de Contenidos

1. [Por qué este módulo es distinto](#1-por-qué-este-módulo-es-distinto)
2. [Cómo leer esta galería](#2-cómo-leer-esta-galería)
3. [Bloque A · Entender: datos, documentos y multimedia](#3-bloque-a--entender-datos-documentos-y-multimedia)
   - A1 [Un Excel de ventas que se explica solo](#a1-un-excel-de-ventas-que-se-explica-solo)
   - A2 [De una foto de factura a una tabla de datos](#a2-de-una-foto-de-factura-a-una-tabla-de-datos)
   - A3 [Un contrato largo, resumido y con sus riesgos](#a3-un-contrato-largo-resumido-y-con-sus-riesgos)
   - A4 [Una reunión o un video, convertidos en acuerdos](#a4-una-reunión-o-un-video-convertidos-en-acuerdos)
4. [Bloque B · Crear: apps, imágenes y texto](#4-bloque-b--crear-apps-imágenes-y-texto)
   - B1 [Una mini-aplicación en dos minutos](#b1-una-mini-aplicación-en-dos-minutos)
   - B2 [Imágenes para una campaña](#b2-imágenes-para-una-campaña)
   - B3 [El mismo mensaje en tres tonos](#b3-el-mismo-mensaje-en-tres-tonos)
5. [Bloque C · Actuar e investigar](#5-bloque-c--actuar-e-investigar)
   - C1 [La IA que ordena tu correo y tu agenda](#c1-la-ia-que-ordena-tu-correo-y-tu-agenda)
   - C2 [Investigar un tema con fuentes citadas](#c2-investigar-un-tema-con-fuentes-citadas)
6. [Bloque D · Pensar contigo](#6-bloque-d--pensar-contigo)
   - D1 [De una idea vaga a un plan accionable](#d1-de-una-idea-vaga-a-un-plan-accionable)
7. [Panorama: qué capacidad tapa qué necesidad](#7-panorama-qué-capacidad-tapa-qué-necesidad)
8. [Glosario del Módulo](#8-glosario-del-módulo)
9. [Práctica guiada (segunda hora)](#9-práctica-guiada-segunda-hora)
10. [Preguntas de repaso](#10-preguntas-de-repaso)
11. [Recursos extra](#11-recursos-extra)

---

## 1. Por qué este módulo es distinto

Los cuatro módulos anteriores fueron construyendo cimientos: **cómo piensa** el modelo (M1),
**cómo hablarle** (M2), **qué producto lo envuelve** (M3) y **con qué método** trabajar en
proyectos reales (M4). Este módulo no añade teoría nueva. Es un **recorrido de ejemplos
concretos**: diez casos de cosas que ya puedes hacer, hoy, con lo que aprendiste.

El objetivo no es que memorices los diez, sino que **veas el abanico**. Mucha gente usa la IA
para una sola cosa (redactar correos) sin sospechar que la misma herramienta analiza datos,
lee facturas, construye una mini-app o le pone orden a su correo. Cuando ves la variedad,
cambia la pregunta que te haces: dejas de preguntar *"¿me escribe esto?"* y empiezas a
preguntar *"¿de qué parte de mi trabajo podría encargarse?"*.

> **La idea que atraviesa el módulo:** cada uno de estos casos es una **combinación de
> capacidades que ya conoces** —una herramienta del M3, una técnica de prompt del M2, un
> método del M4—. No hay magia nueva; hay **recombinación**. Aprender a mirar tu día y
> reconocer *"esto es un caso de análisis de datos"* o *"esto es un caso de leer un documento"*
> es la verdadera habilidad.

Y una advertencia que vale para los diez, porque es el corazón del curso: **que la IA pueda
hacerlo no te exime de dirigir y verificar** (M4). Cada caso trae su "ojo" —el punto donde
tienes que comprobar antes de confiar—.

---

## 2. Cómo leer esta galería

Cada caso está presentado como una **ficha** con la misma estructura, para que puedas
compararlos y elegir por dónde empezar:

| Campo | Qué te dice |
|-------|-------------|
| **Escenario** | La situación real donde aparece la necesidad |
| **Qué le pides** | Un prompt de ejemplo, listo para adaptar |
| **Qué esperar** | El tipo de resultado que produce |
| **Qué capacidad usa** | La pieza del curso que hay debajo (para reconocerla en tu día) |
| **Ojo** | Dónde tienes que verificar antes de confiar |

Los casos están agrupados en cuatro bloques según **qué hace la IA**: *entender* material que le
das, *crear* cosas nuevas, *actuar* en tus sistemas y buscar en el mundo, o *pensar* contigo.
No es una lista cerrada: es un menú para encender ideas.

---

## 3. Bloque A · Entender: datos, documentos y multimedia

El primer superpoder es **procesar material que le das** —una hoja de cálculo, una foto, un
documento, una grabación— y devolverte algo útil. Aquí la IA no inventa: razona sobre lo que
tiene delante, que es donde más fiable es (M1).

### A1 · Un Excel de ventas que se explica solo

**Escenario.** Tienes una hoja con las ventas del trimestre y no tienes tiempo (ni ganas) de
armar tablas dinámicas para entenderla.

**Qué le pides:**
```
Te adjunto las ventas del trimestre. Analízalas y dime: producto más y
menos rentable, tendencia por mes, y el dato que más te sorprenda.
Hazme un gráfico de las ventas por mes. Usa cálculo real, no estimes.
```

**Qué esperar.** Un resumen con cifras exactas, un gráfico, y a menudo una observación que no
habías visto ("las ventas caen los lunes"). Puede además entregarte el resultado como un Excel
o un informe descargable.

**Qué capacidad usa.** *Ejecución de código* (M3): corre el cálculo de verdad en un sandbox, no
lo adivina. Esto tapa la debilidad aritmética del modelo (M1).

> **Ojo.** Pídele que **use ejecución de código** para los números; si los calcula "a ojo" en
> texto, pueden fallar. Y revisa que entendió bien las columnas (a veces confunde "unidades"
> con "ingresos"). Aplica la *prueba de la defensa* del M4.

---

### A2 · De una foto de factura a una tabla de datos

**Escenario.** Tienes un montón de facturas o recibos en papel (o en fotos del móvil) y
necesitas pasarlos a una hoja para contabilidad.

**Qué le pides:**
```
Te paso la foto de este recibo. Extrae proveedor, fecha, cada concepto
con su importe, subtotal, IVA y total, y ponlo en una tabla. Si algo no
se lee con seguridad, márcalo en vez de inventarlo.
```

**Qué esperar.** Una tabla limpia con los datos del recibo, lista para pegar en tu hoja. Puedes
hacerlo con varias fotos seguidas y pedir una tabla consolidada.

**Qué capacidad usa.** *Visión / análisis de imágenes* (M3): el modelo "ve" la foto y lee su
contenido, incluso manuscrito o mal iluminado.

> **Ojo.** La lectura visual es buena pero **no infalible**, sobre todo con cifras y texto
> pequeño. Verifica los importes críticos. El truco de pedirle que **marque lo dudoso** en
> lugar de rellenarlo evita que "alucine" un número (M1).

---

### A3 · Un contrato largo, resumido y con sus riesgos

**Escenario.** Te llega un contrato de proveedor de 25 páginas y necesitas saber qué firmas
antes de firmarlo, sin ser abogado.

**Qué le pides:**
```
Adjunto este contrato. Resúmelo en una página: qué me obliga, qué obliga
a la otra parte, plazos, penalizaciones y cláusulas que me pondrían en
riesgo. Cita la sección de cada punto para poder verificarlo.
```

**Qué esperar.** Un resumen ejecutivo con lo esencial, una lista de riesgos y **citas a las
cláusulas** para que puedas ir al texto original.

**Qué capacidad usa.** *Análisis de documentos* + *citas* (M3/M1): razona sobre el documento que
le das —mucho más fiable que tirar de memoria— y ancla cada afirmación a su fuente.

> **Ojo.** Esto **no sustituye a un abogado** para lo importante: es un lector rápido que te
> prepara las preguntas correctas. **Abre las citas** y confírmalas; que cite una cláusula no
> garantiza que la interpretó bien.

---

### A4 · Una reunión o un video, convertidos en acuerdos

**Escenario.** Grabaste una reunión de una hora, o hay un video/tutorial largo que no tienes
tiempo de ver entero.

**Qué le pides:**
```
Aquí está la transcripción (o el enlace) de la reunión. Dame: los tres
temas principales, las decisiones tomadas, y una lista de tareas con
responsable y fecha si se mencionaron. Marca lo que quedó sin cerrar.
```

**Qué esperar.** De una hora de charla dispersa, media página con acuerdos, tareas y cabos
sueltos. Con un video largo, un resumen que te ahorra verlo completo.

**Qué capacidad usa.** *Capacidad multimodal* (audio/video) + *resumen estructurado* (M2):
comprime y organiza material largo en la salida que tú definiste.

> **Ojo.** Si la transcripción tiene errores (nombres, cifras dichas de pasada), se arrastran al
> resumen. Para acuerdos con consecuencias, **verifica contra la grabación**. Y recuerda la
> privacidad: cuidado con qué reuniones subes (se trata a fondo en el M7).

---

## 4. Bloque B · Crear: apps, imágenes y texto

El segundo superpoder es **producir cosas nuevas** que antes exigían una herramienta
especializada o una habilidad que no tenías: programar, diseñar, redactar en un registro
distinto.

### B1 · Una mini-aplicación en dos minutos

**Escenario.** Quieres una calculadora de presupuestos a la medida, o un pequeño quiz para tu
equipo, pero no sabes programar y montar algo así llevaría días.

**Qué le pides:**
```
Créame una calculadora de presupuestos de impresión: campos para tirada,
número de páginas y tipo de papel (con tres precios distintos), que
muestre el subtotal, el IVA y el total. Que se vea limpia y funcione en
el navegador.
```

**Qué esperar.** Una aplicación **funcionando** dentro de un Artifact: la usas ahí mismo, la
iteras ("añade un descuento por volumen"), la compartes con un enlace y la descargas.

**Qué capacidad usa.** *Artifacts* + generación de código (M3): el modelo escribe el programa y
te lo entrega ejecutándose, sin que tú toques código. Es el patrón *iterar sobre un borrador*
del M4, pero con una app.

> **Ojo.** Es genial para herramientas internas y prototipos. Para algo de lo que dependa el
> negocio, **verifica la lógica** (¿el cálculo del IVA es correcto?) y no lo trates como
> software probado. Es el ejemplo perfecto de *deuda técnica* si lo usas sin entenderlo (M4).

---

### B2 · Imágenes para una campaña

**Escenario.** Necesitas ideas visuales para una promoción —un concepto, un fondo, una
ilustración— y no tienes diseñador a mano ni banco de imágenes.

**Qué le pides:**
```
Genera tres conceptos de imagen para una campaña de catálogo de alimentos
orgánicos: tono natural, colores tierra y verdes, sensación artesanal.
Una versión luminosa, una más rústica y una minimalista.
```

**Qué esperar.** Varias propuestas visuales para elegir, refinar o usar como referencia para un
diseñador. Ideal para explorar rápido antes de invertir en producción.

**Qué capacidad usa.** *Generación de imágenes*: el modelo crea imágenes a partir de tu
descripción (recuerda del M2 que la claridad del prompt manda: cuanto mejor describes, mejor
sale).

> **Ojo.** Las imágenes generadas pueden tener detalles raros (texto deforme, manos extrañas) y
> hay que cuidar **derechos de uso y estilo de marca**. Trátalas como bocetos e ideas, no
> siempre como arte final listo para imprenta.

---

### B3 · El mismo mensaje en tres tonos

**Escenario.** Tienes que comunicar una subida de precios, y no es lo mismo decírselo a un
cliente antiguo, a la prensa o al equipo interno.

**Qué le pides:**
```
Tengo que anunciar un aumento del 8% en impresión. Escríbeme tres
versiones del mensaje: una cercana para clientes de confianza, una formal
para clientes nuevos, y una breve y directa para el equipo interno.
```

**Qué esperar.** Tres textos con el mismo fondo y distinto registro, listos para ajustar. Ver
las versiones lado a lado te ayuda a decidir el tono correcto.

**Qué capacidad usa.** *Rol, tono y estilo* (M2/M3): la misma información moldeada para audiencias
distintas. Es prompt engineering puro, aplicado a comunicación.

> **Ojo.** Un mensaje delicado (subir precios, un despido, una disculpa) **siempre pasa por tu
> criterio** antes de enviarse. La IA te da el borrador; el juicio sobre qué es apropiado es
> tuyo (dirigir y verificar, M4).

---

## 5. Bloque C · Actuar e investigar

El tercer superpoder es el que más impresiona: la IA deja de solo *hablar* y empieza a *operar*
—en tus sistemas mediante connectors, o en el mundo mediante la búsqueda web—.

### C1 · La IA que ordena tu correo y tu agenda

**Escenario.** Abres el correo y tienes 40 mensajes sin leer; no sabes por dónde empezar y hay
fechas escondidas que se te van a pasar.

**Qué le pides:**
```
Revisa mi correo de hoy y hazme un resumen de lo urgente y lo que espera
respuesta. Si algún mensaje menciona una fecha o reunión, propón crear el
evento en mi calendario (pídeme confirmación antes de crearlo).
```

**Qué esperar.** Un resumen priorizado de tu bandeja y eventos de calendario propuestos a partir
de lo que leyó. La IA **actúa** en tus herramientas, no solo comenta.

**Qué capacidad usa.** *Connectors / MCP* (M3): el bucle agéntico *descubrir → decidir → ejecutar
→ continuar*. Aquí es donde el modelo pasa de contestar a operar.

> **Ojo.** Esto es lo más potente **y lo más sensible**. Aplica *mínimo privilegio* (M3): da solo
> los permisos necesarios y exige **confirmación antes de acciones con consecuencias** (enviar,
> borrar, agendar). Y cuidado con la *inyección de prompt indirecta* (M3): un correo malicioso
> podría intentar dar órdenes al modelo.

---

### C2 · Investigar un tema con fuentes citadas

**Escenario.** Tienes que decidir entre tres proveedores, o entender una normativa nueva, y
necesitas información **actual** —no lo que el modelo "recuerde" de su entrenamiento—.

**Qué le pides:**
```
Investiga las tres normativas de etiquetado de alimentos orgánicos
vigentes en la región este año. Compáralas en una tabla (requisitos,
costos, plazos) y cítame la fuente de cada dato con enlace.
```

**Qué esperar.** Un informe comparativo con datos recientes y **enlaces a las fuentes** que
puedes abrir y verificar. Convierte una búsqueda de horas en minutos.

**Qué capacidad usa.** *Búsqueda web* (M3): consulta internet en vivo y trae información posterior
a su fecha de corte (M1), con trazabilidad.

> **Ojo.** Que cite una fuente **no garantiza que la haya leído bien**: abre los enlaces de los
> datos que importan. Para decisiones serias, la fuente citada es el principio de la
> verificación, no el final.

---

## 6. Bloque D · Pensar contigo

El último superpoder es más sutil pero quizá el más transformador: usar la IA como un
**socio de pensamiento** que te ayuda a pasar del "no sé por dónde empezar" a un plan concreto.

### D1 · De una idea vaga a un plan accionable

**Escenario.** Tienes una idea difusa —"quiero digitalizar los pedidos de la imprenta", "quiero
organizar el archivo del taller"— pero no sabes cómo aterrizarla.

**Qué le pides:**
```
Tengo una idea vaga: digitalizar los pedidos de la imprenta, que hoy van
en papel. Hazme primero cinco preguntas para entender el contexto. Con mis
respuestas, arma un plan por fases con pasos concretos y un primer paso
que pueda hacer esta semana.
```

**Qué esperar.** Primero preguntas que te obligan a pensar (como en un specdoc, M4); luego un
plan por fases, realista y con un arranque inmediato. La IA no decide por ti: **estructura tu
pensamiento**.

**Qué capacidad usa.** *Razonamiento + método* (M4): el ciclo de especificar antes de ejecutar y
trocear en hitos, aplicado a una idea propia. Aquí no hace falta ninguna herramienta especial,
solo un buen prompt.

> **Ojo.** El plan es un punto de partida, no una verdad revelada. Tú conoces restricciones que
> el modelo no (presupuesto real, política interna, personas). **Ajústalo** con tu criterio: es
> el mejor ejemplo de la IA *amplificando* tu juicio en vez de sustituirlo.

---

## 7. Panorama: qué capacidad tapa qué necesidad

Los diez casos, vistos como lo que son —capacidades del curso recombinadas—:

| Caso | Necesidad que resuelve | Capacidad (módulo) |
|------|------------------------|--------------------|
| A1 · Excel de ventas | Entender datos sin saber de tablas dinámicas | Ejecución de código (M3) |
| A2 · Foto de factura | Pasar papel a datos sin teclear | Visión (M3) |
| A3 · Contrato | Leer documentos densos rápido y con anclaje | Análisis de docs + citas (M3/M1) |
| A4 · Reunión/video | Comprimir horas de audio en acuerdos | Multimodal + resumen (M2) |
| B1 · Mini-app | Crear una herramienta sin programar | Artifacts (M3) |
| B2 · Imágenes | Producir visuales sin diseñador | Generación de imágenes |
| B3 · Tres tonos | Adaptar un mensaje a cada audiencia | Rol y estilo (M2/M3) |
| C1 · Correo y agenda | Que la IA actúe en tus sistemas | Connectors / MCP (M3) |
| C2 · Investigación | Información actual y verificable | Búsqueda web (M3) |
| D1 · Idea → plan | Estructurar el pensamiento propio | Método + razonamiento (M4) |

> **La conclusión del módulo:** no necesitas aprender "diez herramientas nuevas". Necesitas
> reconocer, en tu propio día, **de qué tipo de caso se trata cada tarea** —y ya sabes la
> capacidad que lo resuelve. Esa mirada es lo que convierte la IA en una herramienta de trabajo
> real y no en un juguete para preguntas sueltas.

---

## 8. Glosario del Módulo

| Término | Definición breve |
|---------|-----------------|
| **Caso de uso** | Una tarea concreta resuelta combinando capacidades de la IA que ya conoces |
| **Multimodal** | Capacidad de trabajar con más de un tipo de contenido: texto, imágenes, audio, video |
| **Visión** | Que el modelo "vea" y razone sobre imágenes: fotos, capturas, documentos escaneados |
| **Generación de imágenes** | Crear imágenes nuevas a partir de una descripción en texto |
| **Ejecución de código** | Correr cálculos o análisis reales en un sandbox, en vez de estimarlos (M3) |
| **Artifact** | Panel junto al chat donde vive y se ejecuta contenido reutilizable, como una mini-app (M3) |
| **Connector / MCP** | Integración que permite a la IA actuar en tus apps y datos (M3) |
| **Búsqueda web** | Consulta a internet en vivo para traer información actual con fuentes (M3) |
| **Bucle agéntico** | Ciclo en que el modelo decide, ejecuta una acción y continúa con el resultado (M3) |
| **Prueba de la defensa** | Test de criterio: ¿podrías explicar y defender el resultado sin la IA delante? (M4) |
| **Mínimo privilegio** | Conceder solo el acceso estrictamente necesario para la tarea (M3) |

---

## 9. Práctica guiada (segunda hora)

> El objetivo de hoy no es dominar una técnica, sino **probar la variedad** y salir con al menos
> un caso que vas a incorporar a tu trabajo. Elige, entre todos, cuatro o cinco casos y hazlos
> en vivo. Usa los materiales de la carpeta `insumos/`. Tras cada uno, comparte el resultado y
> comenta en grupo qué te sorprendió.

### Ejercicio 1 — Entender datos · 12 min · (Caso A1)
Con el insumo `01-ventas.csv`:
1. Pide el análisis **exigiendo ejecución de código** y un gráfico.
2. Aplica la *prueba de la defensa*: ¿sabrías explicar de dónde sale cada cifra?
3. **Reflexión:** ¿qué dato no habrías visto tú a simple vista?

### Ejercicio 2 — Leer un documento · 12 min · (Caso A3)
Con el insumo `02-contrato-extracto.md`:
1. Pide el resumen de una página con **riesgos y citas**.
2. Abre **una** cita y verifica que la interpretó bien.
3. **Reflexión:** ¿en qué te ayudó y dónde seguirías necesitando a un humano experto?

### Ejercicio 3 — Crear algo · 15 min · (Caso B1 o B3)
Elige uno:
- **Mini-app:** pide la calculadora de presupuestos en un Artifact e itera un cambio.
- **Tres tonos:** con `03-anuncio-precios.md`, genera las tres versiones y elige.
**Reflexión:** ¿qué habrías tardado tú en hacer lo mismo sin IA?

### Ejercicio 4 — Investigar o actuar · 12 min · (Caso C2 o C1)
Elige uno:
- **Investigación:** pide una comparación de un tema actual **con fuentes citadas** y abre dos.
- **Connector** (si hay uno activo): pide un resumen de correo/agenda con confirmación antes de
  actuar.
**Reflexión:** ¿confiarías en el resultado sin abrir ninguna fuente? ¿Por qué no?

### Ejercicio 5 — Pensar contigo · 12 min · (Caso D1)
Con el insumo `04-idea-vaga.md` (o una idea real tuya):
1. Pide que te haga **cinco preguntas** antes de planear.
2. Con tus respuestas, pide un **plan por fases** con un primer paso para esta semana.
3. **Reflexión:** ¿el plan capturó tus restricciones reales? ¿Qué ajustaste con tu criterio?

> **Cierre de la práctica:** de los diez casos, ¿cuál te llevas para tu trabajo desde mañana? ¿Y
> cuál te sorprendió que fuera posible?

---

## 10. Preguntas de repaso

Estas preguntas consolidan la mirada del módulo. No buscan una respuesta "de examen": el
objetivo es que aprendas a **clasificar tus propias tareas** por tipo de caso.

1. De estos diez casos, ninguno usa una "herramienta mágica nueva". Elige tres y di qué
   capacidad de los Módulos 1-4 hay debajo de cada uno.

2. Un compañero solo usa la IA para redactar correos. Proponle **dos casos** de esta galería que
   encajen con su trabajo y explícale qué ganaría.

3. En el caso del Excel de ventas (A1) y el de la factura (A2), ¿por qué es especialmente
   importante **verificar los números**, y qué técnica del M1 explica el riesgo?

4. Compara el caso "leer un contrato" (A3) con "investigar con fuentes" (C2): ambos dan **citas**.
   ¿Por qué abrir esas citas sigue siendo tu responsabilidad?

5. El caso del correo y la agenda (C1) es el más potente y el más sensible. Nombra **dos
   precauciones** (de las que vimos en el M3) que aplicarías antes de darle acceso.

6. La mini-app (B1) es un ejemplo perfecto de dónde la IA puede meter **deuda técnica**. ¿Qué
   harías para usarla sin acumular esa deuda (M4)?

7. Toma una tarea **real** de tu semana. ¿De qué tipo de caso es (entender, crear, actuar,
   pensar)? ¿Qué capacidad usarías y dónde tendrías que verificar?

---

## 11. Recursos extra

Recursos para explorar las capacidades de esta galería por tu cuenta. La mejor forma de
interiorizarlas es **probarlas** con material tuyo.

**Capacidades integradas (referencia primaria)**
- [Claude.ai — sitio y producto](https://claude.ai/) — el lugar donde probar casi todos estos casos.
- [Enabling and using the analysis tool — Claude Help Center](https://support.claude.com/en/articles/10008684-enabling-and-using-the-analysis-tool) — la ejecución de código para datos y cálculos (casos A1, B1).
- [What are artifacts and how do I use them? — Claude Help Center](https://support.claude.com/en/articles/9487310-what-are-artifacts-and-how-do-i-use-them) — el lienzo donde vive una mini-app (caso B1).
- [Enable and use web search — Claude Help Center](https://support.claude.com/en/articles/10684626-enable-and-use-web-search) — información actual con fuentes (caso C2).

**Actuar en tus sistemas**
- [Pre-built web connectors using remote MCP — Claude Help Center](https://support.claude.com/en/articles/11176164-pre-built-web-connectors-using-remote-mcp) — activar connectors sin código (caso C1).
- [When should I use web search, extended thinking, and research? — Claude Help Center](https://support.claude.com/en/articles/11095361-when-should-i-use-web-search-extended-thinking-and-research) — criterio para elegir la capacidad correcta.

**Trabajar con imágenes y documentos**
- [Vision — Anthropic](https://docs.anthropic.com/en/docs/build-with-claude/vision) — cómo el modelo lee imágenes y documentos (casos A2, A3).

---

*Anterior: [Módulo 4 — Metodologías de desarrollo con IA](./modulo-4-wiki.md)*
*Siguiente: Módulo 6 — Herramientas especializadas*

---

> Versión 1.0 — Módulo 5 de 7 | Curso: Fundamentos de IA Productiva
> Actualizado: julio 2026
