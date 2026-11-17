# Plan y resultados de pruebas

**NOC Redes** · Universidad EAFIT · Curso Sistemas de Información 2026-2

Este documento recoge las pruebas realizadas sobre el prototipo antes de darlo por terminado.

---

## 1. Alcance

Se probaron las siete historias de usuario implementadas, sobre el ambiente desplegado en
`https://sis-info-nine.vercel.app`.

**Qué no se probó:** carga con muchos usuarios simultáneos, compatibilidad con navegadores
antiguos, e integración con fuentes de datos reales — el prototipo trabaja sobre datos simulados.

---

## 2. Pruebas automatizadas de la interfaz

Antes de publicar se ejecutó una prueba de humo que carga la página completa en un navegador
simulado, recorre las ocho vistas, acciona los botones y filtros, y comprueba que ningún
contenedor quede vacío y que no se produzcan errores de ejecución.

### Resultado

```
monitoreo   : 14 equipos · 13 en línea
incidentes  : cumplimiento de SLA 60 % · tiempo medio de cierre 3,2 h
reportes    : 14 filas · disponibilidad 98,76 %
inventario  : 6 registros con observaciones · calidad 57 %
logs        : 121 eventos · 19 errores · 2 patrones detectados
aulas       : 8 · ocupación media 49 % · 1 sensor caído
gráficos    : 4 SVG dibujados

→ sin errores de ejecución; las 8 vistas pintan contenido
```

### Dos defectos encontrados y corregidos

Esta prueba no fue un trámite: encontró dos indicadores que comunicaban algo falso.

**1. Disponibilidad engañosa.** El resumen mostraba 98,9 % unas veces y 92,9 % otras, porque
calculaba el estado del instante: con catorce equipos, uno caído hace caer el indicador siete
puntos. Un acuerdo de nivel de servicio no se mide así. **Se corrigió** para que calcule el
promedio de las últimas 24 horas.

**2. Inventario irreal.** Más de la mitad de los equipos aparecían con la garantía vencida, lo
que daba la impresión de un inventario abandonado en vez de un control de calidad funcionando.
**Se corrigieron** las fechas de los datos simulados.

---

## 3. Pruebas funcionales por historia de usuario

| HU | Caso probado | Resultado esperado | Resultado |
|---|---|---|---|
| HU-01 | Cambiar el intervalo de sondeo a 4 s | Los estados y la hora de última respuesta se actualizan solos | ✔ |
| HU-01 | Pulsar *Sondear ahora* | Consulta inmediata sin esperar el ciclo | ✔ |
| HU-02 | Forzar sondeos hasta que un equipo caiga | Se genera una alerta con equipo, ubicación y hora | ✔ |
| HU-02 | Escalar una alerta a incidente | Aparece un ticket nuevo en la vista de incidentes | ✔ |
| HU-03 | Generar reporte de 7 y de 30 días | Cambian la gráfica y los indicadores | ✔ |
| HU-03 | Exportar CSV | Se descarga un archivo con separador `;`, legible en Excel en español | ✔ |
| HU-04 | Filtrar por estado *Abierto* | La tabla muestra solo los abiertos | ✔ |
| HU-04 | Revisar un incidente con menos de 2 h de margen | La etiqueta de SLA cambia a advertencia | ✔ |
| HU-05 | Filtrar *Solo con observaciones* | Se listan los 6 registros con defectos | ✔ |
| HU-05 | Verificar la detección de serie duplicada | Se señalan los dos equipos que comparten serie | ✔ |
| HU-06 | Filtrar por severidad *ERROR* | Solo se muestran errores | ✔ |
| HU-06 | Pausar el flujo | Deja de llegar eventos nuevos | ✔ |
| HU-07 | Revisar el aula con sensor caído | Se muestra "sin dato", no "0 %" | ✔ |

---

## 4. Pruebas de despliegue

| Prueba | Resultado |
|---|---|
| La URL responde públicamente | ✔ HTTP 200 |
| Se sirve la versión con las 7 HU | ✔ 54.765 bytes |
| Funciona sin conexión tras la primera carga | ✔ no usa recursos externos |
| El ambiente de respaldo responde | ✔ GitHub Pages sirve la misma versión |

---

## 5. Revisión de seguridad del repositorio

Se revisó **el historial completo** del repositorio —no solo los archivos actuales— en busca de
credenciales: tokens de GitHub, claves de AWS, claves privadas, contraseñas en código, cadenas de
conexión y cabeceras de autorización.

```
6 commits · 122 KB de diferencias analizadas
TOTAL: 0 hallazgos
```

Esta revisión importa porque un secreto eliminado en un commit posterior **permanece en el
historial** y sigue siendo recuperable.

---

## 6. Pruebas de aceptación con el usuario

**No se realizaron**, y conviene explicar por qué en lugar de dejar la sección vacía.

Las pruebas de aceptación requieren que un usuario de la empresa ejecute los casos y declare
si el resultado es el esperado. El equipo solicitó esa validación por escrito al contacto del
proyecto, con el enlace al ambiente desplegado y una lista de preguntas cerradas:

| Fecha | Canal | Destinatario | Resultado |
|---|---|---|---|
| 15/11/2026 | Correo | Contacto del proyecto | Sin respuesta |
| 17/11/2026 | Seguimiento por canal alterno | Contacto del proyecto | Sin respuesta |

A la fecha de cierre no se obtuvo respuesta. En consecuencia, **los criterios de aceptación se
verificaron internamente** contra el backlog, uno por uno, sobre el ambiente desplegado; el
detalle está en la sección 4 de este documento y en la sección 4.1 del informe.

Esta limitación queda declarada en la sección 6 del informe, con su efecto sobre las demás
secciones afectadas.

---

## 7. Conclusión

El prototipo cumple los criterios de aceptación de las siete historias sobre el ambiente
desplegado. Los dos defectos detectados eran de **interpretación de los datos**, no de
funcionamiento: la aplicación hacía lo que se le pidió, pero comunicaba una conclusión
equivocada. Ese es el tipo de error que una prueba de "¿abre la página?" no habría encontrado.

