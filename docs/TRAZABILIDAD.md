# Matriz de trazabilidad

**NOC Redes** · Universidad EAFIT · Curso Sistemas de Información 2026-2

Cada fila puede seguirse desde el diagnóstico de la entrega 2 hasta la evidencia de
funcionamiento en el ambiente desplegado. Los códigos `D##` y `P##` son los de los instrumentos
de la entrega 2.

---

## 1. De la brecha a la evidencia

| Brecha / Proceso | Actividad TO BE | HU | Componente | Evidencia funcional | Estado |
|---|---|---|---|---|---|
| **D09** · P01 | Consultar estado de switches y puntos de acceso de forma automática y periódica | HU-01 | Motor de sondeo · vista Monitoreo | Vista *Monitoreo*: 14 equipos con estado, latencia y hora de última respuesta | Desplegada |
| **D09** · P01 | Notificar la caída en menos de un minuto, sin intervención | HU-02 | Generador de alertas · vista Alertas | Vista *Alertas*: alerta con equipo, ubicación y hora | Desplegada |
| **D08** · P02 | Generar el reporte de desempeño de forma programada | HU-03 | Motor de reportes · exportador CSV | Vista *Reportes*: períodos de 1, 7 y 30 días, exportable | Desplegada |
| **D09** · P03 | Registrar el incidente con responsable y medir el tiempo de atención | HU-04 | Gestor de incidentes · reloj de SLA | Vista *Incidentes*: ticket, prioridad, responsable y margen de SLA | Desplegada |
| **D12** · P04 | Validar la calidad del dato del inventario al actualizarlo | HU-05 | Validador de inventario | Vista *Inventario*: 6 registros con observaciones detectadas | Desplegada |
| **D12** · P05 | Consolidar los registros de varias fuentes y agrupar lo repetido | HU-06 | Consolidador de logs · detector de patrones | Vista *Logs*: 4 fuentes unificadas, patrones agrupados | Desplegada |
| **D07** · P08 | Medir la ocupación de aulas y distinguir aula vacía de sensor caído | HU-07 | Panel de ocupación | Vista *Ocupación*: 8 aulas, 1 sensor marcado como caído | Desplegada |
| **D10** · P06 | Programar y hacer seguimiento a las actualizaciones de firmware | — | — | Fuera del alcance de esta fase | Fase 2 |
| **D07** · P07 | Gestionar solicitudes de habilitación de puntos de red y VLAN | — | — | Fuera del alcance de esta fase | Fase 2 |

---

## 2. Qué resuelve cada brecha

| Código | Brecha identificada en la entrega 2 | Cómo la ataca la solución |
|---|---|---|
| **D07** | Los procesos no se ejecutan de manera estandarizada | El sondeo, la generación de alertas y los reportes siguen siempre la misma secuencia, sin depender de quién esté de turno |
| **D08** | Baja proporción de procesos con automatización | Seis de los ocho procesos levantados quedan total o parcialmente soportados |
| **D09** | No se miden tiempos de ciclo ni cuellos de botella | El reloj de SLA mide el tiempo de atención de cada incidente; el reporte calcula el tiempo medio de resolución. **Hoy ese dato no existe** |
| **D10** | No hay mecanismo formal de mejora continua | Los reportes periódicos y el histórico de disponibilidad dan la base de medición que una mejora continua necesita |
| **D12** | No se mide ni gestiona la calidad de los datos | El inventario valida completitud, duplicados y vigencia, y muestra las observaciones en vez de ocultarlas |

---

## 3. Del proceso al tiempo recuperado

Horas/mes de trabajo manual según el levantamiento de la entrega 2.

| Proceso | Horas/mes | HU que lo soporta | ¿Cubierto? |
|---|---|---|---|
| P01 Monitoreo de disponibilidad y alertas | 60 | HU-01 · HU-02 | ✔ |
| P08 Ocupación de aulas (ESP32) | 45 | HU-07 | ✔ |
| P02 Reportes de desempeño | 40 | HU-03 | ✔ |
| P05 Consolidación de logs | 30 | HU-06 | ✔ |
| P03 Incidentes de conectividad | 28 | HU-04 | ✔ |
| P04 Inventario de switches y AP | 20 | HU-05 | ✔ |
| P07 Habilitación de puntos de red y VLAN | 12 | — | Fase 2 |
| P06 Actualizaciones de firmware | 5 | — | Fase 2 |
| **Total levantado** | **240** | | |
| **Cubierto por esta entrega** | **223** | | **93 %** |

---

## 4. Cobertura de las historias de usuario

| HU | Descripción | Sprint | Estado |
|---|---|---|---|
| HU-01 | Monitoreo automático de disponibilidad | 1 | Desplegada |
| HU-02 | Alertas automáticas de incidentes | 1 | Desplegada |
| HU-03 | Reportes de desempeño programados | 1 | Desplegada |
| HU-04 | Registro y trazabilidad de incidentes con SLA | 2 | Desplegada |
| HU-05 | Inventario actualizado con control de calidad | 2 | Desplegada |
| HU-06 | Consolidación de logs | 2 | Desplegada |
| HU-07 | Panel de ocupación de aulas | 2 | Desplegada |

**7 de 7 historias del backlog implementadas y desplegadas.**

---

## 5. Cómo verificar cada fila

Todas las evidencias son comprobables en `https://sis-info-nine.vercel.app` sin credenciales:

1. **HU-01** → vista *Monitoreo*, cambiar el sondeo a 4 s y observar la actualización
2. **HU-02** → vista *Alertas*, esperar una caída o forzarla con *Sondear ahora*
3. **HU-03** → vista *Reportes*, cambiar el período y exportar
4. **HU-04** → vista *Incidentes*, filtrar por *Abierto* y revisar la columna SLA
5. **HU-05** → vista *Inventario*, filtrar *Solo con observaciones*
6. **HU-06** → vista *Logs*, revisar el bloque de patrones detectados
7. **HU-07** → vista *Ocupación*, localizar el aula con el sensor caído
