# NOC Redes — Universidad EAFIT

Proyecto del curso **Sistemas de Información** (Universidad EAFIT, 2026-2).
Empresa analizada: **Universidad EAFIT** · Área intervenida: **Infraestructura TI – Redes**.

**Plataforma de Monitoreo y Automatización de Infraestructura de Red** — prototipo funcional
que implementa las 7 historias de usuario del backlog sobre datos simulados.

### 🔗 Ver en vivo

| Ambiente | URL |
|---|---|
| **Principal** | **https://sis-info-nine.vercel.app** |
| Respaldo | https://smonto-06.github.io/Sistemas_Info/ |

---

## Historias de usuario implementadas

| HU | Vista | Qué demuestra | Proceso / brecha | Responsable |
|---|---|---|---|---|
| **HU-01** | Monitoreo | Sondeo automático de switches y puntos de acceso en intervalo configurable, con latencia, estado e histórico. | P01 · 60 h/mes | Samuel Montoya |
| **HU-02** | Alertas | Alerta automática ante no-respuesta en menos de un minuto, con equipo, ubicación y hora. Escalable a incidente. | P01 | Samuel Montoya |
| **HU-03** | Reportes | Reporte de desempeño por período (hoy / 7 / 30 días) con disponibilidad, incidentes y tiempos. Exportable a CSV y PDF. | P02 · 40 h/mes | Juan José Vanegas |
| **HU-04** | Incidentes | Registro con identificador, responsable, prioridad y **reloj de SLA** que avisa antes de incumplir. | P03 · 28 h/mes · brecha **D09** | Miguel Alzate |
| **HU-05** | Inventario | Inventario con **control de calidad del dato**: detecta series faltantes, series duplicadas, firmware no reportado y garantías vencidas. | P04 · 20 h/mes · brecha **D12** | Miguel Alzate |
| **HU-06** | Logs | Cuatro fuentes consolidadas en un flujo único y **agrupación automática en patrones** para reducir ruido. | P05 · 30 h/mes | Miguel Alzate |
| **HU-07** | Ocupación | Ocupación estimada por aula con sensores ESP32, distinguiendo **aula vacía** de **sensor caído**. | P08 · 45 h/mes | Juan José Vanegas |

## Equipo

| Integrante | Usuario | Rol |
|---|---|---|
| Samuel Montoya Espinosa | [@Smonto-06](https://github.com/Smonto-06) | Scrum Master · desarrollador |
| Miguel Ángel Alzate Osorno | [@Alzate4664](https://github.com/Alzate4664) | Desarrollador |
| Juan José Vanegas | [@juanjoseva2006](https://github.com/juanjoseva2006) | Product Owner · desarrollador |

**Backlog:** GitHub Projects — https://github.com/users/Smonto-06/projects/4

---

## Tecnologías

| | |
|---|---|
| **Lenguajes** | HTML5 · CSS3 · JavaScript ES6 |
| **Gráficos** | SVG generado en el cliente, sin librería |
| **Dependencias externas** | **Ninguna.** No usa CDN, npm ni framework |
| **Hospedaje** | Vercel (principal) · GitHub Pages (respaldo) |
| **Despliegue** | Continuo desde la rama `main` |

## Requisitos

Un navegador moderno: Chrome, Edge, Firefox o Safari en versión reciente.

**No se requiere nada más.** No hay proceso de compilación, ni gestor de paquetes, ni servidor,
ni variables de entorno que configurar.

## Cómo ejecutar

### En línea

Abrir https://sis-info-nine.vercel.app

### En local

```bash
git clone https://github.com/Smonto-06/Sistemas_Info.git
cd Sistemas_Info
```

Luego abrir `index.html` con doble clic, o servirlo si se prefiere:

```bash
python -m http.server 8000
# y abrir http://localhost:8000
```

Ambas formas funcionan igual: toda la lógica se ejecuta en el navegador.

## Características técnicas

- **Una sola página, sin dependencias externas.** No usa CDN ni librerías: funciona sin conexión.
- **Gráficos en SVG** generados en el cliente (línea, barras y columnas).
- **Datos simulados deterministas** mediante generador con semilla, de modo que las cifras son
  estables entre recargas y reproducibles en una demostración.
- **Simulación en vivo**: el sondeo, el flujo de logs y la ocupación se actualizan solos.
- Exportación a **CSV** en incidentes, reportes e inventario · impresión a PDF del reporte.
- Responsive y con hoja de estilo de impresión.

## Datos y seguridad

Todos los datos son **simulados**. El prototipo no se conecta a la infraestructura real de la
Universidad ni usa información operativa: se trata de un ambiente de demostración académica,
conforme a la restricción de no utilizar datos reales sin autorización.

No hay datos personales, por lo que no hay tratamiento de datos en los términos de la
Ley 1581 de 2012. El repositorio **no contiene contraseñas, tokens ni cadenas de conexión**.

## Documentos (`docs/`)

| Archivo | Contenido |
|---|---|
| `ARQUITECTURA.md` | Arquitectura por capas, decisiones y seguridad |
| `TRAZABILIDAD.md` | Matriz brecha → proceso → HU → componente → evidencia |
| `PRUEBAS.md` | Plan y resultados de pruebas |
| `MANUAL_USUARIO.md` | Manual de usuario |
| `DESPLIEGUE.md` | Procedimiento de despliegue |
| `TO_BE_P01_monitoreo.png` | Proceso rediseñado (TO BE) en notación BPMN |
| `AS_IS_redes_EAFIT.png` | Proceso actual (AS IS) |
| `arquitectura_capas_EAFIT.png` | Arquitectura por capas |
| `Entrega2_EAFIT.docx` | Informe de la Entrega 2 |
| `Diagnostico_Madurez_Fase3.xlsx` | Diagnóstico de madurez — 7 dimensiones, 36 indicadores, con esfuerzo |
| `Automatizacion_Procesos_v3.xlsx` | Priorización de procesos y recomendación tecnológica |

---

Universidad EAFIT · Escuela de Ciencias Aplicadas e Ingeniería
Curso Sistemas de Información · Profesor Juan Carlos Quintero Vallejo
