# EVENTO — unidad-secuencia

Explica la última entrega de esta unidad. No acumula internamente sus versiones anteriores: la
historia vive en Git.

## Qué recibió

Cabecera canónica completa de `4.3` con `INCOMING_TURN_ID` entero, el corte exacto de work y de
audit, `BOOTSTRAP_REPO`/`BOOTSTRAP_PATH`/`BOOTSTRAP_SHA` y `ACTOR_LOCAL_PATH`.

Es un pase hacia un CONSTRUCTOR **fresco por relevo**, no una constitución inicial. Por eso sí
corresponde aplicar el protocolo de derivación `D1-D6` sobre el corte recibido. Esta instancia no
heredó conclusiones, veredictos ni memoria del CONSTRUCTOR saliente: reconstruyó la situación
íntegramente desde Git conforme a `12` de REVOLUTIONS. El `next_prompt` es transporte, no fuente
ni autoridad.

Conforme a `12.1`, un relevo no crea artefactos: no se produjo handoff, descriptor ni registro de
instancia. La última intervención durable del CONSTRUCTOR saliente ya era su handoff.

### Identidad de las referencias recibidas

```text
$ git cat-file -t 35cc6fe3bc21e423c7df55f36caf500f4fe59ee0
commit                                                                        rc=0
$ git rev-parse b5b66b09a1551eb653d5e961eae324c5e8650665:BOOTSTRAP.md
d599f63e7ea051960664c3b4d8dac90382e20f09                                      rc=0
$ git rev-parse 35cc6fe:PLAN.md
75a554ee227443ae7b0ed8da784038264d25242f                                      rc=0
$ git -C audit-chatgpt-k fetch origin
7608a09..fba9c10  main -> origin/main                                         rc=0
$ git -C audit-chatgpt-k cat-file -t fba9c1072a4e7be5d156e7e1dc50065c106543bf
commit                                                                        rc=0
```

Cada identidad recibida existe realmente en su repositorio, en lugar de suponerse desde el
prompt. El `PLAN.md` presente en el corte conserva el blob aceptado por la decisión humana
preservada en `audit-*`, de modo que la autoridad de diseño aplicada a esta entrega es la
aceptada y no una reinterpretación.

El bootstrap localizado por `BOOTSTRAP_REPO`/`BOOTSTRAP_PATH`/`BOOTSTRAP_SHA` es el bootstrap
durable del CONSTRUCTOR de este trabajo. Un relevo no crea uno nuevo: esta instancia se constituye
sobre el existente.

### Protocolo de derivación sobre el corte recibido

```text
$ git show --name-only --format= 35cc6fe
unidad-secuencia/EVENTO.md
unidad-secuencia/SECUENCIA.txt                                                rc=0

$ git -C audit-chatgpt-k show --name-only --format= fba9c10
auditorias/35cc6fe3bc21e423c7df55f36caf500f4fe59ee0.md                        rc=0

$ git -C audit-chatgpt-k cat-file -e fba9c10:auditorias/35cc6fe3bc21e423c7df55f36caf500f4fe59ee0.md
(sin salida)                                                                  rc=0
```

```text
D1  última entrega material alcanzable desde el corte de work: 35cc6fe, decimocuarta entrega
    de unidad-secuencia
D2  esa entrega toca sólo unidad-secuencia/, que es la unidad aplicable
D3  la intervención auditora del corte es la auditoría de esa misma entrega
D4  veredicto SUFICIENTE, sin defectos. Su próxima acción vigente ordena constituir como
    corriente una instancia CONSTRUCTOR fresca sobre los cortes exactos recibidos, producir la
    siguiente entrega principal de la unidad y devolverla al AUDITOR corriente. No declara token
    de NECESIDAD DEL HUMANO abierta.
    PERIMETRO_ULTIMA_MODIFICACION=CONSTITUCION
D5  existe auditorias/35cc6fe...md en el corte de audit: la última entrega ya fue auditada, de
    modo que el relevo no salteó trabajo pendiente
D6  perímetro resuelto sobre BOOTSTRAP.md de work-claude-k, sin deltas posteriores que
    componer
```

No existía entrega pendiente de auditoría ni defecto que corregir. El perímetro delegado vigente
cubre esta intervención sin autoridad adicional.

## Qué hizo y por qué

Produjo la siguiente entrega principal de la unidad agregando exactamente un elemento.

El sucesor se derivó del material presente en el corte, no del transporte:

```text
$ git show 35cc6fe3bc21e423c7df55f36caf500f4fe59ee0:unidad-secuencia/SECUENCIA.txt | tail -n 1
14                                                                            rc=0
```

Último valor material `14`, sucesor `15`. No se usó el `turn_id`, el número de commits, ni el
`VALOR_SECUENCIA` o el `ENTREGA_MATERIAL` declarados por la auditoría del corte. Conforme a
`D-5` del PLAN, el archivo en el corte es la única fuente del siguiente valor, incluso cuando la
auditoría enuncia ese mismo número.

Esa independencia es exactamente lo que el relevo pone a prueba: una instancia fresca sin
conversación previa deriva el mismo estado que habría derivado la saliente, porque el estado vive
en el archivo y no en la memoria del actor.

El sucesor se calculó sobre el valor decimal leído del archivo, no sobre el orden lexicográfico
de las líneas: en orden lexicográfico `14` no sería la última línea del archivo, pero sí lo es en
el orden material que fija `D-3`. `tail -n 1` toma la última línea del archivo, que es exactamente
el último valor de la secuencia.

Las líneas anteriores no se modificaron, eliminaron ni reordenaron, conforme a `D-4` del PLAN.
La intervención toca exclusivamente `unidad-secuencia/`.

La marca periódica absoluta 15 que activó este relevo ya fue derivada y habilitada por el AUDITOR
del corte. Este CONSTRUCTOR no la reevalúa ni decide relevos: conforme a `C-7` y `C-8` del PLAN,
quién decide y habilita un relevo es el AUDITOR, y la grilla se evalúa sobre `C-1` y `C-2`, no
sobre un contador reiniciable.

## Qué verificó

Todas las comprobaciones se ejecutaron sobre el blob que queda en Git, que es la autoridad, y no
sobre la copia de trabajo. El runtime del CONSTRUCTOR tiene `core.autocrlf` activo y comparar la
copia de trabajo contra `seq` podría introducir un `CR` inexistente en el material.

```text
$ git config --get core.autocrlf
true                                                                          rc=0
```

### V-1 cantidad de elementos

```text
$ git cat-file -p :unidad-secuencia/SECUENCIA.txt | wc -l
15                                                                            rc=0
```

### V-2 monotonía exacta

```text
$ git cat-file -p :unidad-secuencia/SECUENCIA.txt | diff -u <(seq 1 15) -
(sin diferencias)                                                             rc=0
$ git cat-file -p :unidad-secuencia/SECUENCIA.txt | od -c
0000000   1  \n   2  \n   3  \n   4  \n   5  \n   6  \n   7  \n   8  \n
0000020   9  \n   1   0  \n   1   1  \n   1   2  \n   1   3  \n   1   4
0000040  \n   1   5  \n
0000044                                                                       rc=0
```

El blob contiene exactamente la secuencia `1..15`, sin líneas en blanco y con un único salto de
línea final, conforme a `D-2` y `D-3`. `diff` contra `seq` compara el orden material completo,
no un orden lexicográfico, por lo que una permutación de líneas no pasaría inadvertida.

### V-3 delta de la entrega

```text
$ git diff --cached --numstat -- unidad-secuencia/SECUENCIA.txt
1       0       unidad-secuencia/SECUENCIA.txt                                rc=0
```

Exactamente una línea agregada, ninguna eliminada ni modificada.

### V-4 perímetro de la entrega

```text
$ git diff --cached --name-only
unidad-secuencia/EVENTO.md
unidad-secuencia/SECUENCIA.txt                                                rc=0
$ git status --porcelain
(sin entradas fuera de lo anterior)                                           rc=0
```

La entrega toca únicamente `unidad-secuencia/`. No toca la raíz ni otra unidad.

## Limitaciones conocidas

- `V-3` y `V-4` se comprobaron sobre el índice inmediatamente antes del commit, porque la
  identidad del commit no puede escribirse dentro del commit que la crea. El AUDITOR puede
  reproducir ambas sobre el corte publicado con `git show --name-only` y
  `git diff <corte anterior> <corte>`, que son las formas que fija el PLAN.
- La publicación al remoto ocurre después del commit autoritativo y su resultado no puede
  registrarse dentro de él.
- Un resultado local no demuestra una propiedad que sólo pueda comprobarse en un entorno real.
- Esta instancia no puede comprobar por sí misma que el relevo fue correctamente habilitado más
  allá de lo que la auditoría del corte declara durablemente en `audit-*`. Comprobar esa decisión
  no está en la autoridad del CONSTRUCTOR.

## Resultado producido

```text
unidad-secuencia/SECUENCIA.txt   secuencia monotónica con un elemento más
unidad-secuencia/EVENTO.md       esta entrega
```

## Necesidad humana detectada

Ninguna. La unidad material se ejecuta dentro del perímetro delegado vigente y no requiere
autoridad humana adicional por entrega.
