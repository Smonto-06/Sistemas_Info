# NOC Redes — Universidad EAFIT

Proyecto del curso **Sistemas de Información** (Universidad EAFIT, 2026-2).
Empresa analizada: **Universidad EAFIT** · Área intervenida: **Infraestructura TI – Redes**.

**Plataforma de Monitoreo y Automatización de Infraestructura de Red** — prototipo funcional
que implementa las 7 historias de usuario del backlog sobre datos simulados.

### 🔗 Ver en vivo
**https://smonto-06.github.io/Sistemas_Info/**

---

## Historias de usuario implementadas

| HU | Vista | Qué demuestra | Proceso / brecha |
|---|---|---|---|
| **HU-01** | Monitoreo | Sondeo automático de switches y puntos de acceso en intervalo configurable, con latencia, estado e histórico. | P01 · 60 h/mes |
| **HU-02** | Alertas | Alerta automática ante no-respuesta en menos de un minuto, con equipo, ubicación y hora. Escalable a incidente. | P01 |
| **HU-03** | Reportes | Reporte de desempeño por período (hoy / 7 / 30 días) con disponibilidad, incidentes y tiempos. Exportable a CSV y PDF. | P02 · 40 h/mes |
| **HU-04** | Incidentes | Registro con identificador, responsable, prioridad y **reloj de SLA** que avisa antes de incumplir. | P03 · 28 h/mes · brecha **D09** |
| **HU-05** | Inventario | Inventario con **control de calidad del dato**: detecta series faltantes, series duplicadas, firmware no reportado y garantías vencidas. | P04 · 20 h/mes · brecha **D12** |
| **HU-06** | Logs | Cuatro fuentes consolidadas en un flujo único y **agrupación automática en patrones** para reducir ruido. | P05 · 30 h/mes |
| **HU-07** | Ocupación | Ocupación estimada por aula con sensores ESP32, distinguiendo **aula vacía** de **sensor caído**. | P08 · 45 h/mes |

## Características técnicas

- **Una sola página, sin dependencias externas.** No usa CDN ni librerías: funciona sin conexión.
- **Gráficos en SVG** generados en el cliente (línea, barras y columnas).
- **Datos simulados deterministas** mediante generador con semilla, de modo que las cifras son
  estables entre recargas y reproducibles en una demostración.
- **Simulación en vivo**: el sondeo, el flujo de logs y la ocupación se actualizan solos.
- Exportación a **CSV** en incidentes, reportes e inventario · impresión a PDF del reporte.
- Responsive y con hoja de estilo de impresión.

## Datos

Todos los datos son **simulados**. El prototipo no se conecta a la infraestructura real de la
Universidad ni usa información operativa: se trata de un ambiente de demostración académica,
conforme a la restricción de no utilizar datos reales sin autorización.

## Despliegue

Publicado como sitio estático en **GitHub Pages** desde la rama `main`.
Para ejecutarlo localmente basta con abrir `index.html` en un navegador.

## Backlog

GitHub Projects — https://github.com/users/Smonto-06/projects/4

## Documentos (`docs/`)

| Archivo | Contenido |
|---|---|
| `Entrega2_EAFIT.docx` | Informe de la Entrega 2 |
| `Diagnostico_Madurez_Fase2_D01.xlsx` | Diagnóstico de madurez digital — 7 dimensiones, 36 indicadores |
| `Automatizacion_Procesos_v3.xlsx` | Priorización de procesos y recomendación tecnológica |
| `AS_IS_redes_EAFIT.png` | Proceso actual (AS IS) |
| `arquitectura_capas_EAFIT.png` | Arquitectura por capas |

---

Universidad EAFIT · Escuela de Ciencias Aplicadas e Ingeniería
Curso Sistemas de Información · Profesor Juan Carlos Quintero Vallejo
