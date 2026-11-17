# Manual de usuario — NOC Redes

**Plataforma de Monitoreo y Automatización de Infraestructura de Red**
Universidad EAFIT · Área de Infraestructura TI – Redes

---

## 1. Acceso

La plataforma es una aplicación web. No requiere instalación ni usuario y contraseña.

| | |
|---|---|
| **Dirección** | https://sis-info-nine.vercel.app |
| **Navegadores** | Chrome, Edge, Firefox y Safari en versiones recientes |
| **Dispositivos** | Computador, tableta y teléfono (la interfaz se adapta) |
| **Conexión** | Necesaria para abrir la página. Una vez cargada sigue funcionando sin red |

La navegación se hace desde la barra lateral izquierda. En pantallas pequeñas esa barra se convierte en una fila de pestañas en la parte superior.

---

## 2. Resumen operativo

Es la pantalla inicial y responde a la pregunta *"¿cómo está la red ahora mismo?"*.

- **Disponibilidad**: promedio de las últimas 24 horas. Se compara contra el objetivo de servicio del 99 %.
- **Equipos activos**: cuántos switches y puntos de acceso se vigilan y cuántos tienen novedad.
- **Incidentes abiertos**: casos sin cerrar, con cuántos son de prioridad alta.
- **Horas/mes liberadas**: estimación del tiempo manual que la plataforma evita.

Debajo hay una gráfica de disponibilidad por hora con la línea del umbral, y una lista de actividad reciente generada por el propio sistema.

---

## 3. Monitoreo

Muestra el estado de cada equipo: tipo, ubicación, dirección IP, latencia, estado y hora de la última respuesta.

**Estados posibles:**

| Estado | Significado |
|---|---|
| En línea | El equipo responde con normalidad |
| Degradado | Responde, pero con latencia por encima del umbral de 80 ms |
| Sin respuesta | No contesta. Genera una alerta automática |

**Para cambiar la frecuencia de consulta** use el desplegable *Sondeo*. En una demostración conviene ponerlo en 4 segundos para ver el comportamiento; en operación real, 5 minutos.

**El botón *Sondear ahora*** fuerza una consulta inmediata sin esperar al siguiente ciclo.

---

## 4. Alertas

Se generan solas cuando un equipo deja de responder. Cada alerta indica el equipo, su ubicación y la hora.

**Qué puede hacer:**

- **Escalar a incidente**: convierte la alerta en un caso con identificador, responsable y reloj de servicio. Úselo cuando la caída requiera intervención.
- **Marcar todas como vistas**: limpia la bandeja sin crear incidentes. Úselo cuando la causa ya se conoce.

El filtro superior permite ver solo las no atendidas.

---

## 5. Incidentes

Registro de los casos en curso y cerrados.

**La columna SLA es la importante.** Indica cuánto margen queda antes de incumplir el tiempo de atención comprometido:

| Prioridad | Tiempo de atención |
|---|---|
| Alta | 4 horas |
| Media | 8 horas |
| Baja | 24 horas |

El sistema avisa **antes** de incumplir, no después: cuando quedan menos de dos horas la etiqueta cambia a color ámbar.

**Exportar CSV** descarga el listado completo para análisis o informes.

---

## 6. Reportes

Genera un informe de desempeño para el período que elija: hoy, 7 días o 30 días.

Incluye disponibilidad media, número de incidentes, tiempo medio de resolución y el equipo más inestable del período, además del detalle equipo por equipo.

- **Exportar CSV** para trabajarlo en Excel.
- **Imprimir / PDF** genera una versión lista para archivar o enviar.

---

## 7. Inventario

Listado de equipos con su modelo, serie, ubicación, versión de firmware y vencimiento de garantía.

**La columna *Calidad del dato* es la diferencia con un inventario corriente.** El sistema revisa cada registro y señala cuatro tipos de problema:

- Número de serie faltante
- Número de serie duplicado en dos equipos
- Firmware no reportado
- Garantía vencida

Esas observaciones **se muestran en vez de ocultarse**, porque un inventario con datos incorrectos que parece correcto es peor que uno que reconoce sus vacíos.

Use el filtro *Solo con observaciones* para trabajar la lista de pendientes.

---

## 8. Logs

Reúne en un solo flujo los registros de cuatro fuentes: syslog del núcleo, la controladora inalámbrica, netflow y las trampas SNMP.

**Patrones detectados**: cuando un mismo mensaje se repite cuatro veces o más sobre el mismo equipo, el sistema lo agrupa y lo muestra arriba como un único patrón. Eso evita revisar cientos de líneas sueltas para descubrir que son el mismo problema.

El filtro de severidad permite quedarse solo con los errores. El botón *Pausar* detiene la llegada de eventos nuevos para poder leer con calma.

---

## 9. Ocupación de aulas

Muestra la ocupación estimada de cada aula a partir de los sensores ESP32.

| Etiqueta | Significado |
|---|---|
| Alta | Más del 70 % de la capacidad |
| Normal | Entre 35 % y 70 % |
| Subutilizada | Menos del 35 % |
| **Sensor caído** | Sin reporte en más de 15 minutos |

**La distinción entre "aula vacía" y "sensor caído" es deliberada.** Confundirlas es lo que invalida este tipo de medición: un sensor que dejó de reportar se vería como un aula desocupada y llevaría a decisiones equivocadas sobre asignación de espacios.

---

## 10. Advertencia sobre los datos

Esta versión es un **prototipo académico con datos simulados**. No se conecta a la infraestructura real de la Universidad ni utiliza información operativa.

Para una puesta en producción haría falta integrar las fuentes reales (SNMP, la controladora inalámbrica y los sensores), implementar autenticación con las credenciales institucionales y definir la política de retención de los registros.

---

*Universidad EAFIT · Curso Sistemas de Información · 2026-2*
