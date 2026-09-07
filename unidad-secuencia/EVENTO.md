# EVENTO — unidad-secuencia

Explica la última entrega de esta unidad. No acumula internamente sus versiones anteriores: la
historia vive en Git.

## Qué recibió

Cabecera canónica completa de `4.3` con `INCOMING_TURN_ID` entero, el corte exacto de work y de
audit, `BOOTSTRAP_REPO`/`BOOTSTRAP_PATH`/`BOOTSTRAP_SHA` y `ACTOR_LOCAL_PATH`.

Es el pase de un relevo periódico del CONSTRUCTOR. Esta instancia es fresca: no dispone de
conversación previa y reconstruyó la situación íntegramente desde Git. El `next_prompt` es
transporte, no fuente ni autoridad: ningún dato material se tomó de él.

### Identidad de las referencias recibidas

```text
$ git cat-file -t e1ddea1eb8cc7ac7509034065f5cf3160d10cc85
commit                                                                        rc=0
$ git rev-parse b5b66b09a1551eb653d5e961eae324c5e8650665:BOOTSTRAP.md
d599f63e7ea051960664c3b4d8dac90382e20f09                                      rc=0
$ git rev-parse e1ddea1:PLAN.md
75a554ee227443ae7b0ed8da784038264d25242f                                      rc=0
$ git -C audit-chatgpt-k fetch origin
70e62b3..f6763ac  main -> origin/main                                         rc=0
$ git -C audit-chatgpt-k cat-file -t f6763acc3f9d37d665f104df46a818d7d90f3210
commit                                                                        rc=0
```

Cada identidad recibida existe realmente en su repositorio, en lugar de suponerse desde el
prompt. El `PLAN.md` presente en el corte conserva el blob aceptado por la decisión humana
preservada en `audit-*`, de modo que la autoridad de diseño aplicada a esta entrega es la
aceptada y no una reinterpretación.

### Protocolo de derivación sobre el corte recibido

```text
$ git show --name-only --format= e1ddea1
unidad-secuencia/EVENTO.md
unidad-secuencia/SECUENCIA.txt                                                rc=0

$ git -C audit-chatgpt-k show --name-only --format= f6763ac
auditorias/e1ddea1eb8cc7ac7509034065f5cf3160d10cc85.md                        rc=0

$ git -C audit-chatgpt-k ls-tree -r --name-only f6763ac | grep e1ddea1
auditorias/e1ddea1eb8cc7ac7509034065f5cf3160d10cc85.md                        rc=0
```

```text
D1  última entrega material alcanzable desde el corte de work: e1ddea1, octava entrega de
    unidad-secuencia
D2  esa entrega toca sólo unidad-secuencia/, que es la unidad aplicable
D3  la intervención auditora del corte es la auditoría de esa misma entrega
D4  veredicto SUFICIENTE, sin defectos. Su próxima acción vigente dispone el relevo del
    CONSTRUCTOR con `NEXT_INSTANCE_CONSTRUCTOR=fresh` y ordena que la instancia fresca
    reconstruya desde Git y produzca la siguiente entrega principal de la unidad. No declara
    token de NECESIDAD DEL HUMANO abierta.
    PERIMETRO_ULTIMA_MODIFICACION=CONSTITUCION
D5  existe auditorias/e1ddea1...md en el corte de audit: la última entrega ya fue auditada
D6  perímetro resuelto sobre BOOTSTRAP.md de work-claude-k, sin deltas posteriores que
    componer
```

No existía entrega pendiente de auditoría ni defecto que corregir. El perímetro delegado vigente
cubre esta intervención sin autoridad adicional.

## Qué hizo y por qué

Produjo la siguiente entrega principal de la unidad agregando exactamente un elemento.

El sucesor se derivó del material presente en el corte, no del transporte:

```text
$ git show e1ddea1eb8cc7ac7509034065f5cf3160d10cc85:unidad-secuencia/SECUENCIA.txt | tail -n 1
8                                                                             rc=0
```

Último valor material `8`, sucesor `9`. No se usó el `turn_id`, el número de commits, ni el
`VALOR_SECUENCIA` o el `ENTREGA_MATERIAL` declarados por la auditoría del corte. Conforme a
`D-5` del PLAN, el archivo en el corte es la única fuente del siguiente valor, incluso cuando la
auditoría enuncia ese mismo número. Esta entrega es además la primera prueba real de esa
propiedad tras un relevo: la instancia que la produce no vio ninguna de las entregas anteriores.

Las líneas anteriores no se modificaron, eliminaron ni reordenaron, conforme a `D-4` del PLAN.
La intervención toca exclusivamente `unidad-secuencia/`.

La cadencia del propio rol no se usó como insumo material. La auditoría del corte deriva que
esta instancia nace de la marca absoluta `9` del CONSTRUCTOR; quién decide y habilita un relevo
es el AUDITOR, conforme a `C-7` y `C-8` del PLAN, y el CONSTRUCTOR no cuenta ni se releva a sí
mismo.

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
9                                                                             rc=0
```

### V-2 monotonía exacta

```text
$ git cat-file -p :unidad-secuencia/SECUENCIA.txt | diff -u <(seq 1 9) -
(sin diferencias)                                                             rc=0
$ git cat-file -p :unidad-secuencia/SECUENCIA.txt | od -c
0000000   1  \n   2  \n   3  \n   4  \n   5  \n   6  \n   7  \n   8  \n
0000020   9  \n
0000022                                                                       rc=0
```

El blob contiene exactamente la secuencia `1..9`, sin líneas en blanco y con un único salto de
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
