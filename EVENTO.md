# EVENTO — intervención constitutiva

Intervención previa a toda unidad. Toca únicamente la raíz.

## Qué recibió

Un prompt de constitución inicial conforme a `4.3` del método: `ROL=CONSTRUCTOR`, `WORK_ID`,
`CARRIL`, `INCOMING_TURN_ID` entero, método gobernante, manifiesto, repositorios de auditoría,
trabajo y fuentes, raíz y rutas locales, entornos relevantes, capacidades inicialmente
delegadas y la identidad exacta del bootstrap del AUDITOR constituyente.

No existía bootstrap propio ni corte previo de work. Por eso no se aplicó el protocolo de
derivación `D1-D6`: no había corte de work sobre el cual aplicarlo.

## Qué hizo y por qué

1. Sincronizó las fuentes indicadas y comprobó que cada SHA constitutivo existe realmente en su
   repositorio, en lugar de suponerlo desde el prompt.
2. Localizó el bootstrap del AUDITOR por repositorio, path y SHA exactos, y lo leyó.
3. Creó `BOOTSTRAP.md`, preservando los hechos de constitución y la identidad exacta del
   bootstrap del AUDITOR. Las dos historias Git son independientes y ninguna puede inferir esa
   relación.
4. Comprobó las capacidades aplicables a esta intervención.
5. Produjo `PLAN.md`: el plan mínimo compatible con el manifiesto, con una sola unidad material
   trivial y determinista.
6. No inició la unidad material. El manifiesto sitúa las treinta entregas después de la
   aprobación del PLAN.

## Decisiones técnicas tomadas

- Una sola unidad, un solo archivo de texto plano como materia. Cualquier estructura mayor
  agregaría superficie que la prueba no necesita.
- El valor siguiente de la secuencia se deriva del contenido del archivo en el corte recibido,
  nunca del transporte. Es lo que permite que un CONSTRUCTOR fresco continúe sin conversación
  previa.
- `.gitignore` con una única entrada, `.atl/`, que es ruido de herramientas locales del runtime
  del CONSTRUCTOR y no materia del trabajo.

Ninguna de estas decisiones se trasladó al humano: son decisiones técnicas del rol.

## Qué verificó

### Identidad exacta de las fuentes

```text
$ git -C orchestra-revolutions-ai cat-file -t 4d88fce3ed3c87bd231c45ec60dcb713538b2514
commit                                                                        rc=0
$ git -C rules-orchestrator-ai cat-file -t d2e6be55c74b7aea26694c2007ea3bb74f21642e
commit                                                                        rc=0
$ git -C metodo-manifiestos-ai cat-file -t 9f2c3f0de92f5f6988bdbd2753140fa5cc93a0d8
commit                                                                        rc=0
$ git -C manifiestos-trabajo-ai rev-parse f9a58c0:manifiestos/prueba-orquestador-e2e-relevos-3-5-ai/MANIFIESTO_TRABAJO.md
0651302c129295ff05665ba4a6b5f0b9bb9c3c2b                                      rc=0
$ git -C orchestra-revolutions-ai rev-parse 4d88fce:metodo/REVOLUTIONS.md
4612d3223312769ce781370aeff245df9a095491                                      rc=0
$ git -C orchestra-revolutions-ai rev-parse 4d88fce:metodo/ROL-CONSTRUCTOR.md
c95933a8e04c6e07caa0f1cf4f190d8e47085365                                      rc=0
$ git -C rules-orchestrator-ai rev-parse d2e6be5:REGLAS-ORQUESTADOR.md
6f3957c38574cd16fe39a34dd4e57204fe7ee702                                      rc=0
$ git -C metodo-manifiestos-ai rev-parse 9f2c3f0:METODO-MANIFIESTOS.md
f44f2a0797cde6f569cca6fe5397d45917680258                                      rc=0
```

### Bootstrap del AUDITOR

```text
$ git -C audit-chatgpt-k rev-parse origin/main
a7b25bd60e64a4369af745cd4565873892f0e44f                                      rc=0
$ git -C audit-chatgpt-k ls-tree -r origin/main
100644 blob 3cc3fd85acfe39234e0c44781e35a399f3823398  BOOTSTRAP.md            rc=0
$ git -C audit-chatgpt-k rev-parse origin/main:BOOTSTRAP.md
3cc3fd85acfe39234e0c44781e35a399f3823398                                      rc=0
```

El `AUDITOR_BOOTSTRAP_SHA` recibido coincide exactamente con la punta publicada de
`audit-chatgpt-k`, y su único artefacto es el `BOOTSTRAP.md` citado. Se leyó su contenido
completo y las coordenadas constitutivas que declara coinciden con las recibidas.

### Correspondencia entre punta publicada y SHA constitutivo

```text
$ for r in ...; do git -C $r rev-parse --short main origin/main; done
orchestra-revolutions-ai     local_main=4d88fce  origin_main=4d88fce           rc=0
rules-orchestrator-ai        local_main=d2e6be5  origin_main=d2e6be5           rc=0
manifiestos-trabajo-ai       local_main=45ec9fb  origin_main=f9a58c0           rc=0
metodo-manifiestos-ai        local_main=9f2c3f0  origin_main=9f2c3f0           rc=0
audit-chatgpt-k              local_main=NONE     origin_main=a7b25bd           rc=0
```

### Capacidades comprobadas

```text
$ git -C work-claude-k config user.name / user.email
Franco Guglianone / francogg89@gmail.com                                      rc=0
$ git -C work-claude-k symbolic-ref --short HEAD
main                                                                          rc=0
$ git -C work-claude-k ls-remote origin
(sin refs: repositorio publicado todavía vacío)                               rc=0
$ git config --get-all credential.helper
manager                                                                       rc=0
```

Lectura de las fuentes bajo `C:\Franco_Metodos_AI`: comprobada por las lecturas anteriores.
Escritura material en `C:\Franco_Metodos_AI\work-claude-k`: comprobada por esta entrega.
No se intentó ninguna escritura fuera de `work-claude-k`.

## Limitaciones conocidas

- La publicación al remoto ocurre después del commit autoritativo y su resultado no puede
  registrarse dentro del commit que la precede. Que el remoto sea legible y que exista un
  gestor de credenciales configurado no demuestra por sí solo la escritura remota.
- En el clon local de `manifiestos-trabajo-ai` la rama local `main` apunta a `45ec9fb`, que
  diverge de `origin/main` y no contiene el path del manifiesto. La identidad autoritativa
  usada es `f9a58c0`, que es exactamente `origin/main` y el SHA recibido en la constitución.
  Un actor que lea la punta de esa rama local en lugar del SHA exacto obtendría un resultado
  incorrecto. Es una observación del entorno local, no del material de este trabajo.
- Un resultado local no demuestra una propiedad que sólo pueda comprobarse en un entorno real.

## Resultado producido

```text
BOOTSTRAP.md   hechos de constitución e identidad exacta del bootstrap del AUDITOR
PLAN.md        plan mínimo compatible con el manifiesto
EVENTO.md      esta intervención
.gitignore     exclusión del ruido de herramientas locales del runtime
```

No se creó todavía el directorio de la unidad material.

## Necesidad humana detectada

Se registra y se rutea. Determinar si es real corresponde al AUDITOR; el CONSTRUCTOR no la
declara y no activa directamente al humano.

```text
QUE      una decisión humana sobre la identidad exacta de PLAN.md producida por esta entrega,
         antes de que comience la unidad material
POR QUE  2.2 del método sitúa la aceptación del plan en una decisión humana preservada en
         audit-*, ligada al SHA exacto aceptado, y 10 condiciona el avance entre unidades a que
         el plan haya recibido esa decisión. Esa aceptación no está comprendida en el perímetro
         delegado del CONSTRUCTOR ni en el del AUDITOR
TIPO     no material según 7.1: es una decisión, no exige trabajo sobre un entorno real y no
         crea checkpoint
ALCANCE  aceptar, rechazar o devolver con cambios el plan en su identidad exacta
```

No se creó `CHECKPOINT_HUMANO.md`: forzar el mecanismo material de `7.4` para una decisión no
aportaría ninguna propiedad y el método lo desaconseja expresamente.
