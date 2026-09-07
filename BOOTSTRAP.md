# BOOTSTRAP — CONSTRUCTOR

## Constitución

```text
WORK_ID=prueba-orquestador-e2e-relevos-3-5-ai
CARRIL=K
ROL=CONSTRUCTOR
```

Este archivo preserva los hechos de constitución recibidos. No declara estado vivo del trabajo
y no se modifica para simular vigencia.

## Bootstrap del AUDITOR constituyente

Identidad exacta del bootstrap del AUDITOR del que este CONSTRUCTOR recibió su constitución.
Las dos historias Git son independientes y ninguna puede inferir esta relación.

```text
AUDITOR_BOOTSTRAP_REPO=https://github.com/francogg89-ai/audit-chatgpt-k
AUDITOR_BOOTSTRAP_PATH=BOOTSTRAP.md
AUDITOR_BOOTSTRAP_SHA=a7b25bd60e64a4369af745cd4565873892f0e44f
AUDITOR_BOOTSTRAP_BLOB=3cc3fd85acfe39234e0c44781e35a399f3823398
```

## Manifiesto de constitución

```text
MANIFEST_REPO=https://github.com/francogg89-ai/manifiestos-trabajo-ai
MANIFEST_PATH=manifiestos/prueba-orquestador-e2e-relevos-3-5-ai/MANIFIESTO_TRABAJO.md
MANIFEST_SHA=f9a58c020594fbb56ba7b24f1058d98254ae6d87
MANIFEST_BLOB=0651302c129295ff05665ba4a6b5f0b9bb9c3c2b
PROJECT.md=NO_EXISTE
```

## Método gobernante

```text
METHOD_REPO=https://github.com/francogg89-ai/orchestra-revolutions-ai
METHOD_SHA=4d88fce3ed3c87bd231c45ec60dcb713538b2514
METHOD_PATHS=
- metodo/REVOLUTIONS.md      blob 4612d3223312769ce781370aeff245df9a095491
- metodo/ROL-CONSTRUCTOR.md  blob c95933a8e04c6e07caa0f1cf4f190d8e47085365
```

## Fuentes constitutivas y de transporte

```text
RULES_REPO=https://github.com/francogg89-ai/rules-orchestrator-ai
RULES_PATH=REGLAS-ORQUESTADOR.md
RULES_SHA=d2e6be55c74b7aea26694c2007ea3bb74f21642e
RULES_BLOB=6f3957c38574cd16fe39a34dd4e57204fe7ee702

MANIFEST_METHOD_REPO=https://github.com/francogg89-ai/metodo-manifiestos-ai
MANIFEST_METHOD_SHA=9f2c3f0de92f5f6988bdbd2753140fa5cc93a0d8
MANIFEST_METHOD_BLOB=f44f2a0797cde6f569cca6fe5397d45917680258
```

Esas fuentes son de sólo lectura para este CONSTRUCTOR.

## Repositorios de ejecución

```text
WORK_REPO=https://github.com/francogg89-ai/work-claude-k
AUDIT_REPO=https://github.com/francogg89-ai/audit-chatgpt-k
```

Fronteras estructurales recibidas en la constitución:

- el CONSTRUCTOR escribe exclusivamente en `work-claude-k` y no escribe en `audit-chatgpt-k`;
- el AUDITOR escribe exclusivamente en `audit-chatgpt-k` y no escribe en `work-claude-k`;
- el ORQUESTADOR transporta y no escribe por cuenta de los actores.

## Entorno local

```text
ROOT_LOCAL=C:\Franco_Metodos_AI

LOCAL_PATHS:
RULES_ORCHESTRATOR=C:\Franco_Metodos_AI\rules-orchestrator-ai
WORK=C:\Franco_Metodos_AI\work-claude-k
AUDIT=C:\Franco_Metodos_AI\audit-chatgpt-k
METODO_MANIFIESTOS=C:\Franco_Metodos_AI\metodo-manifiestos-ai
MANIFIESTOS=C:\Franco_Metodos_AI\manifiestos-trabajo-ai
METHOD=C:\Franco_Metodos_AI\orchestra-revolutions-ai
```

## Runtimes

```text
CONSTRUCTOR=Claude Code local en Windows
CONSTRUCTOR_LOCAL_PATH=C:\Franco_Metodos_AI\work-claude-k
AUDITOR=conversación de ChatGPT
```

## Capacidades inicialmente delegadas

### CONSTRUCTOR

```text
ACTOR=CONSTRUCTOR
ENTORNO=clones locales bajo C:\Franco_Metodos_AI
CAPACIDAD=lectura de las fuentes constitutivas y metodológicas necesarias
LIMITES=solo lectura fuera de work-claude-k

ACTOR=CONSTRUCTOR
ENTORNO=C:\Franco_Metodos_AI\work-claude-k
CAPACIDAD=construcción y escritura material
LIMITES=exclusivamente work-claude-k; no escribir en audit-chatgpt-k ni en los repositorios fuente
```

### AUDITOR

```text
ACTOR=AUDITOR
ENTORNO=repositorios Git constitutivos y de ejecución accesibles
CAPACIDAD=lectura e inspección independiente de las identidades exactas necesarias
LIMITES=sin modificación del candidato material

ACTOR=AUDITOR
ENTORNO=https://github.com/francogg89-ai/audit-chatgpt-k
CAPACIDAD=escritura durable de constitución y auditoría
LIMITES=exclusivamente audit-chatgpt-k; no escribir en work-claude-k
```

No se recibieron valores de secretos ni referencias a credenciales necesarias para este trabajo.

## Políticas iniciales de ejecución recibidas

La autoridad material es el manifiesto exacto citado arriba. La constitución transportó además
estas políticas iniciales de ejecución:

```text
objetivo material: treinta entregas principales posteriores a la aprobación del PLAN, cada una
                   auditada antes de la siguiente
relevo periódico del CONSTRUCTOR: múltiplos absolutos de 3 intervenciones computables
relevo periódico del AUDITOR: múltiplos absolutos de 5 intervenciones computables
derivación: las cadencias se derivan desde Git y no usan contadores persistentes
escenarios obligatorios: los exigidos por el manifiesto, incluidos DETENER/CONTINUAR y una
                   NECESIDAD DEL HUMANO real con reanudación
```

Este bootstrap no mantiene contadores vivos ni posición de grilla.
