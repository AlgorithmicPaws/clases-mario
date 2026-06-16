# Módulo 2 — Trabajar con el Modelo
### Fundamentos de IA Productiva

> **Perfil del lector:** ingeniero informático con sólida experiencia técnica para quien
> el paradigma de inteligencia artificial es nuevo. Este documento explica los conceptos de
> forma directa y técnica, y profundiza más allá de lo presentado en clase: cada sección
> añade detalle, matices y consecuencias prácticas que la presentación solo enuncia.

> **Formato de la clase:** una primera hora de **conceptos y demostración** (secciones 1 a 5)
> y una segunda hora de **práctica y retroalimentación** (sección 7). La sección 7 está
> pensada para hacerse en vivo, con el modelo abierto al lado.

---

## Tabla de Contenidos

1. [La ventana de contexto](#1-la-ventana-de-contexto)
   - 1.1 [Qué es la ventana de contexto](#11-qué-es-la-ventana-de-contexto)
   - 1.2 [Qué ocupa la ventana (todo cuenta)](#12-qué-ocupa-la-ventana-todo-cuenta)
   - 1.3 [Por qué importa: costo, límite y latencia](#13-por-qué-importa-costo-límite-y-latencia)
   - 1.4 [Context rot: más contexto no es mejor contexto](#14-context-rot-más-contexto-no-es-mejor-contexto)
   - 1.5 [Estrategias para gestionar la ventana](#15-estrategias-para-gestionar-la-ventana)
2. [Prompt engineering: la base](#2-prompt-engineering-la-base)
   - 2.1 [Claridad y dirección: la regla de oro](#21-claridad-y-dirección-la-regla-de-oro)
   - 2.2 [Dar contexto y motivación (el "por qué")](#22-dar-contexto-y-motivación-el-por-qué)
   - 2.3 [Rol y system prompt](#23-rol-y-system-prompt)
   - 2.4 [Controlar el formato de salida](#24-controlar-el-formato-de-salida)
   - 2.5 [Anatomía de un buen prompt](#25-anatomía-de-un-buen-prompt)
3. [Estrategias de estructuración](#3-estrategias-de-estructuración)
   - 3.1 [Few-shot: enseñar con ejemplos](#31-few-shot-enseñar-con-ejemplos)
   - 3.2 [Chain-of-thought: pedir que razone en pasos](#32-chain-of-thought-pedir-que-razone-en-pasos)
   - 3.3 [XML tagging: estructurar el prompt](#33-xml-tagging-estructurar-el-prompt)
   - 3.4 [Combinarlas: el patrón completo](#34-combinarlas-el-patrón-completo)
4. [Una tarea vs. varias: cuándo dividir](#4-una-tarea-vs-varias-cuándo-dividir)
   - 4.1 [Señales de que un prompt hace demasiado](#41-señales-de-que-un-prompt-hace-demasiado)
   - 4.2 [Prompt chaining: encadenar pasos](#42-prompt-chaining-encadenar-pasos)
   - 4.3 [Cuándo conviene todo en un solo prompt](#43-cuándo-conviene-todo-en-un-solo-prompt)
5. [Evaluar si una respuesta es buena](#5-evaluar-si-una-respuesta-es-buena)
   - 5.1 ["Suena bien" no es "es correcto"](#51-suena-bien-no-es-es-correcto)
   - 5.2 [Los cinco criterios](#52-los-cinco-criterios)
   - 5.3 [Rúbricas y el modelo como juez](#53-rúbricas-y-el-modelo-como-juez)
   - 5.4 [Checklist práctico de revisión](#54-checklist-práctico-de-revisión)
6. [Glosario del Módulo](#6-glosario-del-módulo)
7. [Práctica guiada (segunda hora)](#7-práctica-guiada-segunda-hora)
8. [Preguntas de repaso](#8-preguntas-de-repaso)
9. [Recursos extra](#9-recursos-extra)

---

## 1. La ventana de contexto

### 1.1 Qué es la ventana de contexto

La **ventana de contexto** es la cantidad máxima de tokens (ver Módulo 1) que el modelo puede
tener "a la vista" en una sola interacción. Incluye **todo**: tus instrucciones, el historial
de la conversación, los documentos que pegaste, las definiciones de herramientas y la propia
respuesta que está generando. Es un espacio finito y compartido entre la entrada y la salida.

Hay un punto que choca con la intuición de un ingeniero acostumbrado a procesos con estado: el
modelo **no tiene memoria entre llamadas**. Cada vez que envías un mensaje, la plataforma le
reenvía toda la conversación desde el inicio. Lo que parece "memoria" en un chat es, en
realidad, el historial completo viajando una y otra vez dentro de la ventana. Cuando la
conversación deja de caber, lo más antiguo se descarta o se resume — y a partir de ahí el
modelo "olvida" esos tramos porque, literalmente, ya no los está viendo.

Esto también explica que dos chats distintos no compartan nada: cada conversación es su propia
ventana aislada. Si en otro hilo le diste contexto valioso, en este no existe.

> **En resumen:** la ventana de contexto es la memoria de trabajo del modelo para *esta*
> interacción. No es un disco duro ni una base de datos: es un espacio finito que se llena, y
> lo que no está dentro, para el modelo no existe.

---

### 1.2 Qué ocupa la ventana (todo cuenta)

Es fácil pensar que la ventana solo la ocupa "lo que escribo". En realidad la consumen varias
fuentes simultáneas:

```
┌──────────────────── VENTANA DE CONTEXTO (p. ej. 200k tokens) ───────────────────┐
│                                                                                  │
│  [System prompt]   instrucciones de la plataforma + rol + reglas                 │
│  [Herramientas]    definiciones de tools disponibles (búsqueda, código…)         │
│  [Documentos]      archivos pegados, PDFs, código adjunto                        │
│  [Historial]       todos los turnos previos de la conversación                   │
│  [Tu mensaje]      la pregunta o instrucción actual                              │
│  [Respuesta]       lo que el modelo está generando ahora (también ocupa)         │
│                                                                                  │
└──────────────────────────────────────────────────────────────────────────────┘
```

Esto explica comportamientos que de otro modo parecen caprichosos:

- En una conversación larga, el modelo "olvida" algo del principio: ese tramo se quedó fuera
  de la ventana o se resumió.
- Pegar un PDF de 80 páginas consume gran parte del espacio antes de que escribas tu pregunta.
- Una respuesta larga puede cortarse a medias: no quedaba espacio de salida.
- El modelo deja de seguir una instrucción del system prompt en chats muy largos: queda
  "lejos" y compite con todo lo demás por su atención.

> **Punto clave para un técnico:** la ventana se mide en **tokens, no en mensajes**. Un mensaje
> corto con un archivo adjunto enorme puede ocupar más que cincuenta mensajes de texto.
> Razonar en tokens, no en turnos, es el cambio mental que hay que hacer. Las plataformas
> suelen exponer un contador de uso de contexto: vale la pena mirarlo.

---

### 1.3 Por qué importa: costo, límite y latencia

La gestión de la ventana no es un tecnicismo: impacta directamente cuatro cosas que te importan
en el trabajo real.

| Dimensión | Cómo la afecta la ventana |
|-----------|---------------------------|
| **Costo** | Se cobra por token de entrada **y** de salida. Reenviar un historial gigante en cada turno multiplica el costo, aunque tu pregunta sea de una línea. |
| **Límite** | Si lo que quieres meter no cabe, no entra. Hay que elegir qué incluir. |
| **Latencia** | Más tokens de entrada → respuesta más lenta. Una ventana medio llena responde más despacio que una limpia. |
| **Calidad** | Contraintuitivo pero medido: más contexto puede **empeorar** la respuesta (ver 1.4). |

> **Prompt caching.** Las plataformas modernas permiten *cachear* partes estables del contexto
> (un documento largo, un system prompt extenso) para no reprocesarlas ni volver a pagarlas
> enteras en cada turno. El primer envío cuesta normal; los siguientes que reutilizan ese
> tramo cacheado son mucho más baratos y rápidos. No tienes que configurarlo en un chat
> normal, pero es la razón por la que reutilizar el mismo documento en una conversación sale
> más barato que pegarlo de nuevo cada vez — y un punto de diseño importante si construyes
> aplicaciones sobre la API.

---

### 1.4 Context rot: más contexto no es mejor contexto

Uno de los hallazgos más importantes y menos intuitivos de los últimos años: **el rendimiento
del modelo se degrada a medida que crece la entrada**, aunque el dato relevante siga estando
ahí. Se le llama *context rot* ("pudrición del contexto").

La intuición de "le doy todo y que él filtre" es justo la equivocada. Cuanta más información
irrelevante metes, más se diluye la señal relevante entre el ruido, y más le cuesta al
mecanismo de atención (Módulo 1) localizar lo que importa.

**Dos fenómenos relacionados:**

**"Lost in the middle" (perdido en el medio).** Los modelos prestan más atención al **inicio**
y al **final** del contexto que al medio. La precisión dibuja una curva en forma de U: alta en
los extremos, baja en el centro. Cuando el dato relevante se mueve del borde al medio, el
rendimiento puede caer **más de un 30%**.

**Degradación por longitud.** Un estudio de Chroma (2025) probó 18 modelos de frontera (GPT-4.1,
Claude 4, Gemini 2.5, Qwen3) y **todos** rindieron peor a medida que crecía la entrada — la
caída más pronunciada en el rango de 100k–500k tokens. No es defecto de un modelo concreto: es
una propiedad general de la arquitectura.

```
Precisión al recuperar un dato según su posición en un contexto largo:

  alta │■■■■■                                   ■■■■■
       │     ■■■                             ■■■
       │        ■■                         ■■
       │          ■■                     ■■
       │            ■■■               ■■■
  baja │               ■■■■■■■■■■■■■■■
       └────────────────────────────────────────────
        inicio            el medio              final
        (se ve bien)   (se "diluye")        (se ve bien)
```

> **Implicación práctica directa:**
> 1. **Pon lo importante al principio o al final**, no enterrado en el medio.
> 2. Con documentos largos, **pon el documento arriba y tu pregunta al final** — en pruebas de
>    Anthropic esto mejora la calidad hasta un 30% en entradas complejas.
> 3. **Menos es más.** Un contexto curado y relevante supera a uno enorme y ruidoso. La
>    habilidad no es "meter todo", es *elegir qué meter*.

Conviene también distinguir la ventana **anunciada** de la **efectiva**: que un modelo acepte
1M de tokens no significa que razone igual de bien con la ventana llena. La cifra de catálogo
es un techo, no una garantía de calidad a esa longitud.

---

### 1.5 Estrategias para gestionar la ventana

| Estrategia | Cuándo usarla |
|-----------|---------------|
| **Curar, no acumular** | Siempre. Incluye solo los documentos y el historial que de verdad hacen falta para la tarea actual. |
| **Documento arriba, pregunta abajo** | Al trabajar sobre un texto largo. Mejora la precisión y reduce el "lost in the middle". |
| **Pedir citas primero** | En análisis de documentos: pídele que primero extraiga las citas relevantes y luego responda. Eso lo ancla al texto y reduce alucinaciones. |
| **Resumir y reiniciar** | Cuando una conversación se vuelve muy larga, pídele un resumen del estado y empieza un chat nuevo con ese resumen. Limpia la mesa. |
| **Una tarea por conversación** | Mezclar tres temas distintos en un mismo chat ensucia el contexto. Un hilo por objetivo. |
| **Dividir el material** | Si un documento no cabe o satura la ventana, trocéalo y procésalo por partes (enlaza con prompt chaining, 4.2). |

> **Regla mental:** trata la ventana como un recurso escaso que tú administras, no como un
> cajón infinito donde tirar todo. La calidad de la salida depende tanto de lo que *quitas*
> como de lo que pones.

---

## 2. Prompt engineering: la base

El *prompt engineering* es el oficio de escribir instrucciones que produzcan buenas respuestas
de forma fiable. No es magia ni "palabras secretas": es comunicación clara y específica
aplicada a un sistema muy capaz pero literal, que no comparte tu contexto, tus convenciones ni
lo que tienes en la cabeza.

El cambio de mentalidad clave: el modelo **no adivina tu intención**. Si algo se puede
interpretar de dos formas, lo interpretará de cualquiera de ellas. La mayor parte de las
respuestas malas no son culpa del modelo, sino de un prompt que dejaba demasiado implícito. La
buena noticia es que esto es controlable: casi todo problema de calidad se resuelve mejorando
el prompt antes que cambiando de modelo.

---

### 2.1 Claridad y dirección: la regla de oro

La causa número uno de respuestas malas es un prompt ambiguo. El modelo responde
excepcionalmente bien a instrucciones explícitas y específicas, y mal a las vagas.

> **La regla de oro (Anthropic).** Muéstrale tu prompt a un colega con poco contexto de la
> tarea y pídele que lo siga. **Si se confunde, el modelo también se confundirá.**

```
Menos efectivo:
  "Crea un dashboard de analítica."

Más efectivo:
  "Crea un dashboard de analítica. Incluye tantas funciones e interacciones
   relevantes como sea posible. Ve más allá de lo básico para lograr una
   implementación completa."
```

Tres hábitos concretos:

- **Sé específico sobre el formato y las restricciones** de la salida que esperas (longitud,
  estructura, idioma, audiencia, qué incluir y qué no).
- **Da instrucciones como pasos secuenciales** (lista numerada) cuando el orden o la
  completitud importan.
- **Define los términos ambiguos.** Si pides un resumen "breve", di "máximo 5 viñetas". "Breve"
  significa cosas distintas para ti y para el modelo.

> **Matiz importante (2026):** los modelos actuales siguen instrucciones de forma muy literal y
> son muy proactivos. El truco de gritar **"CRÍTICO: DEBES hacer X"** que funcionaba en modelos
> antiguos hoy provoca el efecto contrario (*overtriggering*: el modelo sobre-reacciona). Con
> los modelos actuales basta lenguaje normal y directo: *"Usa esta herramienta cuando…"*.

---

### 2.2 Dar contexto y motivación (el "por qué")

Explicarle al modelo *por qué* quieres algo mejora la respuesta, porque le permite generalizar
a partir de la intención en lugar de seguir la regla al pie de la letra y fallar en los casos
que no previste.

```
Menos efectivo:
  "NUNCA uses puntos suspensivos."

Más efectivo:
  "Tu respuesta la leerá en voz alta un motor de texto-a-voz, así que nunca uses
   puntos suspensivos porque el motor no sabe pronunciarlos."
```

Con el "por qué", el modelo entiende el objetivo real y toma decisiones coherentes en
situaciones que tu regla no contemplaba (p. ej., también evitará otros símbolos impronunciables,
no solo los puntos suspensivos). Es la diferencia entre dar una orden aislada y dar el criterio
detrás de la orden.

Lo mismo aplica al contexto de fondo: para quién es la salida, dónde se va a usar, qué nivel de
detalle se espera, qué decisiones dependen de ella. Cuanto mejor entienda el objetivo, mejores
serán sus juicios en lo que no especificaste.

---

### 2.3 Rol y system prompt

Asignar un **rol** enfoca el tono, el vocabulario y el comportamiento del modelo. Incluso una
sola frase marca diferencia. En interfaces de chat esto suele ir en las "instrucciones
personalizadas" o en la descripción de un Proyecto; vía API es el *system prompt*.

```
Sin rol:
  "¿Cómo ordeno una lista de diccionarios por una clave?"

Con rol (system prompt):
  "Eres un asistente experto en Python que prioriza código idiomático y legible.
   Explicas el porqué de cada decisión en una frase."
```

> **Diferencia clave:** el **system prompt** define *quién es* el modelo y *cómo* debe
> comportarse de forma persistente durante toda la conversación. El **mensaje de usuario** es la
> tarea concreta de este turno. Separar ambos mantiene el comportamiento estable entre
> preguntas: el rol no se "gasta", aplica a todos los turnos.

Buenas prácticas para el system prompt: que sea estable (no lo cambies a mitad de hilo sin
motivo), que recoja las reglas que aplican siempre (tono, formato, restricciones), y que no se
mezcle con la petición puntual. Si una instrucción solo aplica a *este* mensaje, va en el
mensaje, no en el rol.

---

### 2.4 Controlar el formato de salida

Tres técnicas que funcionan especialmente bien para dirigir el formato:

**1. Di qué hacer, no qué no hacer.** Las instrucciones en positivo son más fiables que las
prohibiciones.

```
En vez de:  "No uses markdown."
Prueba:     "Escribe la respuesta en párrafos de prosa que fluyan con naturalidad."
```

**2. Usa indicadores de formato con etiquetas.**

```
"Escribe las secciones de prosa de tu respuesta dentro de etiquetas
 <prosa> ... </prosa>."
```

**3. Haz que el estilo de tu prompt se parezca al de la salida deseada.** El formato del prompt
influye en el de la respuesta: si escribes el prompt sin markdown, recibes menos markdown; si
quieres prosa, escribe en prosa. Si quieres JSON, muéstrale el esquema exacto.

Para salidas estructuradas que va a consumir otro programa (JSON, CSV), dos refuerzos extra:
**da el esquema explícito** con nombres de campo y tipos, y **prefija el inicio de la respuesta**
(p. ej., empezar tú con `{` ) para evitar que el modelo añada texto introductorio. Muchas APIs
ofrecen además un "modo JSON" o *structured output* que garantiza un objeto válido.

> **Nota de 2026:** los modelos actuales son más concisos por defecto y pueden saltarse
> resúmenes o preámbulos. Si quieres más detalle, un resumen final o que explique su
> razonamiento, **pídelo explícitamente**.

---

### 2.5 Anatomía de un buen prompt

No todos los prompts necesitan todas las piezas, pero este es el esqueleto completo, en un orden
que funciona bien:

```
1. ROL / CONTEXTO     → quién eres y para qué sirve la tarea
2. INSTRUCCIÓN        → qué quieres, en pasos si hace falta
3. CONTEXTO/DATOS     → documentos o información (¡arriba si son largos!)
4. EJEMPLOS           → 1-5 ejemplos del formato deseado (sección 3.1)
5. FORMATO DE SALIDA  → cómo quieres exactamente la respuesta
6. LA PREGUNTA        → al final, sobre todo con documentos largos
```

El orden no es arbitrario: combina lo que vimos sobre *context rot* (datos largos arriba,
pregunta al final) con la lógica de dar primero el marco y luego la tarea concreta.

> **En resumen:** un buen prompt no es largo ni rebuscado. Es **claro, específico, estructurado
> y honesto sobre lo que quieres.** Iterar sobre el prompt es más eficaz que buscar la "frase
> mágica" o saltar de modelo en modelo.

---

## 3. Estrategias de estructuración

Tres técnicas elevan la fiabilidad de las respuestas de forma medible. Se pueden usar solas o
combinadas.

### 3.1 Few-shot: enseñar con ejemplos

El **few-shot prompting** (también *multishot*) consiste en incluir un puñado de ejemplos de
entrada → salida dentro del prompt. Mostrar el patrón es más fiable que describirlo con
palabras: el modelo infiere el formato, el tono y los criterios de tus ejemplos y los replica.

```
Clasifica el sentimiento de cada reseña como POSITIVO, NEUTRO o NEGATIVO.

<ejemplos>
  <ejemplo>Reseña: "Llegó tarde pero el producto está bien." → NEUTRO</ejemplo>
  <ejemplo>Reseña: "Una maravilla, lo recomiendo a todos." → POSITIVO</ejemplo>
  <ejemplo>Reseña: "Se rompió a la semana, pésima calidad." → NEGATIVO</ejemplo>
</ejemplos>

Reseña: "Cumple lo que promete, sin más." →
```

Para que los ejemplos funcionen, deben ser:

- **Relevantes:** que reflejen de cerca tu caso real.
- **Diversos:** que cubran casos límite y varíen lo suficiente para que el modelo no agarre un
  patrón no deseado (p. ej., que todos los ejemplos positivos sean largos y deduzca que
  "largo = positivo").
- **Consistentes:** todos con el mismo formato exacto de salida, porque ese formato es justo lo
  que va a imitar.
- **Estructurados:** envueltos en etiquetas `<ejemplo>` (varios en `<ejemplos>`) para que los
  distinga de las instrucciones.

> **Recomendación:** entre **3 y 5 ejemplos** suele ser el punto óptimo. Few-shot brilla en
> tareas de **clasificación, extracción y formato estricto** (JSON, YAML, plantillas). Su
> límite: cada ejemplo gasta tokens, y ejemplos mal elegidos *sesgan* la salida en lugar de
> mejorarla.

---

### 3.2 Chain-of-thought: pedir que razone en pasos

El **chain-of-thought** (CoT, "cadena de pensamiento") consiste en pedirle al modelo que muestre
su razonamiento paso a paso *antes* de dar la respuesta final. La base técnica es lo que vimos
en el Módulo 1: el modelo genera texto token a token condicionándose a lo ya escrito. Si le
dejas escribir los pasos intermedios, esos pasos pasan a formar parte del contexto sobre el que
construye la respuesta final, y la calidad sube de forma medible en tareas de razonamiento.

```
Forma simple (zero-shot CoT):
  "...resuelve el problema. Piensa paso a paso antes de dar la respuesta final."

Forma estructurada (separando razonamiento y respuesta):
  "Razona dentro de <razonamiento> </razonamiento> y luego da la respuesta
   final dentro de <respuesta> </respuesta>."
```

La forma estructurada tiene una ventaja práctica doble: puedes **leer el razonamiento** para
ver dónde falló si la respuesta es mala, y **extraer solo la respuesta** de forma limpia para
un sistema automatizado.

> **Matices importantes:**
> - Para razonamiento, el **zero-shot CoT** ("piensa paso a paso") a menudo supera al few-shot,
>   porque el modelo genera su propia lógica sin quedar atado a ejemplos que quizá no
>   representan bien tu caso.
> - Los modelos actuales tienen un **modo de "pensamiento" (thinking) adaptativo** que hace esto
>   internamente cuando la tarea lo amerita. Los llamados *reasoning models* lo llevan al
>   extremo. En interfaces modernas no siempre hace falta pedir CoT a mano; sí ayuda saber que
>   existe y por qué funciona.
> - El razonamiento que el modelo muestra es **útil pero no es una auditoría literal** de su
>   cómputo interno: léelo como una explicación plausible, no como una traza exacta.
> - Pídele que **se autoverifique** al final: *"Antes de terminar, comprueba tu respuesta contra
>   [criterio]."* Esto atrapa errores de forma fiable, sobre todo en código y matemática.

---

### 3.3 XML tagging: estructurar el prompt

Las **etiquetas XML** (`<instrucciones>`, `<contexto>`, `<ejemplo>`, `<documento>`) delimitan
sin ambigüedad las distintas partes de un prompt complejo: qué son instrucciones, qué son datos,
qué son ejemplos. Sin esa separación, el modelo puede confundir un fragmento de un documento con
una orden tuya, o viceversa. Los modelos Claude en particular fueron entrenados prestando
atención especial a esta estructura.

```
<instrucciones>
  Resume el informe en 3 viñetas para un comité ejecutivo.
</instrucciones>

<documento>
  {{aquí va el texto largo del informe}}
</documento>

<formato>
  Tres viñetas, máximo 20 palabras cada una, sin jerga técnica.
</formato>
```

Buenas prácticas:

- Usa nombres de etiqueta **consistentes y descriptivos** en todos tus prompts.
- **Anida** cuando haya jerarquía natural (varios documentos dentro de `<documentos>`, cada uno
  en `<documento index="n">`), lo que además ayuda a citar por índice.
- No hay etiquetas "oficiales" obligatorias: lo que importa es que sean claras y coherentes.
- Combínalas con la regla de *context rot*: la etiqueta del documento largo, arriba; la de la
  pregunta, al final.

---

### 3.4 Combinarlas: el patrón completo

Las tres técnicas se potencian juntas. Un prompt robusto típico usa XML para estructurar,
few-shot para fijar el formato y CoT para el razonamiento:

```
<instrucciones>
  Eres un analista de soporte. Clasifica cada ticket por urgencia (ALTA/MEDIA/BAJA)
  y justifica brevemente.
</instrucciones>

<ejemplos>
  <ejemplo>
    Ticket: "No puedo entrar y tengo una demo con un cliente en 10 minutos."
    <razonamiento>Bloqueo total + límite de tiempo inmediato.</razonamiento>
    <respuesta>ALTA</respuesta>
  </ejemplo>
</ejemplos>

<ticket>
  "Sería bueno poder exportar a Excel algún día."
</ticket>

Razona dentro de <razonamiento> y da el veredicto en <respuesta>.
```

> **En resumen:** XML organiza, few-shot muestra el patrón, CoT da espacio para razonar. Empieza
> simple; añade estructura solo cuando la respuesta no salga bien a la primera. Sobre-estructurar
> un prompt sencillo gasta tokens sin mejorar nada.

---

## 4. Una tarea vs. varias: cuándo dividir

Una de las decisiones más prácticas del día a día: ¿meto todo en un solo prompt, o lo parto en
pasos?

### 4.1 Señales de que un prompt hace demasiado

Recuerda del Módulo 1: cuantas más restricciones simultáneas impones, más probable es que el
modelo cumpla unas y "olvide" otras. Señales de que un prompt está sobrecargado:

- Pide **varias cosas de naturaleza distinta** a la vez (investigar **y** redactar **y**
  formatear **y** traducir).
- El resultado cumple unas instrucciones e ignora otras, de forma inconsistente entre intentos.
- Necesitas **inspeccionar un paso intermedio** antes de seguir.
- El prompt se ha vuelto tan largo que ya no sabes qué parte está fallando.

Cuando una sola petición mezcla objetivos distintos, algo casi siempre se pierde. Separar los
objetivos —pedir uno, revisar el resultado, y solo entonces pedir el siguiente— produce mejores
resultados y, sobre todo, te deja ver *dónde* falla.

---

### 4.2 Prompt chaining: encadenar pasos

El **prompt chaining** descompone una tarea en una secuencia de pasos, donde la salida de uno es
la entrada del siguiente. Cada paso es más simple, más fiable y más fácil de depurar, porque el
modelo se concentra en una sola cosa a la vez.

El patrón más común y útil es la **autocorrección**:

```
  ┌──────────┐      ┌──────────────┐      ┌────────────┐
  │ 1. DRAFT │ ───▶ │ 2. REVISIÓN  │ ───▶ │ 3. REFINAR │
  │ genera   │      │ critícalo    │      │ aplica la  │
  │ borrador │      │ contra       │      │ crítica    │
  └──────────┘      │ criterios    │      └────────────┘
                    └──────────────┘
```

- **Paso 1 — Draft:** "Escribe un primer borrador del correo a clientes."
- **Paso 2 — Revisión:** "Revisa este borrador. ¿Es claro? ¿Tono adecuado? Lista 3 mejoras
  concretas."
- **Paso 3 — Refinar:** "Reescribe el correo aplicando esas mejoras."

Otras formas de descomposición útiles:

| Patrón | Idea | Ejemplo |
|--------|------|---------|
| **Encadenado (chaining)** | Pasos fijos en secuencia | Extraer → resumir → traducir |
| **Paralelo** | Subtareas independientes a la vez | Analizar 5 documentos por separado y luego unir |
| **Enrutado (routing)** | Clasificar primero y derivar al prompt adecuado | Detectar el tipo de ticket → enviarlo a su plantilla |
| **Borrador → revisión → refinamiento** | Autocorrección | (el ejemplo de arriba) |

> **Ventaja oculta del chaining:** puedes **ver y corregir cada paso**. Si el resumen salió mal,
> lo arreglas ahí, sin rehacer toda la cadena. Es depuración aplicada a prompts. Este flujo
> iterativo es el corazón del Módulo 4.

---

### 4.3 Cuándo conviene todo en un solo prompt

Dividir no siempre es mejor: cada paso extra cuesta tokens, latencia y complejidad, y puede
propagar errores de un eslabón al siguiente. Conviene un solo prompt cuando:

- La tarea es **cohesiva** y cabe sin sobrecargar (resumir un texto, responder una pregunta,
  reformatear datos).
- No necesitas inspeccionar pasos intermedios.
- El modelo ya la resuelve bien a la primera.

| Situación | Mejor enfoque |
|-----------|---------------|
| Resumir un documento | Un solo prompt |
| Extraer datos a JSON | Un solo prompt (con few-shot) |
| Investigar, redactar y maquetar un informe | Encadenar pasos |
| Tarea donde necesitas validar un paso intermedio | Encadenar pasos |
| Procesar 50 elementos independientes | Paralelo (uno por uno o por lotes) |
| Razonamiento complejo de varios pasos | Un prompt con CoT / thinking |

> **Regla práctica:** empieza con **un solo prompt bien escrito**. Solo divide cuando veas que
> el modelo se atraganta, cuando necesites inspeccionar un paso, o cuando una parte falle de
> forma repetida. No optimices la complejidad antes de necesitarla.

---

## 5. Evaluar si una respuesta es buena

Generar es la mitad fácil. La habilidad que separa a un usuario novato de uno experto es **saber
juzgar la respuesta** — no solo si suena bien.

### 5.1 "Suena bien" no es "es correcto"

Los modelos producen texto fluido, seguro y bien estructurado **incluso cuando se equivocan**.
Esa fluidez es la trampa: el cerebro asocia confianza y buena redacción con veracidad, y el
modelo es excelente en ambas por diseño (es lo que vimos sobre alucinaciones y RLHF en el
Módulo 1). La forma de la respuesta no es evidencia de su fondo: hay que verificar lo que dice,
no cómo lo dice.

> **Cuidado con la adulación (*sycophancy*).** Los modelos tienden a estar de acuerdo contigo y a
> reforzar lo que pareces querer oír. Si preguntas "¿verdad que esto está bien?", es más probable
> que diga que sí. Pregunta en neutro: *"Encuentra los problemas de esto"* en vez de *"¿está bien
> esto?"*. Cómo formulas la pregunta condiciona la respuesta tanto como el contenido.

---

### 5.2 Los cinco criterios

En lugar de un juicio global ("me gusta / no me gusta"), evalúa por criterios concretos. Cinco
bastan para la mayoría de los casos:

| Criterio | Pregunta de control |
|----------|---------------------|
| **Correctitud** | ¿Los hechos, datos y afirmaciones son verdaderos y verificables? |
| **Completitud** | ¿Cubre todo lo que pedí, o se dejó partes en el tintero? |
| **Coherencia** | ¿El razonamiento se sostiene? ¿Hay saltos lógicos o contradicciones? |
| **Fidelidad a la fuente** | Si le di un documento, ¿la respuesta se basa en él o se lo inventó? |
| **Formato y utilidad** | ¿Cumple el formato pedido? ¿Me sirve tal cual o tengo que rehacerlo? |

> **Por qué criterio a criterio (no global):** un puntaje global ("7/10") esconde *qué* falló.
> Evaluar por criterios te dice exactamente dónde está el problema — y qué hacer: si es de
> correctitud, vas a verificar; si es de formato, ajustas el prompt; si es de completitud, pides
> lo que faltó.

---

### 5.3 Rúbricas y el modelo como juez

Cuando evalúas muchas respuestas (o quieres consistencia), formaliza los criterios en una
**rúbrica**: una lista explícita de qué hace que una respuesta sea buena.

- **Rúbrica holística:** un solo puntaje global. Rápida pero opaca: no dice *por qué*.
- **Rúbrica analítica:** un puntaje por criterio. Más trabajo, pero muestra exactamente qué
  capacidad mejoró o empeoró entre versiones. **Es la recomendada.**

**El modelo como juez (*LLM-as-judge*).** Puedes usar un modelo para evaluar la salida de otro
(o de sí mismo) contra una rúbrica. Es muy útil para revisar a escala, con tres cautelas:

- Dale **criterios específicos**, no "¿está bien?". Pídele puntaje **por criterio**.
- Tiene sesgos conocidos: tiende a premiar respuestas largas, bien formateadas y a preferir las
  generadas por su propia familia de modelos. Úsalo como **primer filtro**, no como veredicto
  final en lo que de verdad importa.
- Para tareas serias, ancla el juez con un **conjunto de referencia** (*golden set*): casos con
  la respuesta correcta ya validada por un humano, contra los que mides si el juez —y el modelo—
  aciertan.

```
Eres un evaluador estricto. Califica la RESPUESTA contra estos criterios,
de 1 a 5 cada uno, con una frase de justificación:
- Correctitud   - Completitud   - Coherencia   - Fidelidad a la fuente

<fuente>{{documento original}}</fuente>
<respuesta>{{la respuesta a evaluar}}</respuesta>
```

Cuando trabajas con prompts que vas a reutilizar mucho, esta evaluación deja de ser manual y se
vuelve un *eval*: un pequeño banco de casos que corres cada vez que cambias el prompt o el modelo,
para detectar regresiones. Es la versión "test automatizado" del prompt engineering.

---

### 5.4 Checklist práctico de revisión

Una rutina de 30 segundos antes de dar por buena una respuesta:

- [ ] **¿Hay datos específicos** (fechas, cifras, nombres, citas)? → Verifícalos por fuera.
- [ ] **¿Le di una fuente?** → ¿La respuesta se sostiene en ella o inventó cosas?
- [ ] **¿Pedí varias cosas?** → ¿Cumplió todas, o se saltó alguna?
- [ ] **¿El razonamiento se sostiene** leído paso a paso, no solo la conclusión?
- [ ] **¿Estoy preguntando en neutro**, o le di pistas de lo que quería oír?
- [ ] **¿La estoy aceptando porque es correcta, o porque suena bien y estoy cansado?**

> **Principio clave (enlaza con el Módulo 1):** el modelo es un colaborador capaz, no un oráculo.
> Tu valor no está en generar — el modelo genera más rápido que tú — sino en **dirigir y
> verificar**. La evaluación es donde pones ese valor.

---

## 6. Glosario del Módulo

| Término | Definición breve |
|---------|-----------------|
| **Ventana de contexto** | Cantidad máxima de tokens que el modelo procesa de una vez; incluye instrucciones, historial, documentos y respuesta |
| **System prompt** | Instrucción persistente que define el rol y comportamiento del modelo durante toda la conversación |
| **Context rot** | Degradación de la calidad de la respuesta a medida que crece el contexto, aunque el dato relevante siga presente |
| **Lost in the middle** | Tendencia del modelo a prestar menos atención a la información ubicada en el centro del contexto que en los extremos |
| **Prompt caching** | Reutilizar partes estables del contexto entre llamadas para reducir costo y latencia |
| **Prompt engineering** | Oficio de redactar instrucciones que producen buenas respuestas de forma fiable |
| **Few-shot / multishot** | Incluir varios ejemplos de entrada→salida en el prompt para fijar formato y estilo |
| **Zero-shot** | Pedir la tarea sin ejemplos, solo con la instrucción |
| **Chain-of-thought (CoT)** | Pedir al modelo que muestre su razonamiento paso a paso antes de la respuesta final |
| **Thinking / reasoning models** | Modelos o modos que razonan internamente más tiempo cuando la tarea lo amerita |
| **XML tagging** | Usar etiquetas (`<contexto>`, `<ejemplo>`…) para separar las partes de un prompt sin ambigüedad |
| **Structured output** | Modo que obliga a la salida a cumplir un esquema (p. ej. JSON válido) |
| **Prompt chaining** | Descomponer una tarea en pasos secuenciales, donde la salida de uno alimenta al siguiente |
| **Routing** | Clasificar la entrada primero y derivarla al prompt o modelo adecuado |
| **Autocorrección** | Patrón de chaining: generar borrador → revisar contra criterios → refinar |
| **Rúbrica** | Lista explícita de criterios para evaluar la calidad de una respuesta |
| **LLM-as-judge** | Usar un modelo para evaluar la salida de otro modelo contra una rúbrica |
| **Golden set / eval** | Conjunto de casos con respuesta validada para medir calidad y detectar regresiones |
| **Sycophancy** | Tendencia del modelo a estar de acuerdo con el usuario y reforzar lo que parece querer oír |

---

## 7. Práctica guiada (segunda hora)

> Estos ejercicios están pensados para hacerse en vivo con el modelo abierto. El objetivo no es
> "acertar", sino **observar la diferencia** que hacen las técnicas. Tras cada uno, comparte el
> resultado y recibe retroalimentación.

### Ejercicio 1 — Antes y después (claridad) · 10 min
Toma una tarea real tuya (redactar un correo, generar un script, resumir un documento).
1. Escribe el prompt "como lo harías normalmente" y guarda la respuesta.
2. Reescríbelo aplicando 2.1–2.4: rol, instrucción específica, el "por qué" y formato.
3. Compara. **Pregunta de reflexión:** ¿qué cambió y por qué?

### Ejercicio 2 — Few-shot en acción · 10 min
Pide una clasificación o extracción (p. ej., clasificar 5 frases por sentimiento).
1. Primero **sin ejemplos**.
2. Luego con **3 ejemplos** bien estructurados en etiquetas.
3. Observa la consistencia del formato entre ambos.

### Ejercicio 3 — El poder de "piensa paso a paso" · 10 min
Dale un problema de razonamiento con varios pasos (un acertijo lógico o un cálculo con
condiciones).
1. Pídele **solo la respuesta**.
2. Pídele que **razone en `<razonamiento>` y responda en `<respuesta>`**.
3. ¿Cambió la respuesta? ¿Puedes ver dónde se equivocaría si fallara?

### Ejercicio 4 — Encadenar: borrador → crítica → refinamiento · 15 min
Elige algo a redactar (un mensaje difícil, una descripción de producto).
1. Genera el borrador.
2. En el **mismo chat**, pide: "Critica este borrador y lista 3 mejoras concretas."
3. Pide: "Reescríbelo aplicando esas mejoras."
4. **Reflexión:** ¿el resultado encadenado es mejor que pedirlo todo de una vez?

### Ejercicio 5 — Caza de errores (evaluación) · 15 min
Pídele un dato verificable sobre un tema de nicho (una fecha, una cifra, una cita).
1. Aplica el **checklist 5.4**: ¿es específico? ¿lo puedes verificar?
2. Verifica el dato por fuera.
3. Vuelve a preguntar **en neutro**: "Encuentra los problemas o imprecisiones de tu respuesta
   anterior." Observa si se autocorrige o se adula.

> **Cierre de la práctica:** ¿qué técnica vas a incorporar a tu trabajo desde mañana?

---

## 8. Preguntas de repaso

Estas preguntas consolidan los conceptos antes de pasar al Módulo 3. No buscan una respuesta "de
examen": el objetivo es razonar en voz alta.

1. Tienes un PDF de 100 páginas y una pregunta concreta sobre algo que está en la página 60.
   ¿Cómo estructurarías el prompt para maximizar la probabilidad de una buena respuesta, sabiendo
   lo que sabes sobre *context rot* y *lost in the middle*?

2. Un compañero dice: "uso siempre la ventana de contexto más grande posible para que el modelo
   tenga toda la información". ¿Qué le responderías, y qué diferencia hay entre la ventana
   anunciada y la efectiva?

3. ¿Cuándo usarías **few-shot** y cuándo **chain-of-thought**? Da un ejemplo de tarea para cada
   uno donde la otra técnica sería peor opción.

4. Te piden automatizar la redacción de respuestas a reseñas de clientes. ¿Lo harías en un solo
   prompt o encadenado? Justifica con los criterios de la sección 4.

5. El modelo te entrega una respuesta impecablemente redactada y segura. Enumera tres cosas que
   harías antes de confiar en ella para un entregable importante.

6. Explícale a alguien sin contexto técnico por qué "el modelo no recuerda" lo que le dijiste
   hace media hora en otro chat, aunque "parezca" que tiene memoria.

7. Vas a reutilizar el mismo prompt cientos de veces en producción. ¿Cómo montarías un *eval*
   para saber si un cambio de prompt o de modelo lo mejora o lo empeora?

---

## 9. Recursos extra

Recursos seleccionados para profundizar. Los oficiales de Anthropic son la referencia primaria;
el resto aporta evidencia o perspectivas complementarias.

**Documentación oficial (referencia primaria)**
- [Prompting best practices — Claude Docs](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices) — la guía canónica: claridad, ejemplos, XML, thinking, contexto largo.
- [Building Effective AI Agents — Anthropic](https://www.anthropic.com/research/building-effective-agents) — patrones de descomposición: prompt chaining, paralelización, orquestador-trabajadores.
- [Use examples (multishot prompting) — Claude Docs](https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/multishot-prompting) — cómo elegir y estructurar ejemplos.

**Ventana de contexto y context rot**
- [Context Rot: How Increasing Input Tokens Impacts LLM Performance — Chroma (2025)](https://research.trychroma.com/context-rot) — estudio de 18 modelos; la evidencia clave de que más contexto degrada el rendimiento.
- ["Lost in the Middle: How Language Models Use Long Contexts" — Liu et al. (paper original)](https://arxiv.org/abs/2307.03172) — el trabajo fundacional sobre la curva en U.
- [Context Rot — guía explicativa (Morph)](https://www.morphllm.com/context-rot) — resumen accesible del fenómeno y mitigaciones.

**Estructuración: few-shot, CoT, XML**
- [Zero-Shot vs Few-Shot prompting: guía con ejemplos — Vellum](https://www.vellum.ai/blog/zero-shot-vs-few-shot-prompting-a-guide-with-examples)
- [Chain of Thought Prompting (CoT): todo lo que necesitas saber — Vellum](https://www.vellum.ai/blog/chain-of-thought-prompting-cot-everything-you-need-to-know)
- [Prompt engineering across OpenAI, Anthropic & Gemini — Steve Kinney](https://stevekinney.com/writing/prompt-engineering-frontier-llms) — comparativa práctica entre proveedores.

**Evaluación de respuestas**
- [LLM-as-a-Judge: la guía completa — Confident AI](https://www.confident-ai.com/blog/why-llm-as-a-judge-is-the-best-llm-evaluation-method)
- [Rúbricas analíticas vs. LLM-as-a-Judge — A. Masood](https://medium.com/@adnanmasood/rubric-based-evals-llm-as-a-judge-methodologies-and-empirical-validation-in-domain-context-71936b989e80)

---

*Anterior: [Módulo 1 — Cómo piensan los modelos](./modulo-1-wiki.md)*
*Siguiente: Módulo 3 — Interfaz y ecosistema*

---

> Versión 2.0 — Módulo 2 de 7 | Curso: Fundamentos de IA Productiva
> Actualizado: junio 2026
