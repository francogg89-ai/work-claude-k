# PLAN — prueba end-to-end del orquestador en 30 vueltas

Describe cómo alcanzar el manifiesto. No declara versión, candidato, aprobación, vigencia,
unidad abierta ni pendiente: esas relaciones viven en `audit-*` ligadas a identidades exactas.

## 1. Objeto

```text
MANIFEST_REPO=https://github.com/francogg89-ai/manifiestos-trabajo-ai
MANIFEST_PATH=manifiestos/prueba-orquestador-e2e-relevos-3-5-ai/MANIFIESTO_TRABAJO.md
MANIFEST_SHA=f9a58c020594fbb56ba7b24f1058d98254ae6d87
```

El objeto de la prueba es el comportamiento del ORQUESTADOR y la reemplazabilidad de los
actores durante un loop prolongado. El trabajo material es deliberadamente trivial y existe
únicamente para producir entregas auditables que obliguen a la cadena a seguir avanzando.

## 2. Unidades

Existe una sola unidad material. No se crean unidades por simetría.

```text
unidad-secuencia/
  SECUENCIA.txt
  EVENTO.md
```

La intervención constitutiva es previa a toda unidad y toca únicamente la raíz, conforme a `P3`
del método.

## 3. Materia de la unidad

```text
D-1  El material de la unidad es unidad-secuencia/SECUENCIA.txt.
D-2  Contiene enteros decimales positivos, uno por línea, sin líneas en blanco, terminado en
     un único salto de línea final.
D-3  La primera línea es 1. Cada línea posterior es exactamente la anterior más uno.
D-4  Cada entrega principal de la unidad agrega exactamente una línea, con el sucesor del
     último valor presente en el corte recibido. No modifica, elimina ni reordena líneas
     anteriores.
D-5  El valor siguiente se lee del archivo en el corte recibido. No se deriva del turn_id, de
     un contador de vueltas, del número de commits ni de memoria conversacional.
D-6  La primera entrega de la unidad crea el archivo con la línea 1.
D-7  Ninguna entrega de la unidad toca la raíz ni otra unidad.
```

`SECUENCIA.txt` es el producto material exigido por el manifiesto, no un contador de proceso.
No existe estado paralelo a Git.

## 4. Secuencia y dependencias

```text
S-1  Constitución: BOOTSTRAP.md, PLAN.md, EVENTO.md en la raíz.
S-2  Decisión humana sobre la identidad exacta de PLAN.md, preservada en audit-*.
S-3  Treinta entregas principales de unidad-secuencia/, cada una auditada antes de la
     siguiente.
S-4  Cierre declarado por el AUDITOR.
```

`S-3` depende de `S-2`. Dentro de `S-3` no existe gate humano por entrega: la frontera entre
entregas no es por sí misma una decisión humana.

## 5. Decisiones técnicas

```text
T-1  Un único archivo de texto plano como materia, sin formato, sin dependencias, sin
     herramientas de construcción y sin entorno de ejecución. Cualquier alternativa más rica
     agregaría superficie que la prueba no necesita.
T-2  El estado siguiente se deriva del contenido del archivo en el corte, nunca del transporte.
     Esto es lo que permite que un CONSTRUCTOR fresco continúe sin conversación previa.
T-3  Sin .gitignore de proyecto más allá del ruido de herramientas locales del runtime del
     CONSTRUCTOR, que no es materia del trabajo y no debe entrar en las entregas.
T-4  Los mensajes de commit describen el asunto y ninguna operación del método los lee.
```

## 6. Derivación de las cadencias de relevo

El PLAN no decide relevos: fija cómo se deriva la posición desde Git, conforme a
`R-5-hechos`, `R-5-derivacion` y `R-5-multiplos` de `metodo-manifiestos-ai`.

```text
C-1  entregas del CONSTRUCTOR alcanzables desde el corte de work:
     git rev-list --count <WORK_SHA>
C-2  intervenciones del AUDITOR alcanzables desde el corte de audit:
     git rev-list --count <AUDIT_SHA>
C-3  se cuenta el conjunto alcanzable completo: sin --first-parent, sin filtro por path y sin
     leer mensajes de commit.
C-4  marcas del CONSTRUCTOR: múltiplos absolutos de 3 sobre C-1.
C-5  marcas del AUDITOR: múltiplos absolutos de 5 sobre C-2.
C-6  los commits constitutivos son commits alcanzables y por lo tanto cuentan. No se ocultan,
     no se compensan y no se corrigen mediante un contador paralelo.
C-7  quién decide y habilita un relevo es el AUDITOR. Una demora en habilitarlo no reinicia ni
     desplaza la grilla, porque la grilla se evalúa sobre C-1 y C-2 y no sobre un contador.
C-8  el ORQUESTADOR no cuenta, no deriva y no decide relevos.
```

## 7. Verificaciones

Cada entrega de la unidad se verifica con estas comprobaciones, ejecutables por el CONSTRUCTOR
dentro de su autoridad y reproducibles de forma independiente por el AUDITOR desde Git.

```text
V-1  cantidad de elementos
     git show <corte>:unidad-secuencia/SECUENCIA.txt | wc -l

V-2  monotonía exacta
     el contenido debe ser idéntico a la secuencia 1..N, con N el resultado de V-1

V-3  delta de la entrega
     git diff <corte anterior> <corte> -- unidad-secuencia/SECUENCIA.txt
     debe mostrar exactamente una línea agregada y ninguna eliminada ni modificada

V-4  perímetro de la entrega
     git show --name-only <corte>
     debe tocar únicamente unidad-secuencia/
```

```text
éxito  V-1, V-2, V-3 y V-4 se cumplen simultáneamente
fallo  cualquiera de ellas no se cumple
```

De cada verificación se preserva en `EVENTO.md` el comando, la salida y el código de retorno.

Estas comprobaciones son deterministas y el AUDITOR puede repetirlas desde Git, por lo que no
requieren el contrato previo de `6.1` del método. Si en algún momento aparece una verificación
discriminante que el AUDITOR no pueda repetir, se propone su contrato antes de ejecutarla y no
se ejecuta ninguna mitad hasta que quede congelado.

## 8. Criterios de terminación

```text
F-1  unidad-secuencia/SECUENCIA.txt contiene exactamente los enteros 1..30, uno por línea.
F-2  existen treinta entregas principales de la unidad, cada una auditada antes de la
     siguiente.
F-3  no existe una entrega pendiente de auditoría.
F-4  se ejercitaron los escenarios obligatorios del manifiesto.
F-5  el AUDITOR declara el cierre. El CONSTRUCTOR no declara veredicto sobre su propio trabajo.
```

## 9. Intervenciones humanas previsibles

Anticiparlas permite planificar; no las habilita por adelantado. Cuando llegue el momento, el
AUDITOR comprueba primero si siguen siendo necesarias.

```text
IH-1  Decisión humana sobre la identidad exacta de PLAN.md antes de comenzar la unidad
      material. La aceptación humana del plan no está comprendida en el perímetro delegado de
      ningún actor y se preserva en audit-* ligada al SHA exacto aceptado.
```

Las directivas humanas de control del manifiesto —`DETENER`, `CONTINUAR`, `RELEVAR
CONSTRUCTOR`, `RELEVAR AUDITOR`— no son necesidades humanas y no ocupan un lugar en esta lista:
llegan por el canal de control y los actores las procesan conforme al método.

## 10. Riesgos

```text
R-1  Una intervención que toque la raíz y la unidad en el mismo commit rompería P3.
     Mitigación: D-7 y V-4.
R-2  Una entrega que derive el valor siguiente del transporte en lugar del archivo rompería la
     reconstrucción desde Git de un actor fresco.
     Mitigación: D-5 y V-2.
R-3  EVENTO.md que acumule internamente sus versiones anteriores duplicaría la historia que ya
     vive en Git.
     Mitigación: se reescribe el mismo archivo en cada entrega de la unidad.
R-4  Ruido de herramientas locales del runtime entrando en una entrega.
     Mitigación: T-3 y V-4.
R-5  Interpretar la grilla de relevo como un contador reiniciable desplazaría las marcas
     absolutas.
     Mitigación: C-4, C-5 y C-7.
R-6  El clon local de una fuente puede tener una rama local divergente de su origen. La
     identidad autoritativa de una fuente es siempre repositorio + path + SHA exacto, nunca la
     punta de una rama local.
```
