# Arquitectura de la solución

**NOC Redes** · Universidad EAFIT · Área de Infraestructura TI – Redes

Este documento describe la arquitectura **de lo que realmente se desplegó**, no de una solución
ideal. Donde hay diferencia con lo diseñado en la entrega 2, se señala y se explica.

---

## 1. Arquitectura por capas

```
┌──────────────────────────────────────────────────────────────┐
│  PRESENTACIÓN                                                │
│  Aplicación web de página única · HTML + CSS + JavaScript    │
│  8 vistas: resumen, monitoreo, alertas, incidentes,          │
│  reportes, inventario, logs y ocupación                      │
└──────────────────────────────────────────────────────────────┘
                              │
┌──────────────────────────────────────────────────────────────┐
│  APLICACIÓN / LÓGICA DE NEGOCIO                              │
│  Reglas ejecutadas en el navegador:                          │
│  · ciclo de sondeo y clasificación de estado                 │
│  · generación de alertas ante no-respuesta                   │
│  · cálculo de SLA y detección de riesgo de incumplimiento    │
│  · validación de calidad del inventario                      │
│  · agrupación de registros en patrones                       │
└──────────────────────────────────────────────────────────────┘
                              │
┌──────────────────────────────────────────────────────────────┐
│  INTEGRACIÓN                                                 │
│  No implementada en el prototipo. Prevista para producción:  │
│  SNMP, controladora inalámbrica, syslog y sensores ESP32     │
└──────────────────────────────────────────────────────────────┘
                              │
┌──────────────────────────────────────────────────────────────┐
│  DATOS                                                       │
│  Modelo en memoria con generador determinista por semilla    │
│  Exportación a CSV · sin persistencia entre sesiones         │
└──────────────────────────────────────────────────────────────┘
                              │
┌──────────────────────────────────────────────────────────────┐
│  INFRAESTRUCTURA Y DESPLIEGUE                                │
│  Vercel (principal) · GitHub Pages (respaldo)                │
│  Despliegue continuo desde la rama main del repositorio      │
└──────────────────────────────────────────────────────────────┘
```

### Detalle por capa

| Capa | Componentes | Tecnología | Responsabilidad |
|---|---|---|---|
| **Presentación** | Aplicación web de página única, responsiva | HTML5, CSS3, JavaScript ES6 | Interfaz, navegación entre vistas, gráficos SVG generados en el cliente |
| **Aplicación** | Motor de sondeo, generador de alertas, control de SLA, validador de inventario, agrupador de patrones | JavaScript | Reglas de negocio del dominio de monitoreo |
| **Integración** | *No aplica en el prototipo* | — | Prevista: SNMP v3, API de la controladora, syslog, MQTT para los ESP32 |
| **Datos** | Modelo en memoria, exportación CSV | JavaScript | Catálogo de 14 equipos, incidentes, registros y 8 aulas |
| **Infraestructura** | Hospedaje estático con despliegue continuo desde el repositorio | Vercel · GitHub Pages | Publicación, certificado TLS, reversión a versión anterior |
| **Seguridad** *(transversal)* | HTTPS, sin datos personales, sin credenciales en el código | Vercel / GitHub | Ver sección 3 |
| **Operación** *(transversal)* | Historial de despliegues, reversión a versión anterior | Vercel | Trazabilidad de los cambios publicados |

---

## 2. Decisiones de arquitectura

| Decisión | Alternativas consideradas | Justificación |
|---|---|---|
| **Aplicación de página única sin dependencias externas** | React, Vue, Bootstrap, Chart.js desde CDN | Elimina el riesgo de que un CDN falle durante la sustentación, carga al instante y permite que la aplicación funcione sin conexión una vez abierta. Para ocho vistas no se justificaba un framework |
| **Gráficos en SVG generados por código** | Chart.js, D3, imágenes estáticas | Sin librería externa, escalan sin perder nitidez y se imprimen bien en el PDF del reporte |
| **Datos simulados con generador de semilla fija** | Datos aleatorios, datos reales | Con semilla fija las cifras son **reproducibles**: no cambian entre recargas, lo que permite demostrar y documentar con números estables. Los datos reales exigirían autorización del área |
| **Vercel como ambiente principal** | GitHub Pages únicamente, servidor de la empresa | La empresa no facilitó infraestructura. Vercel expone de forma explícita la **configuración del ambiente** —rama de origen, dominio y despliegue continuo— y permite revertir a una versión anterior |
| **Lógica en el cliente, sin servidor** | API en Node o Python con base de datos | Para un prototipo de validación, un servidor añade costo, mantenimiento y una superficie de seguridad sin aportar nada a lo que se quiere demostrar |

### Cambio frente a la entrega 2

En la entrega 2 el diagrama de arquitectura se corrigió para **retirar Vercel** y dejar la
aplicación en GitHub Pages. En esta entrega se volvió a Vercel como ambiente principal.

**Motivo:** la §4.3 pide describir el procedimiento de despliegue. Vercel conserva un historial
de despliegues con fecha y commit asociado, que constituye evidencia verificable; GitHub Pages no
lo expone. GitHub Pages se mantiene activo como ambiente de respaldo, de modo que la solución
queda publicada en dos lugares.

---

## 3. Seguridad y tratamiento de datos

### Qué datos maneja

**Ninguno personal.** El prototipo trabaja con datos simulados de equipos de red: nombres,
direcciones IP privadas, modelos y números de serie ficticios. Los nombres que aparecen como
responsables de incidente son de fantasía.

No se recogen, almacenan ni transmiten datos de personas identificables, por lo que **no hay
tratamiento de datos personales en el sentido de la Ley 1581 de 2012**.

### Acceso y autenticación

El prototipo es de acceso público y de solo lectura: no permite modificar información persistente.
No requiere autenticación porque no hay nada que proteger.

**Para producción** sería obligatorio: autenticación con las credenciales institucionales,
perfiles diferenciados (operador, consulta, administrador) y registro de auditoría de las acciones
que modifiquen incidentes.

### Credenciales

No hay credenciales, tokens ni cadenas de conexión en el código. Se verificó **el historial
completo** del repositorio, no solo la versión actual, porque un secreto eliminado en un commit
posterior permanece recuperable. Resultado: sin hallazgos.

### Datos de la empresa

Conforme a la restricción de la plantilla, **no se utilizó información operativa real de la
Universidad sin autorización**. Los volúmenes de los procesos citados en los indicadores provienen
del levantamiento documentado en la entrega 2.

---

## 4. Lo que faltaría para producción

| Elemento | Estado | Qué implicaría |
|---|---|---|
| Integración con fuentes reales | No implementado | Agentes SNMP, API de la controladora, receptor de syslog, broker MQTT |
| Persistencia | No implementado | Base de datos de series temporales para el histórico |
| Autenticación | No implementado | Integración con el directorio institucional |
| Notificación externa | No implementado | Correo o mensajería para las alertas fuera de la aplicación |
| Retención de registros | No definido | Política de cuánto tiempo se conservan los logs |

Reconocer este límite es parte del diseño: lo entregado valida **el proceso rediseñado y la
utilidad de la información**, que es lo que había que verificar antes de invertir en la
integración real.

