# Insumo 3 — Lote de correos de pedidos

**Ejercicio:** "Clasificar los correos de pedidos" (Tema 3 · Estructuración).

Clasifica cada correo entrante por **tipo de trabajo** (LIBRO / AGENDA / FOLLETO /
MERCHANDISING) y **urgencia** (ALTA / MEDIA / BAJA), de forma consistente. El ejercicio
practica **few-shot** (ejemplos), **XML** (separar ejemplos de datos) y **CoT** (razonar la
urgencia).

---

## A) Ejemplos para el few-shot (ya etiquetados)

Usa estos 3 ejemplos dentro del prompt para fijar el formato:

```
<ejemplo>
  Correo: "Necesito reimprimir 500 trípticos para una feria que es este sábado. ¿Alcanzan?"
  <razonamiento>Folleto + fecha límite inmediata (este sábado).</razonamiento>
  <tipo>FOLLETO</tipo> <urgencia>ALTA</urgencia>
</ejemplo>
<ejemplo>
  Correo: "Queremos cotizar 1.000 cuadernos corporativos para entregar en marzo del próximo año."
  <razonamiento>Merchandising/cuadernos + plazo muy holgado.</razonamiento>
  <tipo>MERCHANDISING</tipo> <urgencia>BAJA</urgencia>
</ejemplo>
<ejemplo>
  Correo: "Avancemos con el anuario del colegio; cierre de contenidos en 3 semanas."
  <razonamiento>Libro/anuario + plazo medio, no inmediato.</razonamiento>
  <tipo>LIBRO</tipo> <urgencia>MEDIA</urgencia>
</ejemplo>
```

## B) Correos para clasificar (los datos)

```
<correo id="1">Hola, somos un colegio y necesitamos 800 agendas escolares para entregar antes
del inicio de clases (primera semana de marzo). ¿Nos cotizan?</correo>

<correo id="2">Se nos acabaron los folletos en plena campaña. Necesitamos 2.000 dípticos
reimpresos para pasado mañana sin falta, el archivo no cambió.</correo>

<correo id="3">Estamos pensando en sacar un libro de fotografía el próximo semestre. Aún no
tenemos fecha, queríamos ir conversando opciones de papel y formato.</correo>

<correo id="4">¿Hacen bolsas de tela con logo? Serían unas 300 para un evento corporativo en
un mes y medio.</correo>

<correo id="5">URGENTE: la tapa del manual que imprimieron salió con un color distinto al
aprobado. Tenemos entrega al cliente final mañana a mediodía.</correo>

<correo id="6">Buenas, quisiéramos cotizar la segunda edición de nuestro recetario, 1.500
ejemplares, tapa dura. No hay apuro, es para fin de año.</correo>

<correo id="7">Necesitamos 5.000 lápices grabados y 5.000 libretas para la kermés del colegio,
que es en dos semanas.</correo>

<correo id="8">Hola, ¿pueden reimprimir el tríptico institucional? Mismo archivo del año
pasado. Lo necesitamos cuando puedan, no es urgente.</correo>
```

---

## Prompt del ejercicio

```
Eres asistente de recepción de pedidos de la imprenta Castro & MacDonald. Clasifica cada
correo por <tipo> (LIBRO, AGENDA, FOLLETO o MERCHANDISING) y <urgencia> (ALTA, MEDIA o BAJA).
Razona primero la urgencia (plazo y consecuencia de no cumplirlo) y luego decide.

Sigue exactamente el formato de los ejemplos.

[pega el bloque A de ejemplos]
[pega el bloque B de correos]
```

**Qué comparar:** hazlo primero SIN los ejemplos (zero-shot) y luego CON ellos. Observa cómo
con few-shot el formato de salida se vuelve idéntico y la clasificación, más consistente. El
correo id="5" (reclamo de color con entrega mañana) es un buen punto de discusión: ¿es FOLLETO
o un caso aparte? ¿ALTA por el plazo?
