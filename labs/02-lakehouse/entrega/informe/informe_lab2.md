# Lab 2 · Lakehouse end-to-end en AWS: batch y streaming

**SI7006 Almacenamiento y Procesamiento de Grandes Datos · Maestría en Ingeniería de Datos · EAFIT 2026-2**  
**Caso:** PayTrack Colombia · **Equipo:** Luis Alberto Ortiz Quiroga · Santiago Vélez Casallas  
**Repositorio:** https://github.com/santiagovelcasallas/big-data-labs-2026-2 (rama `lab2`)

> Borrador. Se entrega en PDF, máximo 8 páginas, con las respuestas y los experimentos.
> Las preguntas son las del enunciado, literales; las evidencias van en `entrega/evidencias/`.

## Parte A · Batch

**1. Bronze.** ¿Por qué Bronze lee todo como texto? ¿Qué problema evita `replaceWhere` frente a `append`? Muéstralo con lo que pasó en tu prueba de idempotencia.

_Pendiente._

**2. Silver.** ¿Cuántas filas quedaron en cuarentena por cada motivo en cada lote? ¿Por qué se deduplica **antes** de aplicar las reglas de calidad?

_Pendiente._

**3. MERGE.** ¿Por qué la actualización solo debe ocurrir cuando el `status` cambió? ¿Qué reportaría la auditoría si quitaras esa condición y re-ejecutaras un lote?

_Pendiente._

**4. Time travel.** ¿Cuántos contracargos encontró la auditoría y qué monto revierten? ¿Qué pasaría con esta auditoría después de un `VACUUM`?

_Pendiente._

**5. PII.** `silver.customers` se actualiza sobrescribiendo los cambios (tipo 1). ¿Qué análisis de negocio se pierde? ¿Cómo lo resolverías con lo que hiciste en el Lab 1?

_Pendiente._

**6. Consumo.** Compara los MB escaneados del TODO 1 y del TODO 2 de Athena. ¿Por qué existe Gold si Silver ya responde la pregunta? ¿Qué pierdes?

_Pendiente._

## Parte B · Streaming

**7. Garantías de entrega.** ¿Qué garantía da tu productor: *at-most-once*, *at-least-once* o *exactly-once*? ¿Y Kinesis con tus reintentos? Explica qué combinación de checkpoint, Delta y `MERGE` hace que las tablas queden como si cada evento se hubiera procesado exactamente una vez. Usa tu prueba de idempotencia como evidencia.

_Pendiente._

**8. Watermark.** Responde el experimento 1. ¿Por qué la consulta `silver` no usa watermark? ¿Qué pasaría con los pagos tardíos si lo usara?

_Pendiente._

**9. Latencia.** ¿Cuánto tarda en aparecer una alerta en `gold.fraud_alerts` después del último pago de la ráfaga? ¿Qué parte de ese tiempo se debe al modo *append* y al watermark? ¿Cómo la bajarías y qué perderías?

_Pendiente._

**10. Precisión.** Reporta la precisión de las alertas (TODO 5) a 20 y a 50 eventos/s. ¿Por qué cambia? ¿Qué ajustarías para mejorarla?

_Pendiente._

**11. Estado final.** En el TODO 4, ¿qué escenario concreto del productor revertiría un contracargo si quitaras la condición sobre `'chargeback'`? ¿Por qué `latest_per_transaction` no basta para evitarlo?

_Pendiente._

**12. Partition key.** Con el experimento 3: ¿cómo se repartió la carga con cada llave? ¿Cambiaría el número de alertas que detecta Spark con `transaction_id` como llave? Si Spark agrupa por cliente de todas formas, ¿para qué sirve la partition key? (piensa en el contracargo y su pago).

_Pendiente._

**13. Batch y streaming en la misma tabla.** Revisa `DESCRIBE HISTORY` de `silver.transactions` después del streaming: ¿cuántas versiones creó?, ¿cuántas filas reescribió cada `MERGE` (`numTargetRowsCopied`)? ¿Qué problema anticipas a 500K pagos/día y cómo lo resolverías? ¿Qué pasaría si el job silver batch y el stream escribieran al mismo tiempo? Con el TODO 6 de Athena: ¿cuál es la fuente de verdad, la capa rápida o la batch?

_Pendiente._

**14. Costos y operación.** Estima el costo mensual de las dos partes con 500K transacciones diarias (S3, Glue, Glue Streaming 24/7, Kinesis y Athena). ¿Qué cambiarías si el streaming no necesitara correr 24/7? ¿Por qué no se debe poner una regla de expiración de S3 sobre `lakehouse/`?

_Pendiente._

## Experimentos (B.3)

| Experimento | Medición | Resultado |
|---|---|---|
| 1 · Watermark | Filas descartadas por watermark en `metrics`: availableNow (`--fast`) vs en vivo | _Pendiente_ |
| 2 · Carga | Alertas y precisión (TODO 5 de Athena) a 20 y a 50 eventos/s | _Pendiente_ |
| 3 · Partition key | Reparto por partición (`kafka-get-offsets.sh`) con llave constante y con `transaction_id` | _Pendiente_ |

## Anexos

- **A.** Diagrama de la arquitectura (`entrega/diagrama/`)
- **B.** Evidencias de ejecución local, AWS, Athena y limpieza (`entrega/evidencias/`)
