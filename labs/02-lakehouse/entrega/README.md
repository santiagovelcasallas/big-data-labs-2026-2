# Lab 2 · Entrega

**Equipo:** Luis Alberto Ortiz Quiroga · Santiago Vélez Casallas
**Entrega:** viernes 6 de noviembre de 2026 · **Peso:** 30% · Enunciado: [`../README.md`](../README.md)

Esta carpeta reúne las evidencias, el diagrama y el informe. El código se completa en su lugar
(`ingest.py`, `producer.py`, `jobs/`, `sql/athena.sql`, `infra/serverless.yml`); los archivos dados
(`jobs/common.py`, `run_local.sh`, `run_aws.sh`, `tests/`) y las validaciones de cada job no se modifican.

## Entregables del README y dónde van

| | Entregable | Dónde |
|---|---|---|
| ☐ | Código: `ingest.py`, `producer.py`, los 5 jobs, `athena.sql` y `serverless.yml` | En su lugar dentro de `labs/02-lakehouse/` |
| ☐ | Captura de `pytest` en verde (los dos archivos de tests) | `evidencias/a_batch_local/` (`test_ingest`) y `evidencias/b_streaming_local/` (`test_producer`) |
| ☐ | Salida de `run_local.sh` para los dos lotes, incluida la segunda ejecución del lote 2 (idempotencia) | `evidencias/a_batch_local/` |
| ☐ | Salida de `run_local.sh stream` en modo availableNow (dos veces: idempotencia) y en vivo | `evidencias/b_streaming_local/` |
| ☐ | Captura de los 4 jobs batch en `Succeeded` para los dos lotes, y del job `paytrack-stream` en `Succeeded` | `evidencias/aws_glue/` |
| ☐ | Resultados y MB escaneados de las 6 consultas de Athena | `evidencias/athena/` |
| ☐ | Diagrama de la arquitectura en draw.io: zonas, tablas por capa, jobs, consultas de streaming y servicios de AWS | `diagrama/` (`.drawio` + `.png`) |
| ☐ | Informe en PDF (máx. 8 páginas) con las respuestas y los experimentos | `informe/` |
| ☐ | Recursos eliminados, incluido el stream de Kinesis | `evidencias/limpieza/` (captura de S3, CloudFormation y Kinesis vacíos) |

## Orden de trabajo (del README)

1. **A.0** generar los lotes → **A.1** batch en local (cada lote dos veces).
2. **B.1** productor con tests → **B.2** streaming en local (availableNow dos veces y en vivo) → **B.3** experimentos.
3. **AWS** el mismo día: desplegar, correr los dos lotes y el stream, Athena, y **limpieza**.
4. Diagrama e informe.

## Antes de usar AWS

Copiar `.envs/aws.env.example` a `.envs/aws.env` y llenar las credenciales. `.envs/*.env` está en
`.gitignore`: nunca se sube. Kinesis cobra por hora mientras exista el stream (~USD 0,72 al día).

## Rama y PR

Todo el Lab 2 va en la rama `lab2`, creada desde el `main` del profesor. La entrega del Lab 1 (PR #7) sale
de `main` y no se toca. Al terminar, se abre un PR nuevo de `lab2` hacia `asacrea/big-data-labs-2026-2:main`.
