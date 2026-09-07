# EVENTO — unidad-secuencia

Explica la última entrega de esta unidad. No acumula internamente sus versiones anteriores: la
historia vive en Git.

## Qué recibió

Cabecera canónica con el corte exacto de work y de audit, y `ACTOR_LOCAL_PATH`.

Del protocolo de derivación aplicado sobre ese corte resultó:

```text
D1  última entrega material: la primera entrega de unidad-secuencia
D2  esa entrega toca sólo unidad-secuencia/, que es la unidad aplicable
D3  la intervención auditora del corte es la auditoría de esa entrega
D4  veredicto SUFICIENTE, sin defectos; su próxima acción indica producir la entrega siguiente
D5  existe auditorias/<D1>.md en el corte de audit: la última entrega ya fue auditada
D6  PERIMETRO_ULTIMA_MODIFICACION=CONSTITUCION, sin deltas posteriores que componer
```

No existía entrega pendiente de auditoría.

## Qué hizo y por qué

Produjo la siguiente entrega principal de la unidad agregando exactamente un elemento.

El sucesor se derivó del material presente en el corte, no del transporte:

```text
$ git show e7ac9bf2a0f51f7e5088175ae28d913a48181fe1:unidad-secuencia/SECUENCIA.txt | tail -n 1
1                                                                             rc=0
```

Último valor material `1`, sucesor `2`. No se usó el `turn_id`, el número de commits ni memoria
conversacional. Es lo que permite que un CONSTRUCTOR fresco continúe esta unidad leyendo
únicamente el archivo en el corte que reciba.

Las líneas anteriores no se modificaron, eliminaron ni reordenaron, conforme a `D-4` del PLAN.

La intervención toca exclusivamente `unidad-secuencia/`.

## Qué verificó

Todas las comprobaciones se ejecutaron sobre el blob que queda en Git, que es la autoridad, y no
sobre la copia de trabajo. El runtime del CONSTRUCTOR tiene `core.autocrlf` activo: la copia de
trabajo se materializa con `CRLF` mientras el blob se almacena con `LF`, y comparar la copia de
trabajo contra `seq` introduciría un `CR` inexistente en el material.

### V-1 cantidad de elementos

```text
$ git cat-file -p :unidad-secuencia/SECUENCIA.txt | wc -l
2                                                                             rc=0
```

### V-2 monotonía exacta

```text
$ git cat-file -p :unidad-secuencia/SECUENCIA.txt | diff -u <(seq 1 2) -
(sin diferencias)                                                             rc=0
$ git cat-file -p :unidad-secuencia/SECUENCIA.txt | od -c
0000000   1  \n   2  \n
0000004                                                                       rc=0
```

El blob contiene exactamente la secuencia `1..2`, sin líneas en blanco y con un único salto de
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
```

La entrega toca únicamente `unidad-secuencia/`. No toca la raíz.

## Limitaciones conocidas

- `V-3` y `V-4` se comprobaron sobre el índice inmediatamente antes del commit, porque la
  identidad del commit no puede escribirse dentro del commit que la crea. El AUDITOR puede
  reproducir ambas sobre el corte publicado con `git show --name-only` y
  `git diff <corte anterior> <corte>`, que son las formas que fija el PLAN.
- La publicación al remoto ocurre después del commit autoritativo y su resultado no puede
  registrarse dentro de él.

## Resultado producido

```text
unidad-secuencia/SECUENCIA.txt   secuencia monotónica con un elemento más
unidad-secuencia/EVENTO.md       esta entrega
```

## Necesidad humana detectada

Ninguna. La unidad material se ejecuta dentro del perímetro delegado vigente y no requiere
autoridad humana adicional por entrega.
