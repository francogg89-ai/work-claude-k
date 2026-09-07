# EVENTO — unidad-secuencia

Explica la última entrega de esta unidad. No acumula internamente sus versiones anteriores: la
historia vive en Git.

## Qué recibió

Cabecera canónica con el corte exacto de work y de audit, y `ACTOR_LOCAL_PATH`.

Del protocolo de derivación aplicado sobre ese corte resultó:

```text
D1  última entrega material: la intervención constitutiva
D2  esa entrega toca sólo la raíz, por lo que es previa a toda unidad
D3  la intervención auditora del corte preserva una decisión humana
D4  su próxima acción indica comenzar la unidad material
D5  existe la auditoría de la última entrega: fue auditada y no arrojó defectos
D6  PERIMETRO_ULTIMA_MODIFICACION=CONSTITUCION, sin deltas posteriores que componer
```

La decisión humana preservada acepta `PLAN.md` en una identidad exacta. Se comprobó que el blob
del PLAN en el corte de work coincide con el blob aceptado, en lugar de suponerlo:

```text
$ git rev-parse b5b66b09a1551eb653d5e961eae324c5e8650665:PLAN.md
75a554ee227443ae7b0ed8da784038264d25242f                                      rc=0
```

## Qué hizo y por qué

Comenzó la única unidad material del PLAN produciendo su primera entrega principal.

Conforme a `D-6` del PLAN, la primera entrega crea `SECUENCIA.txt` con la línea `1`. En el corte
recibido el archivo no existía, de modo que no había un último valor del cual tomar el sucesor.

El valor no se derivó del `turn_id`, del número de commits ni de memoria conversacional. Esa
independencia es lo que permite que un CONSTRUCTOR fresco continúe esta unidad leyendo
únicamente el archivo en el corte que reciba.

La intervención toca exclusivamente `unidad-secuencia/`.

## Qué verificó

### V-1 cantidad de elementos

```text
$ git cat-file -p :unidad-secuencia/SECUENCIA.txt | wc -l
1                                                                             rc=0
```

### V-2 monotonía exacta

```text
$ git cat-file -p :unidad-secuencia/SECUENCIA.txt | diff -u <(seq 1 1) -
(sin diferencias)                                                             rc=0
$ git cat-file -p :unidad-secuencia/SECUENCIA.txt | od -c
0000000   1  \n
0000002                                                                       rc=0
```

El blob contiene exactamente la secuencia `1..1`, sin líneas en blanco y con un único salto de
línea final, conforme a `D-2` y `D-3`.

`V-1` y `V-2` se comprobaron sobre el blob que queda en Git, que es la autoridad, y no sobre la
copia de trabajo. El runtime del CONSTRUCTOR tiene `core.autocrlf` activo: la copia de trabajo
se materializa con `CRLF` mientras el blob se almacena con `LF`. Comparar la copia de trabajo
contra `seq` introduciría un `CR` final que no existe en el material y produciría un fallo
espurio. La forma reproducible por el AUDITOR sobre el corte publicado es
`git show <corte>:unidad-secuencia/SECUENCIA.txt`.

### V-3 delta de la entrega

En la primera entrega de la unidad no existe una versión anterior del archivo contra la cual
diferenciar. El delta equivalente es la creación del archivo con exactamente una línea agregada
y ninguna eliminada.

```text
$ git diff --cached --numstat -- unidad-secuencia/SECUENCIA.txt
1       0       unidad-secuencia/SECUENCIA.txt                                rc=0
```

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
unidad-secuencia/SECUENCIA.txt   primera entrega de la secuencia monotónica
unidad-secuencia/EVENTO.md       esta entrega
```

## Necesidad humana detectada

Ninguna. La decisión humana que el PLAN anticipaba en `IH-1` ya fue resuelta y preservada en
`audit-*`. La unidad material se ejecuta dentro del perímetro delegado vigente y no requiere
autoridad humana adicional por entrega.
