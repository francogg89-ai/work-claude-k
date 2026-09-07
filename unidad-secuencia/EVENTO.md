# EVENTO — unidad-secuencia

Explica la última entrega de esta unidad. No acumula internamente sus versiones anteriores: la
historia vive en Git.

## Qué recibió

Cabecera canónica completa de `4.3` con `INCOMING_TURN_ID` entero, el corte exacto de work y de
audit, y `ACTOR_LOCAL_PATH`.

Es un CONSTRUCTOR fresco que entra por el relevo periódico ya habilitado. No dispone de
conversación previa y reconstruyó la situación exclusivamente desde Git.

### Identidad del bootstrap propio

```text
$ git rev-parse b5b66b09a1551eb653d5e961eae324c5e8650665:BOOTSTRAP.md
d599f63e7ea051960664c3b4d8dac90382e20f09                                      rc=0
```

El `BOOTSTRAP_SHA` recibido existe en `work-claude-k` y contiene el `BOOTSTRAP.md` del que se
leyó la constitución durable.

### Protocolo de derivación sobre el corte recibido

```text
$ git rev-parse 6bf2ceb0a3632c6335b1bc7dad21a7b4684094c5
6bf2ceb0a3632c6335b1bc7dad21a7b4684094c5                                      rc=0

$ git show --name-only --format= 6bf2ceb
unidad-secuencia/EVENTO.md
unidad-secuencia/SECUENCIA.txt                                                rc=0

$ git -C audit-chatgpt-k show --name-only --format= fb93997
decisiones/resolucion-h2-relevos-3-5.md                                       rc=0

$ git -C audit-chatgpt-k cat-file -e fb93997:auditorias/6bf2ceb...md
(existe)                                                                      rc=0
```

```text
D1  última entrega material: 6bf2ceb, segunda entrega de unidad-secuencia
D2  esa entrega toca sólo unidad-secuencia/, que es la unidad aplicable
D3  la intervención auditora del corte es una decisión humana preservada, no una auditoría
D4  su próxima acción vigente ordena producir la siguiente entrega material de la unidad y,
    al cerrarla, emitir el pase al AUDITOR con next_instance=fresh. No declara token de
    NECESIDAD DEL HUMANO abierta. PERIMETRO_ULTIMA_MODIFICACION=CONSTITUCION
D5  existe auditorias/<D1>.md en el corte de audit: la última entrega ya fue auditada
D6  perímetro resuelto sobre BOOTSTRAP.md de work-claude-k, sin deltas posteriores que
    componer
```

No existía entrega pendiente de auditoría. El defecto de colisión de relevos registrado en la
auditoría de `6bf2ceb` bloqueaba el pase, no el candidato material: esa auditoría declara
`AFECTA_CANDIDATO_MATERIAL=NO`, y la decisión humana leída en `D3` lo resolvió y reanudó el
loop. Por eso esta intervención continúa la unidad en lugar de corregir la entrega anterior.

## Qué hizo y por qué

Produjo la siguiente entrega principal de la unidad agregando exactamente un elemento.

El sucesor se derivó del material presente en el corte, no del transporte:

```text
$ git show 6bf2ceb0a3632c6335b1bc7dad21a7b4684094c5:unidad-secuencia/SECUENCIA.txt | tail -n 1
2                                                                             rc=0
```

Último valor material `2`, sucesor `3`. No se usó el `turn_id`, el número de commits, el
número de entrega declarado por la auditoría ni memoria conversacional. Es precisamente lo que
esta intervención demuestra: un CONSTRUCTOR fresco, sin ninguna continuidad conversacional,
continúa la unidad leyendo únicamente el archivo en el corte que recibe.

Las líneas anteriores no se modificaron, eliminaron ni reordenaron, conforme a `D-4` del PLAN.

La intervención toca exclusivamente `unidad-secuencia/`.

No se tomó ninguna decisión sobre el relevo del AUDITOR. Esa decisión ya está tomada y
preservada en `audit-*`; esta intervención únicamente la transporta al cerrar, conforme al
cierre de `ROL-CONSTRUCTOR`.

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
3                                                                             rc=0
```

### V-2 monotonía exacta

```text
$ git cat-file -p :unidad-secuencia/SECUENCIA.txt | diff -u <(seq 1 3) -
(sin diferencias)                                                             rc=0
$ git cat-file -p :unidad-secuencia/SECUENCIA.txt | od -c
0000000   1  \n   2  \n   3  \n
0000006                                                                       rc=0
```

El blob contiene exactamente la secuencia `1..3`, sin líneas en blanco y con un único salto de
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
autoridad humana adicional por entrega. La necesidad humana anterior está resuelta y preservada
en el corte de audit recibido; el CONSTRUCTOR no la reabre ni la declara cerrada.
