# Módulo 1 — Cómo Piensan los Modelos
### Fundamentos de IA Productiva
---

## Tabla de Contenidos

1. [¿Qué es un LLM y cómo genera texto?](#1-qué-es-un-llm-y-cómo-genera-texto)
   - 1.1 [Qué es un LLM](#11-qué-es-un-llm)
   - 1.2 [Tokens: la unidad mínima de trabajo](#12-tokens-la-unidad-mínima-de-trabajo)
   - 1.3 [El proceso de generación paso a paso](#13-el-proceso-de-generación-paso-a-paso)
   - 1.4 [Qué hay dentro: la arquitectura Transformer](#14-qué-hay-dentro-la-arquitectura-transformer)
2. [Probabilidad, sampling y alucinaciones](#2-probabilidad-sampling-y-alucinaciones)
   - 2.1 [Temperatura y los controles de sampling](#21-temperatura-y-los-controles-de-sampling)
   - 2.2 [Por qué los modelos inventan cosas](#22-por-qué-los-modelos-inventan-cosas)
   - 2.3 [Tipos de alucinación y cómo reconocerlas](#23-tipos-de-alucinación-y-cómo-reconocerlas)
   - 2.4 [Cómo reducir las alucinaciones](#24-cómo-reducir-las-alucinaciones)
3. [Fortalezas reales y fallos sistemáticos](#3-fortalezas-reales-y-fallos-sistemáticos)
   - 3.1 [Lo que los modelos hacen excepcionalmente bien](#31-lo-que-los-modelos-hacen-excepcionalmente-bien)
   - 3.2 [Dónde fallan de forma predecible](#32-dónde-fallan-de-forma-predecible)
   - 3.3 [La regla práctica](#33-la-regla-práctica)
4. [Qué diferencia a los modelos entre sí](#4-qué-diferencia-a-los-modelos-entre-sí)
   - 4.1 [Tamaño: parámetros y lo que significan](#41-tamaño-parámetros-y-lo-que-significan)
   - 4.2 [Entrenamiento base (pretraining)](#42-entrenamiento-base-pretraining)
   - 4.3 [Fine-tuning: especialización post-entrenamiento](#43-fine-tuning-especialización-post-entrenamiento)
   - 4.4 [RLHF: alinear con preferencias humanas](#44-rlhf-alinear-con-preferencias-humanas)
   - 4.5 [Otros ejes de diferenciación](#45-otros-ejes-de-diferenciación)
   - 4.6 [Tabla comparativa de modelos actuales](#46-tabla-comparativa-de-modelos-actuales)
5. [Cómo leer un benchmark](#5-cómo-leer-un-benchmark)
   - 5.1 [Qué mide y qué no mide un benchmark](#51-qué-mide-y-qué-no-mide-un-benchmark)
   - 5.2 [Benchmarks comunes y su utilidad real](#52-benchmarks-comunes-y-su-utilidad-real)
   - 5.3 [La prueba definitiva: tu caso de uso](#53-la-prueba-definitiva-tu-caso-de-uso)
6. [Glosario del Módulo](#6-glosario-del-módulo)
7. [Preguntas de repaso](#7-preguntas-de-repaso)
8. [Recursos extra](#8-recursos-extra)

---

## 1. ¿Qué es un LLM y cómo genera texto?

### 1.1 Qué es un LLM

Un **LLM** (Large Language Model, modelo de lenguaje grande) es una red neuronal
entrenada sobre cantidades enormes de texto — libros, artículos, código, conversaciones —
con un único objetivo durante el entrenamiento: **predecir el siguiente fragmento de texto**
dado todo lo anterior. No memoriza las páginas que leyó. Lo que ajusta son millones o
miles de millones de valores numéricos internos llamados **pesos**, que codifican los
patrones estadísticos del lenguaje: qué palabras tienden a seguir a cuáles, qué estructuras
gramaticales son válidas, qué hechos co-ocurren, qué tono corresponde a qué contexto.

Cuando le escribes algo, el modelo no consulta una base de datos ni ejecuta reglas escritas
por humanos. Pasa tu texto por esa red de pesos y obtiene una **distribución de
probabilidad** sobre cuál debería ser el siguiente fragmento. De ahí elige uno, lo añade a
lo que ya hay, y repite. Esa es toda la mecánica: un predictor de "lo que viene a
continuación", aplicado una y otra vez.

Tres consecuencias importantes se derivan directamente de esto y conviene tenerlas claras
desde el principio:

- **El modelo no distingue entre "saber" y "sonar correcto".** Genera lo más probable, no
  lo más verdadero. Cuando ambos coinciden, acierta; cuando no, inventa con la misma
  fluidez (esto es la base de las alucinaciones, sección 2).
- **No tiene estado entre llamadas.** Cada vez que respondes en un chat, se le reenvía toda
  la conversación desde el inicio. Lo que parece "memoria" es el historial viajando
  completo en cada turno (se detalla en el Módulo 2).
- **Genera texto genuinamente nuevo.** A diferencia del autocompletado del teléfono — que
  solo mira las últimas palabras — el LLM mantiene coherencia con todo el contexto previo y
  puede producir combinaciones que nunca aparecieron en sus datos. No "copia": recombina
  patrones.

> **En resumen:** un LLM predice el texto más probable dado todo el contexto, usando
> patrones estadísticos aprendidos de una cantidad masiva de texto humano. No es una base
> de datos de hechos ni un motor de reglas: es un motor de predicción.

---

### 1.2 Tokens: la unidad mínima de trabajo

Un LLM no procesa letras ni palabras completas, sino **tokens**: fragmentos de texto que
pueden ser una palabra entera, parte de una palabra, un signo de puntuación o incluso un
espacio. El proceso que parte el texto en tokens se llama **tokenización**, y lo realiza un
*tokenizer* específico de cada familia de modelos.

```
Texto:  "La inteligencia artificial es fascinante"
Tokens: ["La", " intelig", "encia", " artific", "ial", " es", " fascinante"]
Cantidad: 7 tokens  (aproximado, varía según el tokenizer)
```

Los tokenizers modernos (como *Byte-Pair Encoding*, BPE) construyen su vocabulario de forma
estadística: las secuencias de caracteres más frecuentes se vuelven un solo token; las
raras se parten en varios. Por eso una palabra común en inglés suele ser 1 token, mientras
que una palabra técnica, un nombre propio o una palabra en español con tildes puede partirse
en 3 o 4.

El impacto del idioma se ve con un ejemplo (conteos aproximados, varían por modelo):

```
"The cat is sleeping"      →  4 tokens   (cada palabra ≈ 1 token)
"El gato está durmiendo"   →  ~7 tokens  ("El", " g", "ato", " está", " durm", "iendo", ...)
"otorrinolaringólogo"      →  1 palabra, pero ~6 tokens
"🙂"                        →  varios tokens (los emojis se parten en bytes)
```

La misma frase consume más tokens en español que en inglés: eso significa **más costo y
menos espacio efectivo** en la ventana de contexto para el mismo contenido. Puedes
comprobarlo pegando tu propio texto en un tokenizer interactivo (ver *Recursos extra*).

**¿Por qué importa saber esto?**

- **Costo.** Las plataformas cobran por token, tanto de lo que envías (*input*) como de lo
  que el modelo genera (*output*). Una regla de bolsillo útil para inglés: ~1 token ≈ 4
  caracteres ≈ ¾ de palabra. **El español suele consumir más tokens por palabra** que el
  inglés, porque está peor representado en el vocabulario de muchos tokenizers — un detalle
  con impacto real en costo y en el límite de contexto.
- **Límite de contexto.** Existe un máximo de tokens por interacción (la *ventana de
  contexto*, Módulo 2). Se mide en tokens, no en palabras ni mensajes.
- **Errores "tontos" explicados.** Que el modelo cuente mal las letras de una palabra, falle
  en rimas o se confunda con anagramas se explica por la tokenización: nunca ve
  "inteligencia" como una secuencia de letras, la ve como los trozos `intelig`+`encia`. No
  tiene acceso directo a los caracteres.

---

### 1.3 El proceso de generación paso a paso

La generación es **autoregresiva**: el modelo produce un token a la vez, y cada token nuevo
se añade al contexto para predecir el siguiente. No planea la respuesta entera y luego la
escribe; la construye token a token, de izquierda a derecha, sin volver atrás a corregir lo
ya emitido.

```
Paso 1:  Entrada →  "El cielo es de color"
         El modelo calcula probabilidades para todos los tokens posibles:
         P("azul")  = 0.45
         P("gris")  = 0.18
         P("rojo")  = 0.12
         P("verde") = 0.08
         ... (decenas de miles de opciones más)

Paso 2:  Se elige "azul" (según la estrategia de sampling, ver 2.1)
         Contexto nuevo → "El cielo es de color azul"

Paso 3:  Se recalculan probabilidades para el siguiente token
         P(".") = 0.35   P("y") = 0.20   P(",") = 0.15  ...

Paso 4:  Eventualmente se emite el token especial de fin de secuencia → se detiene
```

Dos consecuencias prácticas de que la generación sea autoregresiva:

- **El "streaming" que ves es real.** El texto aparece palabra a palabra porque se genera
  literalmente así. No es un efecto visual.
- **El razonamiento "en voz alta" mejora los resultados.** Como cada token se condiciona a
  los anteriores, dejar que el modelo escriba pasos intermedios antes de la respuesta final
  le da más contexto sobre el cual condicionar — esa es la base técnica de *chain-of-thought*
  (Módulo 2). El modelo, en efecto, "piensa escribiendo".

---

### 1.4 Qué hay dentro: la arquitectura Transformer

No hacen falta matemáticas para entender la arquitectura a nivel funcional. Todos los LLMs
modernos se basan en el **Transformer** (introducido en el paper *"Attention Is All You
Need"*, 2017). Sus piezas clave:

**Embeddings.** Antes de procesarse, cada token se convierte en un **vector** — una lista de
cientos o miles de números — que lo ubica en un "espacio de significado". Tokens con
significados o usos parecidos quedan cerca en ese espacio. Esta representación numérica es
lo que permite al modelo operar matemáticamente con el lenguaje, y es la base de cosas como
la búsqueda semántica.

**Mecanismo de atención (self-attention).** Al predecir el siguiente token, el modelo puede
"mirar" todos los tokens anteriores y asignar más peso a los relevantes para lo que está
construyendo ahora. Si una frase solo cobra sentido por algo dicho mucho antes, la atención
es el mecanismo que conecta ambos puntos. Es lo que da coherencia a largo alcance y lo que
distingue a un Transformer del viejo autocompletado.

**Capas apiladas.** El modelo tiene muchas capas (decenas a más de cien). De forma
intuitiva: las capas iniciales detectan patrones superficiales (qué tokens suelen ir
juntos), y las profundas capturan relaciones abstractas (quién hace qué a quién, intención,
tono, estructura argumental). La salida final vuelve a convertirse en una distribución de
probabilidad sobre el vocabulario.

**Una limitación inherente: el costo de la atención.** La self-attention compara cada token
con todos los demás, así que su costo crece *cuadráticamente* con la longitud del contexto.
Por eso procesar contextos muy largos es caro y lento, y por eso existe tanta investigación
en hacer la atención más eficiente. Tenlo presente: contexto largo no es gratis.

> **Lo importante para un usuario:** el modelo no "entiende" como un humano. Manipula
> representaciones vectoriales y relaciones estadísticas entre tokens. Que de ahí salgan
> resultados aparentemente comprensivos es real y útil, pero el mecanismo subyacente sigue
> siendo predicción estadística, no comprensión consciente.

---

## 2. Probabilidad, sampling y alucinaciones

### 2.1 Temperatura y los controles de sampling

En el paso 2 de la generación, el modelo tiene una distribución de probabilidad y debe
**elegir** un token. Cómo elige se controla con los parámetros de *sampling*. El más conocido
es la **temperatura**, que escala la distribución antes de muestrear:

```
Distribución de probabilidades para el siguiente token:
  "azul"   → 45%      "verde"  →  8%
  "gris"   → 18%      "negro"  →  7%
  "rojo"   → 12%      otros    → 10%

Temperatura = 0 (determinista):
  → Elige siempre el token más probable ("azul"). Salida repetible y predecible.

Temperatura ≈ 0.7 (el rango habitual por defecto):
  → Suele elegir "azul", pero a veces "gris" o "rojo". Equilibrio entre fiabilidad y variedad.

Temperatura ≈ 1.5 (alta):
  → La distribución se "aplana": opciones poco probables ganan chance. Salida creativa
    pero más propensa a incoherencias.
```

La temperatura **no controla la inteligencia ni la veracidad**, solo cuánta aleatoriedad se
inyecta. Conviene conocer otros dos controles que suelen acompañarla:

- **Top-p (nucleus sampling).** En lugar de considerar todo el vocabulario, restringe la
  elección al conjunto más pequeño de tokens cuya probabilidad acumulada llega a *p* (p. ej.
  0.9). Descarta la cola de opciones absurdas manteniendo variedad razonable.
- **Top-k.** Limita la elección a los *k* tokens más probables.

Para tareas que exigen precisión y reproducibilidad (código, extracción de datos, cálculos)
se usa temperatura baja. Para tareas creativas (lluvia de ideas, redacción libre) se sube.
En interfaces como claude.ai estos valores están preconfigurados por la plataforma según el
contexto, así que rara vez los tocas a mano; entender qué hacen explica por qué la misma
pregunta puede dar respuestas distintas en dos intentos.

---

### 2.2 Por qué los modelos inventan cosas

Las **alucinaciones** son respuestas que suenan plausibles y se expresan con confianza, pero
son incorrectas, inventadas o falsas. Es el problema más importante que un usuario nuevo debe
interiorizar, y no es un "bug" que se vaya a arreglar del todo: es consecuencia directa de
cómo funciona el modelo.

**La causa técnica.** El modelo genera el token más probable dado el contexto; no tiene un
mecanismo para consultar hechos verificados ni para distinguir "lo sé" de "no lo sé". Si la
pregunta toca un hecho poco representado en sus datos de entrenamiento, no se detiene a
admitir ignorancia: produce el texto que *estadísticamente parece* una respuesta correcta
para esa forma de pregunta.

```
Pregunta: "¿Cuál fue el resultado del partido entre Copiapó y O'Higgins
           el 14 de marzo de 2019?"

El modelo no tiene ese dato concreto.
Pero sí conoce la forma de un resultado de fútbol: "X ganó Y-Z en el Estadio W".
Genera: "Copiapó ganó 2-1 en el Estadio Municipal."
→ Completamente inventado, presentado con total seguridad.
```

El mismo mecanismo produce el caso más traicionero para el trabajo profesional, la
**cita inventada**:

```
Pregunta: "Dame una referencia académica que respalde esta afirmación."

El modelo conoce la FORMA de una cita (autor, año, título plausible, revista real),
pero no tiene la referencia exacta.
Genera: "Pérez & Soto (2019), 'Efectos del gramaje en la durabilidad del libro',
         Revista Iberoamericana de Artes Gráficas, 12(3), 45-58."
→ El formato es impecable; el paper no existe.
```

A esto se suma un factor de diseño: el ajuste por preferencias humanas (RLHF, sección 4.4)
premia las respuestas útiles y completas, lo que empuja al modelo a *responder* en lugar de
abstenerse. Por eso un modelo tiende a llenar huecos antes que a decir "no tengo ese dato",
salvo que esté explícitamente entrenado o instruido para reconocer sus límites.

> **Hallazgo reciente (OpenAI, 2025).** El estudio *"Why Language Models Hallucinate"*
> sostiene que las alucinaciones no son un misterio, sino el resultado predecible de cómo se
> entrena y evalúa a los modelos: la mayoría de los *benchmarks* premian **adivinar** por
> encima de **admitir incertidumbre**. Como en un examen tipo test donde dejar una pregunta
> en blanco puntúa igual que fallarla, al modelo le "conviene" arriesgar una respuesta antes
> que decir "no sé". Mientras la evaluación recompense el acierto y castigue la duda, los
> modelos seguirán inventando con seguridad (ver *Recursos extra*).

---

### 2.3 Tipos de alucinación y cómo reconocerlas

| Tipo | Descripción | Ejemplo |
|------|-------------|---------|
| **Factual** | Inventa datos concretos: fechas, cifras, nombres | "La empresa fue fundada en 1987" (dato falso pero preciso) |
| **Citación** | Inventa referencias que no existen | Papers con título y autores plausibles pero inexistentes |
| **Confabulación** | Mezcla hechos reales con inventados de forma coherente | Biografía de una persona real con eventos ficticios intercalados |
| **Razonamiento** | Pasos intermedios incorrectos en una deducción | Resultado correcto llegado por camino equivocado, o viceversa |
| **Recencia** | Datos desactualizados presentados como actuales | "El CEO de la empresa es [nombre de hace 3 años]" |
| **De instrucción** | Afirma haber hecho algo que no hizo | "He revisado todo el documento" cuando solo procesó una parte |

**Señales de alerta:**

- El modelo da datos muy específicos (cifras exactas, fechas, nombres propios) sobre un tema
  oscuro o poco documentado.
- Responde con la misma seguridad sobre algo que sabes con certeza y sobre algo que no puedes
  verificar — la confianza del texto no correlaciona con su exactitud.
- Cita fuentes que no le pediste, o aporta URLs y referencias demasiado convenientes.
- Da detalles que no podría conocer (eventos posteriores a su fecha de corte, datos privados).

---

### 2.4 Cómo reducir las alucinaciones

No se eliminan, pero se reducen mucho con técnicas concretas. Conviene conocerlas desde ya,
aunque varias se profundizan en el Módulo 2:

- **Dar el contexto en el prompt (grounding).** Si la respuesta debe basarse en un documento,
  pégalo en el prompt y pide explícitamente que se ciña a él. El modelo alucina mucho menos
  cuando razona sobre material que tiene delante que cuando tira de "memoria" de
  entrenamiento.
- **RAG (Retrieval-Augmented Generation).** Patrón en el que un sistema busca primero
  fragmentos relevantes en una base de conocimiento y los inyecta en el contexto antes de
  generar. Es la forma estándar de anclar un modelo a información actualizada y verificable
  (se ve en módulos posteriores).
- **Pedir citas y "no sé".** Instruir: *"responde solo con lo que esté en el documento; si no
  está, di que no aparece"* reduce drásticamente la invención.
- **Bajar la temperatura** en tareas factuales.
- **Usar herramientas.** Para cálculos, fechas o búsquedas, dejar que el modelo ejecute
  código o consulte la web es más fiable que confiar en su texto.
- **Verificar lo verificable.** Para cualquier dato específico que vaya a un entregable
  importante, confírmalo por fuera. Es la red de seguridad definitiva.

> **Regla práctica:** cuanto más específico y verificable sea el dato, más vale confirmarlo.
> Para razonamiento general, síntesis y transformación de texto la tasa de error es baja;
> para hechos puntuales y recientes, siempre verifica.

---

## 3. Fortalezas reales y fallos sistemáticos

### 3.1 Lo que los modelos hacen excepcionalmente bien

**Síntesis y comprensión de texto.** Dado un documento largo, extraer puntos clave, resumir
o responder preguntas sobre su contenido. Los modelos actuales son extraordinariamente
buenos en esto, incluso con material muy técnico — siempre que el texto esté en el contexto.

**Transformación de formato.** Convertir texto no estructurado a JSON, Markdown, XML o CSV;
reformatear tablas; extraer campos de texto libre. Muy fiable y de enorme ahorro de tiempo.

**Generación de código.** Para los lenguajes populares, generan código funcional con alta
frecuencia: el modelo procesó millones de repositorios durante el entrenamiento. Funciona
especialmente bien para *boilerplate*, traducción entre lenguajes y explicación de código
ajeno.

**Reescritura y adaptación de tono.** Llevar un texto técnico a lenguaje accesible o
viceversa, pasar de formal a conversacional, ajustar longitud. Calidad muy alta.

**Razonamiento sobre el contexto dado.** Si le das reglas, procedimientos o datos y pides que
razone sobre ellos ("dado este contrato, ¿qué cláusula aplica a…?"), funciona muy bien. La
clave es que la respuesta esté *contenida* en lo que le diste.

**Generación de variantes.** Proponer 5 alternativas para un nombre, reescribir un párrafo de
tres formas, generar casos de prueba. La capacidad de producir variaciones a demanda es muy
valiosa en el trabajo diario.

**Traducción y trabajo multilingüe.** Calidad alta entre idiomas con buena representación,
incluyendo traducción que preserva tono y matiz mejor que los traductores clásicos.

---

### 3.2 Dónde fallan de forma predecible

**Matemática y cálculo exacto.** El modelo no calcula: predice el texto que parece el
resultado de un cálculo. Con números pequeños a veces acierta; con números grandes o varios
pasos, la probabilidad de error sube mucho.

```
¿Cuánto es 17 × 83 + 44?   → puede acertar, pero no porque calculó: lo predijo.
¿Cuánto es 7931 × 6847?    → aquí el riesgo de error crece notablemente.
```

> **Solución:** para cálculos, usa la ejecución de código o una calculadora integrada en vez
> de confiar en la respuesta en texto.

**Conteo y operaciones carácter a carácter.** "¿Cuántas veces aparece la letra 'a'?" es
sorprendentemente difícil, porque el modelo procesa tokens, no caracteres (sección 1.2).

**Conocimiento reciente o muy específico.** Todo lo posterior a la fecha de corte del modelo
es invisible para él salvo que use búsqueda web. Para eventos poco documentados, la calidad
cae y el riesgo de alucinación sube.

**Instrucciones con muchas condiciones simultáneas.** Cuantas más restricciones impones en un
solo prompt, más probable es que cumpla unas y "olvide" otras. (En el Módulo 2 veremos cuándo
conviene dividir la tarea.)

**Coherencia y recuperación en contextos muy largos.** Aunque las ventanas actuales son
grandes, la atención a partes lejanas se degrada: los detalles del centro de un documento
largo pueden "diluirse" (es el *context rot* / *lost in the middle* del Módulo 2).

**Autoconciencia de sus límites.** El modelo no sabe de forma fiable qué sabe y qué no, ni
cuántos tokens le quedan, ni si una herramienta falló. No te fíes de sus afirmaciones sobre
su propio estado.

---

### 3.3 La regla práctica

Una heurística para decidir cuánto confiar en una respuesta:

| Si la tarea requiere... | Confianza recomendada |
|------------------------|----------------------|
| Síntesis de texto provisto | Alta |
| Generación de código (lenguaje popular) | Alta con revisión |
| Razonamiento sobre reglas explícitas dadas | Alta |
| Hechos históricos bien documentados | Media |
| Hechos específicos recientes | Baja — verificar |
| Cálculo numérico exacto | Baja — usar código |
| Conteo de caracteres o elementos | Muy baja — verificar siempre |
| Eventos oscuros o poco documentados | Muy baja — alta probabilidad de alucinación |

> **Principio clave:** el modelo es un colaborador muy capaz, no un oráculo. Trata sus
> respuestas como un borrador inteligente, no como fuente de verdad. Tu rol es dar dirección
> y verificar lo que importa.

---

## 4. Qué diferencia a los modelos entre sí

### 4.1 Tamaño: parámetros y lo que significan

Los modelos se describen por su número de **parámetros** — los valores numéricos ajustados
durante el entrenamiento que definen su comportamiento. Se expresan en miles de millones:
7B, 70B, 405B. A grandes rasgos, más parámetros dan más **capacidad** para representar
relaciones complejas del lenguaje, pero la relación no es lineal ni garantiza más "inteligencia".

Matices que importan en la práctica:

- **Más grande = más caro y más lento.** Más parámetros exigen más memoria y cómputo, lo que
  encarece cada respuesta y aumenta la latencia.
- **Calidad del entrenamiento > tamaño bruto.** Un modelo pequeño entrenado con buenos datos
  y técnica puede superar a uno grande entrenado descuidadamente. La cantidad y calidad de
  los datos de entrenamiento pesa tanto como el número de parámetros.
- **Mixture of Experts (MoE).** Muchos modelos grandes modernos no activan todos sus
  parámetros en cada token: tienen "expertos" especializados y enrutan cada token solo a unos
  pocos. Así un modelo puede tener cientos de miles de millones de parámetros *totales* pero
  activar solo una fracción por token, ganando calidad sin pagar todo el costo de cómputo.
- **Cuantización.** Reducir la precisión numérica de los pesos (de 16 a 8 o 4 bits) achica el
  modelo y lo acelera con una pérdida de calidad pequeña. Es lo que permite correr modelos
  potentes en hardware modesto.

Para la mayoría de usos cotidianos, un modelo de gama media es más que suficiente y
notablemente más económico que el más grande.

---

### 4.2 Entrenamiento base (pretraining)

El **pretraining** es la fase más costosa y lenta. Se expone al modelo a un corpus gigantesco
y se le entrena a predecir el siguiente token una y otra vez, miles de millones de veces,
ajustando los pesos en cada paso para reducir el error de predicción.

```
Un paso de pretraining (simplificado):

1. Texto del corpus: "La fotosíntesis convierte luz solar en [energía]"
2. El modelo predice el siguiente token → p. ej. "calor"
3. Se compara con el token real ("energía") y se mide el error
4. Se ajustan los pesos (descenso de gradiente) para reducir ese error
5. Se repite miles de millones de veces con textos distintos
```

Al terminar el pretraining el modelo "sabe" muchísimo sobre el mundo y el lenguaje, pero
**todavía no es útil como asistente**: solo sabe continuar texto. Si le escribes una
pregunta, es tan probable que la responda como que genere *otra* pregunta parecida, porque en
su corpus las preguntas a menudo van seguidas de más preguntas. Convertirlo en un asistente
que sigue instrucciones requiere las fases siguientes.

Conviene saber también que el corpus determina los **sesgos** y los **vacíos** del modelo:
está mejor en los idiomas y dominios sobrerrepresentados en internet, y peor en los demás.
Y todo lo posterior a su **fecha de corte** simplemente no está.

---

### 4.3 Fine-tuning: especialización post-entrenamiento

El **fine-tuning** (ajuste fino) es un entrenamiento adicional, mucho más pequeño y barato,
que parte del modelo base ya entrenado y ajusta su comportamiento sin rehacerlo desde cero.

**Tipos comunes:**

- **Instruction tuning.** Se entrena con muchos ejemplos del formato instrucción → respuesta.
  Es lo que transforma un "continuador de texto" en un "asistente que responde y obedece
  instrucciones". Es el salto cualitativo que hace usable a un modelo.
- **Domain fine-tuning.** Entrenamiento con textos de un dominio (legal, médico, financiero)
  para afinar vocabulario, formato y patrones de ese campo.
- **Format fine-tuning.** Enseñar a responder siempre en una estructura concreta (JSON
  estricto, un esquema de etiquetas, un estilo de la empresa).

**Una técnica clave: LoRA / adaptadores.** En vez de reajustar todos los pesos (caro), se
entrenan pequeñas matrices adicionales que "corrigen" el comportamiento. Permite especializar
un modelo grande con poco cómputo y mantener muchas variantes ligeras del mismo base.

Límite importante: **el fine-tuning no crea conocimiento de la nada.** Si el modelo base no
vio un dominio, ajustar no lo inventa; refuerza patrones existentes y ajusta comportamiento y
formato. Para *añadir* conocimiento nuevo y verificable, lo apropiado suele ser RAG (sección
2.4), no fine-tuning.

---

### 4.4 RLHF: alinear con preferencias humanas

**RLHF** (Reinforcement Learning from Human Feedback) es la técnica que hace que los modelos
sean útiles, seguros y alineados con lo que las personas prefieren. Es lo que convierte un
modelo que "técnicamente responde" en uno que responde *bien*, declina peticiones
problemáticas y tiene un "carácter" reconocible.

El proceso, en tres pasos:

1. **Recopilar preferencias humanas.** Se generan varias respuestas a la misma pregunta y
   evaluadores humanos indican cuál prefieren. Se construye un dataset de comparaciones.
2. **Entrenar un modelo de recompensa (*reward model*).** Con esas comparaciones se entrena
   un modelo auxiliar que aprende a predecir qué respuesta gustará más a un humano. Actúa como
   juez automático escalable.
3. **Ajustar el LLM con ese juez.** Mediante aprendizaje por refuerzo, se ajustan los pesos
   del LLM para maximizar la puntuación del reward model, en un ciclo iterativo.

Variantes y matices que vale la pena conocer:

- **DPO (Direct Preference Optimization)** y métodos afines logran un efecto similar de forma
  más directa y barata, sin entrenar un reward model separado. Muchos modelos recientes los
  usan.
- **RLAIF / Constitutional AI.** En lugar de (o además de) humanos, se usan principios
  escritos y feedback generado por IA para alinear el modelo. Es el enfoque que Anthropic usa
  con Claude para guiar su comportamiento con una "constitución" de principios.

**Por qué le importa al usuario:** RLHF explica por qué distintos modelos tienen
personalidades y "valores" distintos (cada empresa usa sus propios datos y criterios), por qué
a veces el modelo es excesivamente cauto o excesivamente complaciente (*sycophancy*, Módulo
2), y por qué tiende a responder antes que a abstenerse.

---

### 4.5 Otros ejes de diferenciación

Más allá de tamaño y entrenamiento, al comparar modelos conviene mirar:

- **Longitud de la ventana de contexto.** De ~8k a más de 1M de tokens según el modelo.
  Determina cuánto material puedes darle de una vez (Módulo 2).
- **Modalidades.** Solo texto, o también imagen, audio y vídeo (modelos *multimodales*).
- **Latencia y throughput.** Qué tan rápido responde y cuántas peticiones soporta; crítico
  para aplicaciones en producción.
- **Capacidad de razonamiento extendido (*thinking*).** Algunos modelos pueden "pensar" más
  tiempo antes de responder, mejorando tareas complejas a cambio de latencia y costo.
- **Uso de herramientas / *function calling*.** Qué tan bien sabe llamar a funciones, buscar
  en la web o ejecutar código.
- **Abierto vs. cerrado.** Modelos con pesos abiertos (Llama, DeepSeek, Qwen) que puedes
  desplegar tú mismo, frente a modelos propietarios accesibles solo por API. Afecta
  privacidad, control y costo.
- **Precio por token** de entrada y de salida, que puede variar en órdenes de magnitud.

---

### 4.6 Tabla comparativa de modelos actuales

| Modelo | Empresa | Puntos fuertes | Cuándo usarlo |
|--------|---------|----------------|---------------|
| **Claude Opus 4** | Anthropic | Razonamiento profundo, análisis largo, escritura | Tareas complejas, flujos de trabajo autónomos |
| **Claude Sonnet 4** | Anthropic | Equilibrio calidad/costo, velocidad | Uso cotidiano, código, análisis |
| **Claude Haiku** | Anthropic | Velocidad, bajo costo | Tareas simples, alto volumen |
| **GPT-4o** | OpenAI | Multimodal sólido, ecosistema amplio | Cuando se necesita visión integrada |
| **o3 / o4-mini** | OpenAI | Razonamiento matemático y científico | Problemas de lógica y matemática |
| **Gemini 2.5 Pro** | Google | Contexto muy largo, multimodal | Análisis de documentos masivos |
| **Llama 3.x** | Meta | Pesos abiertos, desplegable localmente | Privacidad, control total, sin costo de API |
| **DeepSeek R1** | DeepSeek | Razonamiento, pesos abiertos | Alternativa económica para razonamiento |

> **Nota:** el panorama cambia cada pocos meses. Un modelo que es el mejor en enero puede ser
> el tercero en abril. La comparación por benchmarks sirve como punto de partida, pero la
> prueba en tu caso de uso concreto es siempre más informativa (sección 5.3).

---

## 5. Cómo leer un benchmark

### 5.1 Qué mide y qué no mide un benchmark

Un **benchmark** es un conjunto de pruebas estandarizadas con respuestas conocidas, diseñado
para medir el rendimiento de un modelo en condiciones controladas y comparables. Es útil,
pero mide *exactamente lo que mide*, ni más ni menos — un puntaje alto en un benchmark no
garantiza buen desempeño en tu trabajo real.

**Qué sí mide un benchmark bien diseñado:**
- Rendimiento en ese tipo específico de preguntas, en ese momento.
- Comparación relativa entre modelos bajo condiciones iguales.
- Progreso de un modelo entre versiones.

**Qué no mide:**
- Rendimiento en *tu* tarea específica.
- Calidad sostenida en conversaciones largas.
- Fiabilidad en dominios muy especializados o en español.
- Latencia, costo y experiencia de uso real.

**Una trampa frecuente: la contaminación de datos.** Si las preguntas del benchmark (o muy
parecidas) aparecieron en el corpus de entrenamiento, el modelo puede "acertar" recordándolas
en vez de razonando. Esto infla puntajes y es difícil de detectar desde fuera. Por eso los
benchmarks más valiosos se renuevan o se mantienen privados.

---

### 5.2 Benchmarks comunes y su utilidad real

| Benchmark | Qué mide | Utilidad práctica |
|-----------|----------|-------------------|
| **MMLU** | Conocimiento general en 57 dominios | Media — indica amplitud de conocimiento |
| **HumanEval / SWE-bench** | Generación de código, resolución de bugs reales | Alta para quienes programan |
| **MATH / AIME** | Problemas matemáticos de competencia | Alta si necesitas razonamiento matemático |
| **GPQA** | Preguntas de nivel PhD en ciencias | Indica razonamiento profundo; poco relevante para uso cotidiano |
| **MT-Bench** | Conversación multi-turno, seguir instrucciones | Media — mide bien la capacidad de asistente |
| **Arena (LMSYS)** | Preferencias humanas en conversación libre | Alta — refleja satisfacción de usuarios reales |

**El problema del "benchmark hacking".** Hay evidencia de que los laboratorios optimizan sus
modelos para los benchmarks públicos más conocidos, inflando los resultados. Un modelo con
92% en MMLU no es necesariamente mejor para redactar propuestas comerciales que uno con 88%.
Mira la *tendencia* y el *conjunto* de benchmarks, no un único número de titular.

---

### 5.3 La prueba definitiva: tu caso de uso

La forma más fiable de elegir un modelo es construir un pequeño test personal: toma 5-10
tareas reales que necesitas hacer habitualmente, ejecútalas en los 2-3 modelos candidatos y
evalúa:

1. ¿Cuál resuelve mejor el problema sin instrucciones adicionales?
2. ¿Cuál produce el formato que necesitas?
3. ¿Cuál comete menos errores en tu dominio y en tu idioma?
4. ¿Cuál es más conveniente en velocidad y costo para tu volumen?

Este proceso toma una hora y vale más que cualquier tabla de benchmarks. Guárdalo: te servirá
de "evaluación casera" cada vez que salga un modelo nuevo.

---

## 6. Glosario del Módulo

| Término | Definición breve |
|---------|-----------------|
| **LLM** (Large Language Model) | Modelo de lenguaje entrenado sobre grandes cantidades de texto para predecir el siguiente token |
| **Token** | Fragmento de texto que el modelo procesa como unidad mínima; puede ser una palabra, parte de una palabra o un símbolo |
| **Tokenización** | Proceso de partir el texto en tokens; lo realiza un *tokenizer* propio de cada familia de modelos |
| **Embedding** | Representación de un token como vector numérico que codifica su significado y uso |
| **Parámetros** | Valores numéricos ajustables que definen el comportamiento del modelo; se miden en miles de millones |
| **Transformer** | Arquitectura de red neuronal base de todos los LLMs modernos, introducida en 2017 |
| **Atención (Attention)** | Mecanismo que permite relacionar partes lejanas del texto al predecir el siguiente token |
| **Autoregresivo** | Generación en la que cada token producido depende de todos los anteriores |
| **Temperatura** | Parámetro de sampling que controla la aleatoriedad de la elección de tokens |
| **Top-p / Top-k** | Estrategias de sampling que restringen las opciones a las más probables |
| **Alucinación** | Respuesta incorrecta o inventada presentada con confianza |
| **RAG** | Retrieval-Augmented Generation: recuperar información relevante y añadirla al contexto antes de generar |
| **Pretraining** | Fase de entrenamiento masivo inicial sobre un corpus gigantesco |
| **Fine-tuning** | Entrenamiento adicional sobre datos específicos para especializar comportamiento o formato |
| **LoRA / adaptadores** | Técnica de fine-tuning eficiente que entrena pequeñas matrices en vez de todos los pesos |
| **RLHF** | Reinforcement Learning from Human Feedback; alinea el modelo con preferencias humanas |
| **Reward model** | Modelo auxiliar que predice qué respuestas prefieren los humanos; guía el RLHF |
| **MoE (Mixture of Experts)** | Arquitectura que activa solo una fracción de los parámetros por token |
| **Cuantización** | Reducir la precisión numérica de los pesos para achicar y acelerar el modelo |
| **Fecha de corte** | Momento hasta el cual el modelo tiene conocimiento de su corpus de entrenamiento |
| **Benchmark** | Suite de pruebas estandarizadas para medir y comparar el rendimiento de modelos |
| **Corpus** | El conjunto de textos usado para entrenar un modelo |
| **Ventana de contexto** | Cantidad máxima de tokens que un modelo procesa en una sola interacción (se detalla en Módulo 2) |

---

## 7. Preguntas de repaso

Estas preguntas sirven para consolidar los conceptos antes de pasar al Módulo 2. No hay una
respuesta "de examen": el objetivo es razonar en voz alta.

1. Si un modelo responde con una fecha exacta sobre un evento histórico menor, ¿qué deberías
   hacer antes de usar esa fecha en un documento importante, y por qué la confianza del texto
   no te sirve como señal?

2. Tienes que elegir entre un modelo de 7B que corre localmente en tu servidor y uno de 70B
   accesible por API. ¿Qué preguntas harías —sobre privacidad, costo, latencia y calidad—
   antes de decidir cuál usar para clasificar correos de clientes?

3. Explica por qué el fine-tuning no es la herramienta adecuada para que un modelo "aprenda"
   los datos internos y actualizados de tu empresa. ¿Qué usarías en su lugar?

4. Un proveedor te muestra que su modelo tiene el puntaje más alto en MMLU. ¿Qué dos preguntas
   le harías —una sobre relevancia y otra sobre contaminación de datos— para saber si eso
   importa en tu caso?

5. Explícale a alguien sin contexto técnico por qué un LLM puede generar texto que nunca
   existió antes, aunque no tenga creatividad ni comprensión "reales".

6. ¿Por qué un cambio de temperatura no arregla una alucinación factual? ¿Qué sí ayudaría?

---

## 8. Recursos extra

Recursos seleccionados para profundizar en los conceptos del módulo. Empieza por los
explicadores visuales si el tema es nuevo; los papers y la documentación oficial son la
referencia primaria.

**Cómo funcionan los modelos (explicadores visuales)**
- [3Blue1Brown — Neural networks (serie, incl. "But what is a GPT?")](https://www.3blue1brown.com/topics/neural-networks) — la mejor intuición visual de qué es un Transformer y la atención, sin perderse en matemáticas.
- [The Illustrated Transformer — Jay Alammar](https://jalammar.github.io/illustrated-transformer/) — el clásico que desglosa la arquitectura pieza por pieza con diagramas.
- [Andrej Karpathy — canal de YouTube](https://www.youtube.com/@AndrejKarpathy) — sus charlas *"Intro to Large Language Models"* y *"Deep Dive into LLMs like ChatGPT"* explican de fábrica a uso todo el ciclo (pretraining → fine-tuning → RLHF).
- [Transformer Explainer (interactivo)](https://poloclub.github.io/transformer-explainer/) — visualiza en vivo cómo un modelo GPT genera el siguiente token.

**Tokens (pruébalo tú mismo)**
- [OpenAI Tokenizer](https://platform.openai.com/tokenizer) — pega texto y mira cómo se parte en tokens y cuántos son.
- [Tiktokenizer](https://tiktokenizer.vercel.app/) — lo mismo pero comparando varios tokenizers/modelos lado a lado.

**Alucinaciones**
- [Why Language Models Hallucinate — OpenAI (2025)](https://openai.com/index/why-language-models-hallucinate/) — por qué entrenar y evaluar premiando el acierto produce invención; la explicación detrás del recuadro de la sección 2.2. ([paper en arXiv](https://arxiv.org/abs/2509.04664))

**Arquitectura, entrenamiento y alineación**
- [Attention Is All You Need (2017)](https://arxiv.org/abs/1706.03762) — el paper original que introdujo el Transformer.
- [Illustrating Reinforcement Learning from Human Feedback (RLHF) — Hugging Face](https://huggingface.co/blog/rlhf) — los tres pasos del RLHF explicados con diagramas.
- [Constitutional AI: Harmlessness from AI Feedback — Anthropic](https://www.anthropic.com/research/constitutional-ai-harmlessness-from-ai-feedback) — cómo Claude se alinea con una "constitución" de principios en vez de solo feedback humano.

**Comparar modelos y benchmarks**
- [LMArena / Chatbot Arena](https://lmarena.ai/) — ranking por votación humana a ciegas entre pares de modelos (Elo). Refleja preferencia real de uso.
- [Artificial Analysis](https://artificialanalysis.ai/) — compara modelos por calidad, velocidad y **precio por token** en un solo lugar; ideal para decidir según costo.
- [Stanford HELM](https://crfm.stanford.edu/helm/) — evaluación holística y transparente de modelos en muchas dimensiones.

---

*Siguiente: [Módulo 2 — Trabajar con el modelo](./modulo-2-wiki.md)*

---

> Versión 2.1 — Módulo 1 de 7 | Curso: Fundamentos de IA Productiva
> Actualizado: junio 2026
