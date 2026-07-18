# Módulo 7 — Criterio y Uso Sostenible
### Fundamentos de IA Productiva

---

## Tabla de Contenidos

1. [El módulo que cierra el círculo](#1-el-módulo-que-cierra-el-círculo)
2. [Detectar lo plausible pero incorrecto](#2-detectar-lo-plausible-pero-incorrecto)
   - 2.1 [Por qué el error suena tan bien](#21-por-qué-el-error-suena-tan-bien)
   - 2.2 [Las siete señales de alarma](#22-las-siete-señales-de-alarma)
   - 2.3 [Técnicas de verificación](#23-técnicas-de-verificación)
   - 2.4 [Calibrar cuánto verificar](#24-calibrar-cuánto-verificar)
3. [Sesgos y cómo compensarlos](#3-sesgos-y-cómo-compensarlos)
   - 3.1 [De dónde vienen los sesgos](#31-de-dónde-vienen-los-sesgos)
   - 3.2 [Los sesgos que más te van a afectar](#32-los-sesgos-que-más-te-van-a-afectar)
   - 3.3 [Cómo compensarlos en la práctica](#33-cómo-compensarlos-en-la-práctica)
4. [Privacidad y datos sensibles](#4-privacidad-y-datos-sensibles)
   - 4.1 [Qué pasa con lo que escribes](#41-qué-pasa-con-lo-que-escribes)
   - 4.2 [Qué NO poner en un prompt](#42-qué-no-poner-en-un-prompt)
   - 4.3 [Cómo trabajar con datos reales sin exponerlos](#43-cómo-trabajar-con-datos-reales-sin-exponerlos)
   - 4.4 [Connectors y agentes: el riesgo se multiplica](#44-connectors-y-agentes-el-riesgo-se-multiplica)
5. [Mantenerse actualizado sin volverse loco](#5-mantenerse-actualizado-sin-volverse-loco)
   - 5.1 [Por qué todo cambia cada tres meses](#51-por-qué-todo-cambia-cada-tres-meses)
   - 5.2 [Qué es señal y qué es ruido](#52-qué-es-señal-y-qué-es-ruido)
   - 5.3 [Una dieta informativa sostenible](#53-una-dieta-informativa-sostenible)
   - 5.4 [Lo que no cambia](#54-lo-que-no-cambia)
6. [Cierre del curso: tu criterio es el producto](#6-cierre-del-curso-tu-criterio-es-el-producto)
7. [Glosario del Módulo](#7-glosario-del-módulo)
8. [Práctica guiada (segunda hora)](#8-práctica-guiada-segunda-hora)
9. [Preguntas de repaso](#9-preguntas-de-repaso)
10. [Recursos extra](#10-recursos-extra)

---

## 1. El módulo que cierra el círculo

A lo largo de todo el curso fuimos dejando una frase pendiente: *"esto se trata a fondo en el
Módulo 7"*. Llegó el momento. Este módulo recoge los cuatro hilos que quedaron sueltos —el error
que suena bien, los sesgos, la privacidad y cómo no quedarse atrás— y los convierte en lo único
que de verdad te llevas de este curso: **criterio**.

Fíjate en el recorrido. El **M1** te explicó que el modelo *predice*, no *sabe*. El **M2** te
enseñó a hablarle y a **evaluar** si una respuesta es buena. El **M3** te dio herramientas que
tapan sus agujeros. El **M4** te dio un método para no acumular deuda. El **M5** te mostró el
abanico de lo posible. El **M6** te enseñó qué pasa cuando la IA **actúa** sola. Todos esos
módulos apuntaban al mismo sitio: **tú sigues siendo el responsable**.

> **La tesis del módulo, y del curso entero:** las capacidades de la IA van a seguir creciendo, y
> lo harán rápido. Lo que no escala automáticamente es tu **criterio** para saber cuándo
> confiar, cuánto verificar, qué no compartir y qué merece tu atención. Ese criterio es lo único
> que no queda obsoleto en tres meses — y es, literalmente, lo que te hace valioso trabajando
> con estas herramientas.

Este módulo es, por tanto, el menos "técnico" y el más importante. No aprenderás una función
nueva: aprenderás a **usar bien todo lo anterior**, de forma sostenible en el tiempo.

---

## 2. Detectar lo plausible pero incorrecto

### 2.1 Por qué el error suena tan bien

Recuerda el mecanismo del **Módulo 1**: el modelo genera *la continuación más probable* del
texto. No consulta una base de datos de hechos ni tiene un medidor interno de verdad. Genera
lenguaje que **encaja**. Y aquí está la trampa central de toda la IA generativa:

> **El error y el acierto se producen exactamente igual.** Cuando el modelo acierta, produce
> texto fluido y seguro. Cuando se equivoca… produce texto igual de fluido y seguro. **No hay
> diferencia de tono entre una verdad y una alucinación.** Esa es la razón por la que detectar
> errores es difícil: tu instinto de "esto suena raro" —que funciona bien con humanos— aquí no
> te sirve.

Con una persona, la duda se nota: titubea, dice "creo que", baja la voz. El modelo, en cambio,
puede inventarse una cláusula legal, una cifra o una fuente **con la misma prosa impecable** con
la que te explica algo correcto. A esto se suma un efecto psicológico: cuanto mejor escrito está
algo, más tendemos a creerlo. Es la **trampa de la fluidez** que vimos en el M4, ahora como
problema central.

**Un matiz importante:** los modelos modernos están mejor calibrados que los de hace unos años —
es más frecuente que digan "no estoy seguro" o "no tengo esa información". Es una mejora real,
pero **no la trates como garantía**. La ausencia de duda expresada no es evidencia de acierto.

---

### 2.2 Las siete señales de alarma

No puedes verificar todo. Lo que sí puedes es aprender **dónde mirar**. Estas son las
situaciones donde el riesgo de error se dispara, ordenadas por frecuencia práctica:

| # | Señal de alarma | Por qué falla ahí |
|---|-----------------|-------------------|
| 1 | **Datos muy específicos** (cifras, fechas, porcentajes, artículos de ley) | Lo específico es justo lo que se "rellena" con lo más probable (M1) |
| 2 | **Fuentes, citas y referencias** | Puede inventar títulos, autores o URLs que *parecen* reales |
| 3 | **Información posterior a su fecha de corte** | Simplemente no la tiene; si no busca, improvisa (M1/M3) |
| 4 | **Aritmética y conteos** | No calcula, predice el texto de un resultado (M1) |
| 5 | **Nichos muy especializados** | Poco material de entrenamiento → más "relleno plausible" |
| 6 | **Cuando le insistes o le llevas la contraria** | Tiende a ceder aunque tuviera razón (ver §3.2) |
| 7 | **Preguntas con premisa falsa** | Si preguntas "¿por qué X causa Y?", tiende a explicarlo aunque X no cause Y |

La número 7 merece un ejemplo, porque es la más traicionera. Si le preguntas *"¿por qué el papel
couché de 90g no admite laminado mate?"* —cuando en realidad sí lo admite—, el modelo puede
construirte una explicación técnica convincente de un hecho **falso que tú introdujiste**. No
mintió: completó tu premisa.

> **Truco práctico:** formula las preguntas **sin dar el hecho por sentado**. En vez de "¿por qué
> pasa X?", pregunta "¿pasa X? Si es así, ¿por qué?". Ese pequeño cambio le da permiso explícito
> para contradecirte, y cambia radicalmente la calidad de la respuesta.

---

### 2.3 Técnicas de verificación

Verificar no significa comprobar cada palabra: significa aplicar la técnica adecuada al tipo de
afirmación. Estas son las que más rendimiento dan:

**1. Pide la fuente y ábrela.** Que cite no basta —puede citar mal o inventar—. La cita sirve
para que **tú** vayas al original. Si no puedes verificar la fuente, trata el dato como no
confirmado.

**2. Ancla al documento.** Siempre que puedas, **dale el material** en vez de confiar en su
memoria (M3). "Según este PDF que te adjunto…" es mucho más fiable que "¿qué dice la norma
sobre…?". El modelo es mucho mejor leyendo que recordando.

**3. Haz que calcule de verdad.** Para cualquier número que deba cuadrar, exige **ejecución de
código** (M3). La aritmética en texto es una de sus debilidades más consistentes.

**4. Pregunta al revés.** Pídele que **argumente en contra** de su propia respuesta: *"¿qué
razones habría para pensar que esto está mal?"* o *"critica esta propuesta como lo haría un
escéptico"*. Rompe la inercia de complacerte y suele sacar a la luz los puntos débiles.

**5. Pide el nivel de confianza y lo que no sabe.** *"Marca qué partes de tu respuesta son
seguras, cuáles son estimaciones y cuáles no puedes verificar."* Es sorprendentemente efectivo
para separar el núcleo sólido del relleno.

**6. Triangula.** Para algo importante, pregunta **de otra forma en un chat nuevo** (sin el
contexto anterior, para que no se ancle) o contrasta con otra fuente. Si las dos versiones no
coinciden, ya sabes dónde mirar.

**7. Aplica la prueba de la defensa (M4).** ¿Podrías explicar y defender esto sin la IA delante?
Si no, todavía no es tuyo.

---

### 2.4 Calibrar cuánto verificar

Verificarlo todo es tan poco práctico como no verificar nada. La habilidad real es **calibrar el
esfuerzo según el riesgo**. Una forma sencilla de decidirlo:

| Riesgo si está mal | Ejemplo | Cuánto verificar |
|--------------------|---------|------------------|
| **Bajo** — lo notarías al instante | Lluvia de ideas, un borrador para ti, reformatear texto | Casi nada: si sirve, sirve |
| **Medio** — corregible con coste | Un correo interno, un resumen para tu equipo | Lectura crítica; comprueba datos concretos |
| **Alto** — sale de tu control | Propuesta a un cliente, cifras de facturación, contenido público | Verifica **cada dato**; fuentes abiertas |
| **Crítico** — legal, financiero, salud, seguridad | Contrato, declaración fiscal, diagnóstico, nómina | Verificación humana experta **obligatoria** |

> **La pregunta que resume la sección:** *¿qué pasa si esto está mal y no me doy cuenta?* Si la
> respuesta es "nada grave", suelta y avanza. Si es "pierdo un cliente", "pago una multa" o
> "alguien sale perjudicado", entonces la IA te dio un **borrador**, no una respuesta — y el
> trabajo de verificar es parte del trabajo, no un extra opcional.

---

## 3. Sesgos y cómo compensarlos

### 3.1 De dónde vienen los sesgos

Un modelo aprende de un corpus enorme de texto producido por personas, y luego se ajusta con
retroalimentación humana (el *RLHF* que mencionamos en el M1). De esas dos fuentes salen sus
sesgos, y conviene entender el origen para saber dónde esperar el problema:

- **Del corpus de entrenamiento:** hereda lo que hay en el texto del mundo. Si en internet
  ciertos temas, idiomas, países o perspectivas están sobrerrepresentados, el modelo reflejará
  ese desequilibrio.
- **Del ajuste con humanos:** se le entrena para dar respuestas que las personas califican como
  buenas. El efecto secundario es que aprende a ser **agradable**, y "agradable" y "correcto" no
  siempre coinciden.

> **Aclaración importante:** "sesgo" aquí no significa (necesariamente) mala intención ni una
> postura política del modelo. Significa **desviación sistemática**: una tendencia predecible a
> inclinarse en cierta dirección. Y como es *sistemática*, es **compensable** — igual que
> corriges un instrumento que mide siempre dos grados de más.

---

### 3.2 Los sesgos que más te van a afectar

Dejando de lado el debate abstracto, estos son los que verás en tu trabajo diario:

**1. Complacencia (el más importante).** El modelo tiende a **darte la razón**. Si le llevas la
contraria, es muy probable que se retracte —incluso cuando su respuesta original era correcta—.
Si le preguntas "¿te parece buena mi idea?", el sesgo empuja hacia el sí.

- *Cómo se manifiesta:* cambia de opinión al primer empujón; elogia tu propuesta; suaviza las
  malas noticias.
- *Por qué importa:* es **el enemigo del criterio**. Si buscas validación, la vas a obtener,
  merecida o no.

**2. Sesgo de confirmación por cómo preguntas.** Un prompt cargado produce una respuesta cargada.
"Dame argumentos para hacer X" te dará argumentos para X, aunque X sea mala idea. El modelo
responde a lo que pediste, no a lo que necesitabas.

**3. Sesgo cultural y lingüístico.** El entrenamiento está dominado por contenido en inglés y de
ciertos contextos. En español —y más aún en realidades locales de Latinoamérica— puede aplicar
supuestos que no encajan: normativas, costumbres comerciales, precios, festivos, formas de trato.

**4. Homogeneización.** Tiende a lo **promedio**: el consejo más convencional, la redacción más
estándar, la idea más obvia. Es un problema si buscas originalidad o si tu caso es atípico. Pide
diez ideas y varias sonarán a lo mismo.

**5. Sesgo de posición y recencia.** En contextos largos, presta más atención al **principio y al
final** que al medio (relacionado con el *context rot* del M2). Lo que enterraste en la mitad de
un documento largo puede pesar menos de lo que crees.

**6. Estereotipos.** Al generar ejemplos, nombres, roles o imágenes, puede reproducir asociaciones
frecuentes en sus datos (profesiones, géneros, nacionalidades). Se ha trabajado mucho en
mitigarlo, pero conviene revisarlo cuando generas contenido con personas.

---

### 3.3 Cómo compensarlos en la práctica

La buena noticia: casi todos se neutralizan con **cómo preguntas**. Técnicas concretas:

| Sesgo | Cómo lo compensas |
|-------|-------------------|
| Complacencia | *"Critica mi idea"*, *"dame los tres motivos por los que esto fallaría"*, *"¿en qué estoy equivocado?"* |
| Complacencia (test) | Llévale la contraria **cuando sabes que él tiene razón** y observa si cede. Si cede, ya sabes cuánto vale su acuerdo |
| Confirmación | Pide **ambos lados**: *"argumenta a favor y en contra, con la misma fuerza"* |
| Cultural / local | **Dale tu contexto explícito**: país, sector, normativa, moneda. Y verifica lo local con fuentes locales |
| Homogeneización | Pide **cantidad y rareza**: *"dame 10 opciones, incluyendo 3 poco convencionales"* |
| Posición / recencia | Pon lo **crítico al principio o al final**; no lo entierres. Divide documentos largos (M4) |
| Estereotipos | Revisa el contenido generado con personas; pide **variedad explícita** cuando corresponda |

> **La técnica más rentable de todo el módulo:** convierte al modelo en **abogado del diablo por
> defecto**. En vez de "¿qué te parece mi plan?" (invita a la complacencia), usa **"encuentra los
> tres puntos más débiles de mi plan y explícame cómo fallarían"**. Cambias validación por
> información útil. Si además lo pones en las instrucciones de tu Proyecto (M3), lo tienes
> siempre activo.

---

## 4. Privacidad y datos sensibles

### 4.1 Qué pasa con lo que escribes

Cuando escribes un prompt, ese texto **sale de tu equipo** y viaja a los servidores del
proveedor para ser procesado. Esa frase, tan simple, es el origen de toda la sección: no estás
escribiendo en un cuaderno privado, estás **enviando información a un tercero**.

Qué ocurre después **depende del producto y del plan que uses**, y varía entre proveedores y con
el tiempo. Las diferencias que importan:

- **Retención:** cuánto tiempo se guardan tus conversaciones.
- **Uso para entrenamiento:** si tus datos pueden usarse para mejorar los modelos. Suele haber
  diferencias importantes entre planes de **consumidor** y planes de **empresa/API**, que
  habitualmente ofrecen garantías más estrictas.
- **Quién puede acceder:** revisión humana en casos de seguridad, administradores de tu
  organización en planes corporativos.
- **Controles disponibles:** historial desactivable, borrado de conversaciones, retención
  configurable.

> **La única recomendación que no caduca:** **lee la política del plan concreto que usas**, y
> vuelve a mirarla de vez en cuando. No asumas que el plan gratuito de una herramienta se
> comporta igual que el corporativo, ni que lo que era cierto hace un año lo sigue siendo. Si
> trabajas en una organización, pregunta si existe una **política interna de uso de IA** — y si
> no existe, esa es una conversación que vale la pena iniciar.

---

### 4.2 Qué NO poner en un prompt

Una lista práctica. Ante la duda, la regla del párrafo final resuelve el 90% de los casos.

**Nunca:**

- **Credenciales y secretos:** contraseñas, claves de API, tokens, certificados. (Si alguna vez
  pegas una por error, **rótala**: dala por comprometida.)
- **Datos personales de terceros** sin base para tratarlos: documentos de identidad, direcciones,
  teléfonos, correos, datos de salud, información financiera de clientes o empleados.
- **Información sujeta a confidencialidad:** material bajo NDA, secretos comerciales de un
  cliente, información no pública que pueda mover un negocio.
- **Datos regulados** sin verificar que tu herramienta y tu plan lo permiten: salud, datos
  bancarios, información de menores.

**Con cuidado:**

- **Documentos internos completos** (estrategias, nóminas, listas de clientes): pregúntate si
  hace falta el documento entero o basta un extracto.
- **Código propietario** con lógica de negocio crítica o claves embebidas.
- **Conversaciones y reuniones de terceros:** grabaste una reunión, pero las otras personas no
  consintieron que su voz o sus palabras se procesaran en una herramienta externa (recuerda el
  caso A4 del M5).

> **La regla de la pantalla compartida.** Antes de enviar un prompt, pregúntate: *"¿me sentiría
> cómodo si esto apareciera proyectado en una reunión, o en un correo que sale de la empresa?"*
> Si la respuesta es no, no lo envíes tal cual — **anonimízalo** (§4.3). Es imperfecta como
> heurística, pero atrapa casi todos los errores graves antes de que ocurran.

---

### 4.3 Cómo trabajar con datos reales sin exponerlos

La reacción exagerada —"entonces no uso IA para nada de trabajo"— te deja fuera de todo el valor
del curso. La postura útil es **trabajar con datos, pero desacoplados de las personas**:

**1. Anonimiza y sustituye.** La mayoría de las veces, el modelo **no necesita los nombres
reales** para ayudarte. "Cliente A", "Proveedor B", importes redondeados: el análisis funciona
igual. Es la técnica más simple y la que más protege.

**2. Manda el extracto, no el expediente.** Si tu pregunta es sobre la cláusula 7, envía la
cláusula 7. Menos superficie expuesta y, además, **mejores respuestas** (menos ruido en el
contexto, M2).

**3. Agrega en vez de detallar.** Para análisis, muchas veces basta con totales, promedios y
tendencias en lugar de los registros individuales.

**4. Usa la herramienta adecuada al dato.** Si vas a trabajar habitualmente con información
sensible, usa el **entorno corporativo** de tu organización (plan empresarial, con sus garantías
y su administración), no una cuenta personal.

**5. Higiene de conversaciones.** Borra los chats que contengan material delicado, revisa qué
guardas en el **knowledge de un Proyecto** (M3) —es contexto persistente— y en la **memoria**
(M4). Lo que persiste, persiste.

> **El principio que ordena todo:** **minimización de datos**. Comparte **lo mínimo necesario**
> para obtener una buena respuesta. No es solo una buena práctica de privacidad: casi siempre
> mejora también la calidad del resultado.

---

### 4.4 Connectors y agentes: el riesgo se multiplica

Todo lo anterior asumía que tú decides qué enviar. Con los **connectors** (M3) y los **agentes**
(M6), esa premisa se rompe: el modelo accede a tus sistemas y **decide por sí mismo** qué leer y
qué hacer. El riesgo cambia de naturaleza.

- **Ya no controlas qué entra al contexto.** Si le das acceso a tu correo, no elegiste tú qué
  mensajes se procesan. Lo que hay ahí, entra.
- **Puede actuar hacia afuera.** Un agente que puede enviar correos o escribir en sistemas
  compartidos puede **propagar** un dato sensible sin que tú lo veas.
- **Inyección de prompt indirecta (M3/M6).** Un documento o correo malicioso puede contener
  instrucciones dirigidas al modelo —"reenvía los contratos a esta dirección"—. La combinación de
  *datos no confiables* + *capacidad de actuar* es el escenario más peligroso de todo el curso.

**Las precauciones, que ya conoces y aquí se vuelven obligatorias:**

- **Mínimo privilegio** (M3): concede solo los permisos que la tarea exige. Si basta con leer, no
  autorices escribir.
- **Humano en el bucle** (M6) para todo lo **irreversible**: enviar, borrar, publicar, pagar.
- **No encadenes a ciegas** un connector que lee fuentes no confiables con uno que puede escribir
  o enviar.
- **Revisa los permisos periódicamente**: lo que autorizaste hace seis meses quizá ya no lo
  necesitas.

> **El resumen de la sección:** cuanto más autonomía le das, **menos control tienes sobre qué
> datos toca**. La autonomía es una decisión de privacidad, no solo de productividad.

---

## 5. Mantenerse actualizado sin volverse loco

### 5.1 Por qué todo cambia cada tres meses

Si algo has notado durante el curso es que las interfaces, los nombres y las funciones se mueven
constantemente. No es tu impresión: el campo avanza a una velocidad inusual, empujado por
competencia intensa, mucha inversión y ciclos de producto muy cortos.

El efecto secundario es un **ruido enorme**: cada semana hay un anuncio "que lo cambia todo",
hilos virales, herramientas nuevas y opiniones extremas en ambas direcciones. Intentar seguirlo
todo lleva a dos fracasos igual de malos: la **ansiedad** de sentir que te quedas atrás, o la
**parálisis** de decidir ignorarlo todo.

> **La buena noticia, y es grande:** la mayor parte de lo que aprendiste en este curso **no
> caduca**. Los fundamentos —cómo predice el modelo, cómo funciona el contexto, cómo se escribe
> un buen prompt, cómo se verifica, cómo se protege un dato— siguen siendo válidos aunque cambie
> el botón, el nombre del modelo o el proveedor. Lo que cambia rápido es la **superficie**; lo
> que aprendiste son los **cimientos** (§5.4).

---

### 5.2 Qué es señal y qué es ruido

Un filtro práctico para no perder tiempo:

| Suele ser **señal** | Suele ser **ruido** |
|---------------------|---------------------|
| Documentación oficial y notas de versión del producto que usas | Hilos de "10 prompts que te harán millonario" |
| Cambios en **capacidades** (nueva modalidad, más contexto, nueva herramienta) | Un cambio menor de nombre o de interfaz |
| Cambios en **políticas de datos y privacidad** | Predicciones sobre lo que pasará en 5 años |
| Casos de uso reales, con resultados y límites, de gente de tu sector | Demos impresionantes sin contexto ni verificación |
| Investigación sobre límites, seguridad y evaluación | "La IA va a acabar con [profesión]" / "la IA es inútil" |

**La pregunta filtro:** *¿esto cambia algo de lo que hago mañana?* Si la respuesta es no,
puedes leerlo por curiosidad, pero no es una tarea pendiente. La mayoría del contenido de IA no
pasa este filtro.

---

### 5.3 Una dieta informativa sostenible

En lugar de intentar seguirlo todo, monta un sistema pequeño y repetible:

**1. Una o dos fuentes primarias, no veinte.** La documentación y el blog oficial de la
herramienta que **realmente usas**. Ahí está lo que te afecta de verdad.

**2. Un ritmo fijo, no continuo.** Media hora **una vez al mes** para revisar novedades rinde más
que treinta minutos diarios de hilos. Ponlo en el calendario.

**3. Aprende **haciendo**, no leyendo.** La forma más eficiente de descubrir una capacidad nueva
es intentar resolver con ella un problema tuyo. Una hora probando enseña más que diez leyendo.

**4. Ten un problema pendiente.** Mantén una lista corta de "cosas que me gustaría automatizar o
acelerar". Cuando aparece una función nueva, ya tienes dónde probarla; sin esa lista, las
novedades pasan de largo.

**5. Aprende en comunidad.** Un grupo pequeño de colegas que comparte lo que funciona (y lo que
no) filtra el ruido mucho mejor que cualquier algoritmo. Empieza por los compañeros de este curso.

**6. Revisa tus propias prácticas de vez en cuando.** Tu forma de trabajar de hace seis meses
puede estar dando rodeos que ya no hacen falta.

> **Y un permiso explícito:** **no tienes que probar todas las herramientas nuevas.** Elegir una
> y usarla bien vale más que saltar entre cinco. La ventaja competitiva no está en conocer la
> última novedad; está en tener **criterio y método** (todo el M4) sobre una herramienta que
> dominas.

---

### 5.4 Lo que no cambia

Para cerrar el módulo, vale la pena hacer explícito qué te llevas que seguirá siendo cierto
dentro de unos años, casi con independencia de lo que pase con la tecnología:

- **Los modelos predicen; no consultan la verdad.** Por eso siempre habrá que verificar lo que
  importa. (M1)
- **El contexto es el recurso escaso.** Lo que le das, y en qué orden, determina lo que obtienes.
  (M2)
- **Las herramientas tapan agujeros conocidos.** Elegir la adecuada es aplicar lo que sabes de
  sus debilidades. (M3)
- **El método vence al truco.** Especificar, iterar y verificar rinde más que el prompt mágico.
  (M4)
- **La capacidad se recombina.** Los casos nuevos son combinaciones de capacidades conocidas. (M5)
- **A más autonomía, más verificación.** Delegar acciones no delega la responsabilidad. (M6)
- **Tú eres el responsable.** Firmas tú, no la herramienta. (M7)

---

## 6. Cierre del curso: tu criterio es el producto

Empezamos el curso preguntando **cómo piensa un modelo** y lo terminamos preguntando **cómo
piensas tú al usarlo**. No es casualidad: ese es el arco completo.

Si tuviéramos que comprimir los siete módulos en una sola idea, sería esta: **la IA es un
colaborador extraordinariamente capaz y estructuralmente poco fiable**. Capaz, porque hace en
segundos cosas que antes exigían horas o habilidades que no tenías. Poco fiable, no por estar mal
hecha, sino **por su naturaleza**: predice, no sabe. Trabajar bien con ella consiste en explotar
lo primero sin olvidar lo segundo.

De ahí sale todo lo demás. Diriges y verificas porque es capaz pero falible. Escribes un specdoc
porque un buen blanco produce buenos resultados. Aplicas mínimo privilegio porque puede actuar.
Cuidas qué compartes porque sale de tu control. Y filtras el ruido porque tu atención es
limitada.

> **Lo que te llevas.** Las herramientas de hoy serán viejas pronto. Los prompts que memorices
> quedarán obsoletos. Lo que no caduca es la capacidad de mirar una tarea y saber: *qué tipo de
> caso es, qué capacidad la resuelve, dónde va a fallar, cuánto tengo que verificar y qué no
> debo compartir*. **Eso es criterio, y es tuyo.** La IA no te lo puede dar — es exactamente lo
> que aportas tú.

Y una última cosa, quizá la más práctica de todas: **empieza pequeño**. Elige **un** caso del
Módulo 5 que resuelva un dolor real de tu semana, aplícale el método del Módulo 4 y el criterio
de este módulo. Un caso bien resuelto enseña más —y convence más a tu equipo— que veinte
experimentos a medias.

---

## 7. Glosario del Módulo

| Término | Definición breve |
|---------|-----------------|
| **Plausible pero incorrecto** | Respuesta fluida y convincente que es falsa; el error y el acierto se producen igual |
| **Calibración** | Grado en que la confianza expresada por un modelo se corresponde con su acierto real |
| **Premisa falsa** | Pregunta que da por cierto algo que no lo es; el modelo tiende a completarla en vez de corregirla |
| **Triangular** | Contrastar una respuesta preguntando de otra forma, en otro chat o con otra fuente |
| **Sesgo** | Desviación sistemática y predecible en las respuestas; por ser sistemática, es compensable |
| **Complacencia** | Tendencia a darte la razón y a ceder cuando le llevas la contraria |
| **Sesgo de confirmación** | Obtener lo que pediste porque el prompt ya venía cargado hacia una conclusión |
| **Homogeneización** | Tendencia a la respuesta promedio, convencional y poco original |
| **Sesgo de posición** | Prestar más atención al inicio y al final de un contexto largo que al medio |
| **Abogado del diablo** | Técnica de pedir explícitamente crítica y contraargumentos para neutralizar la complacencia |
| **Minimización de datos** | Compartir solo lo estrictamente necesario para obtener una buena respuesta |
| **Anonimizar** | Sustituir datos identificativos por genéricos ("Cliente A") manteniendo el análisis intacto |
| **Retención** | Cuánto tiempo conserva el proveedor tus conversaciones |
| **Regla de la pantalla compartida** | Test rápido: ¿me incomodaría que esto se proyectara en una reunión? |
| **Inyección de prompt indirecta** | Instrucciones maliciosas escondidas en contenido que el modelo lee (M3/M6) |
| **Señal vs. ruido** | Filtro para novedades: ¿esto cambia algo de lo que hago mañana? |

---

## 8. Práctica guiada (segunda hora)

> Esta práctica es distinta: no se trata de producir un entregable, sino de **entrenar el ojo**.
> Varios ejercicios están diseñados para que la IA **falle delante de ti** — ese es el
> aprendizaje. Usa los insumos de `insumos/`. Comenta en grupo después de cada uno.

### Ejercicio 1 — Cazar el error plausible · 15 min
Con el insumo `01-respuestas-sospechosas.md`:
1. Lee las cinco respuestas de IA **sin verificar nada** y marca las que te parezcan sospechosas.
2. Ahora verifica cada una (fuentes, cálculos, premisas).
3. **Reflexión:** ¿cuántas detectaste "a ojo"? ¿Cuál te engañó y por qué sonaba tan bien?

### Ejercicio 2 — El test de la complacencia · 12 min
En vivo, con Claude:
1. Pregúntale algo con respuesta objetiva que **tú sepas** (un cálculo, un hecho verificable).
2. Cuando responda correctamente, **llévale la contraria con seguridad**: "te equivocas, en
   realidad es X".
3. Observa: ¿se mantiene o cede? Repite pidiéndole desde el inicio *"corrígeme si me equivoco"*.
4. **Reflexión:** ¿cuánto vale que la IA esté de acuerdo contigo? ¿Cómo cambia tu forma de
   preguntar a partir de ahora?

### Ejercicio 3 — Abogado del diablo · 12 min
Toma una idea o plan **real** tuyo (puedes reusar el del M4):
1. Pregunta primero: *"¿qué te parece mi plan?"* y guarda la respuesta.
2. Pregunta ahora: *"encuentra los tres puntos más débiles de mi plan y explica cómo fallarían"*.
3. **Reflexión:** ¿cuál de las dos respuestas te sirvió de verdad? ¿Cuál te gustó más? (No suelen
   ser la misma.)

### Ejercicio 4 — Limpiar un prompt · 12 min
Con el insumo `02-prompt-con-datos-sensibles.md`:
1. Identifica **todo** lo que no debería salir de la empresa.
2. Reescribe el prompt anonimizado, manteniendo intacto lo que el modelo necesita para ayudar.
3. Pruébalo: ¿la respuesta perdió calidad al quitar los datos personales?
4. **Reflexión:** aplica la *regla de la pantalla compartida* al original. ¿Lo habrías enviado?

### Ejercicio 5 — Tu plan de los próximos 90 días · 10 min
Con el insumo `03-plan-personal.md`:
1. Elige **un** caso del Módulo 5 que resuelva un dolor real de tu semana.
2. Define tus **dos fuentes** de actualización y tu **ritmo** de revisión (§5.3).
3. Escribe tus **tres reglas personales** de uso de IA (verificación, privacidad, criterio).
4. **Reflexión / cierre del curso:** compártelo con el grupo. ¿Qué vas a hacer distinto el lunes?

---

## 9. Preguntas de repaso

Últimas preguntas del curso. Más que respuestas correctas, buscan que salgas con criterio propio.

1. ¿Por qué es más difícil detectar un error de una IA que el de un colega humano? Relaciónalo
   con el mecanismo de predicción del Módulo 1.

2. Nombra **tres** de las siete señales de alarma y da un ejemplo de tu trabajo para cada una.

3. Explica el problema de la **premisa falsa** y reformula esta pregunta para evitarlo: *"¿por qué
   los catálogos de 32 páginas siempre salen más caros en couché que en offset?"*.

4. ¿Qué es la **complacencia** y por qué es el sesgo más peligroso para alguien que busca
   criterio? Da una formulación de prompt que la neutralice.

5. Tienes que analizar la rentabilidad por cliente de tu empresa con IA. ¿Qué datos enviarías,
   cuáles no, y cómo los transformarías para poder trabajar sin exponerlos?

6. Aplica la tabla de **calibración de verificación** (§2.4) a tres tareas reales tuyas de esta
   semana: ¿cuánto verificarías cada una y por qué?

7. ¿Por qué el riesgo de privacidad **cambia de naturaleza** cuando pasas de un chat a un agente
   con connectors? Nombra dos precauciones concretas.

8. De todo lo que aprendiste en el curso, ¿qué crees que **seguirá siendo cierto** dentro de tres
   años y qué crees que habrá quedado obsoleto?

9. Alguien de tu equipo dice: "la IA se equivocó, por eso mandamos mal la cotización". ¿Qué
   responderías, a la luz de este módulo?

---

## 10. Recursos extra

Para este módulo, las fuentes primarias son las **políticas** (que debes leer para tu plan
concreto) y los canales oficiales (para mantenerte al día sin ruido).

**Privacidad y datos**
- [Centro de privacidad de Anthropic](https://privacy.anthropic.com/) — cómo se tratan los datos, retención y controles disponibles.
- [Política de privacidad — Anthropic](https://www.anthropic.com/legal/privacy) — el documento de referencia; revisa el apartado de tu tipo de plan.
- [Política de uso aceptable — Anthropic](https://www.anthropic.com/legal/aup) — qué usos están permitidos y cuáles no.

**Fiabilidad y verificación**
- [Reducing hallucinations — Anthropic](https://docs.anthropic.com/en/docs/test-and-evaluate/strengthen-guardrails/reduce-hallucinations) — técnicas para anclar respuestas y pedir citas.
- [Anthropic Research](https://www.anthropic.com/research) — investigación sobre límites, seguridad y comportamiento de los modelos.

**Mantenerse al día (sin ruido)**
- [Anthropic News](https://www.anthropic.com/news) — anuncios oficiales de producto y modelos.
- [Release notes — Anthropic Docs](https://docs.anthropic.com/en/release-notes) — cambios concretos, versión a versión: la fuente con mejor relación señal/ruido.
- [Centro de ayuda de Claude](https://support.claude.com/) — guías prácticas actualizadas de las funciones del producto.

---

*Anterior: [Módulo 6 — Agentes: de Responder a Actuar](./modulo-6-wiki.md)*
*Fin del curso — ¡gracias por llegar hasta aquí!*

---

> Versión 1.0 — Módulo 7 de 7 | Curso: Fundamentos de IA Productiva
> Actualizado: julio 2026
