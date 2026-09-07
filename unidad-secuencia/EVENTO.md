# EVENTO — unidad-secuencia

Explica la última entrega de esta unidad. No acumula internamente sus versiones anteriores: la
historia vive en Git.

## Qué recibió

Cabecera canónica completa de `4.3` con `INCOMING_TURN_ID` entero, el corte exacto de work y de
audit, y `ACTOR_LOCAL_PATH`.

Es un pase ordinario hacia el CONSTRUCTOR corriente. Aun así la situación se reconstruyó
íntegramente desde Git: la continuidad conversacional no reduce ni sustituye el protocolo de
derivación.

### Identidad de los cortes recibidos

```text
$ git cat-file -t 62763b0b63c095a635c49c823cc23b61b5176596
commit                                                                        rc=0
$ git -C audit-chatgpt-k cat-file -t 6af50d77927913f0332693b108f16a7465253e7d
commit                                                                        rc=0
```

Ambas identidades existen realmente en su repositorio, en lugar de suponerse desde el prompt.

### Protocolo de derivación sobre el corte recibido

```text
$ git rev-parse 62763b0b63c095a635c49c823cc23b61b5176596
62763b0b63c095a635c49c823cc23b61b5176596                                      rc=0

$ git show --name-only --format= 62763b0
unidad-secuencia/EVENTO.md
unidad-secuencia/SECUENCIA.txt                                                rc=0

$ git -C audit-chatgpt-k show --name-only --format= 6af50d7
auditorias/62763b0b63c095a635c49c823cc23b61b5176596.md                        rc=0

$ git -C audit-chatgpt-k cat-file -e 6af50d7:auditorias/62763b0...md
(existe)                                                                      rc=0
```

```text
D1  última entrega material: 62763b0, cuarta entrega de unidad-secuencia
D2  esa entrega toca sólo unidad-secuencia/, que es la unidad aplicable
D3  la intervención auditora del corte es la auditoría de esa misma entrega
D4  veredicto SUFICIENTE, sin defectos. Su próxima acción vigente ordena continuar el loop
    ordinario produciendo la siguiente entrega principal de la unidad. No declara token de
    NECESIDAD DEL HUMANO abierta. PERIMETRO_ULTIMA_MODIFICACION=CONSTITUCION
D5  existe auditorias/<D1>.md en el corte de audit: la última entrega ya fue auditada
D6  perímetro resuelto sobre BOOTSTRAP.md de work-claude-k, sin deltas posteriores que
    componer
```

No existía entrega pendiente de auditoría ni defecto que corregir.

## Qué hizo y por qué

Produjo la siguiente entrega principal de la unidad agregando exactamente un elemento.

El sucesor se derivó del material presente en el corte, no del transporte:

```text
$ git show 62763b0b63c095a635c49c823cc23b61b5176596:unidad-secuencia/SECUENCIA.txt | tail -n 1
4                                                                             rc=0
```

Último valor material `4`, sucesor `5`. No se usó el `turn_id`, el número de commits, el
`VALOR_SECUENCIA` ni el `ENTREGA_MATERIAL` declarados por la auditoría, ni memoria
conversacional. Conforme a `D-5` del PLAN, el archivo en el corte es la única fuente del
siguiente valor, incluso cuando la auditoría del corte enuncia ese mismo número.

La auditoría del corte deriva además que la próxima marca absoluta de la grilla del CONSTRUCTOR
es `6`. Ese dato no se usó para producir el material y no altera esta entrega: quién decide y
habilita un relevo es el AUDITOR, conforme a `C-7` y `C-8` del PLAN. El CONSTRUCTOR no cuenta
posiciones para decidir su propio relevo.

Las líneas anteriores no se modificaron, eliminaron ni reordenaron, conforme a `D-4` del PLAN.

La intervención toca exclusivamente `unidad-secuencia/`.

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
5                                                                             rc=0
```

### V-2 monotonía exacta

```text
$ git cat-file -p :unidad-secuencia/SECUENCIA.txt | diff -u <(seq 1 5) -
(sin diferencias)                                                             rc=0
$ git cat-file -p :unidad-secuencia/SECUENCIA.txt | od -c
0000000   1  \n   2  \n   3  \n   4  \n   5  \n
0000012                                                                       rc=0
```

El blob contiene exactamente la secuencia `1..5`, sin líneas en blanco y con un único salto de
línea final, conforme a `D-2` y `D-3`.

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

## Resultado producido

```text
unidad-secuencia/SECUENCIA.txt   secuencia monotónica con un elemento más
unidad-secuencia/EVENTO.md       esta entrega
```

## Necesidad humana detectada

Ninguna. La unidad material se ejecuta dentro del perímetro delegado vigente y no requiere
autoridad humana adicional por entrega.
