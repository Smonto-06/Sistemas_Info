# Despliegue

**NOC Redes** · Universidad EAFIT · Curso Sistemas de Información 2026-2

---

## 1. Ambiente

| Aspecto | Descripción |
|---|---|
| **Tipo de ambiente** | Prototipo académico de demostración |
| **Proveedor principal** | Vercel — plan gratuito |
| **Ambiente de respaldo** | GitHub Pages |
| **URL principal** | https://sis-info-nine.vercel.app |
| **URL de respaldo** | https://smonto-06.github.io/Sistemas_Info/ |
| **Autorizado por** | *(pendiente de confirmación del contacto de la empresa — ver sección de limitaciones del informe)* |
| **Datos utilizados** | Simulados. No se emplea información operativa de la Universidad |
| **Credenciales** | No aplica: acceso público de solo lectura |

### Por qué un ambiente propio y no de la empresa

La plantilla establece un orden de preferencia: ambiente de la empresa, ambiente académico o
gratuito del equipo, y ejecución local. Se optó por el **segundo** porque la empresa no facilitó
infraestructura dentro del plazo del proyecto.

Esta elección es además coherente con la otra restricción de la plantilla: *"en ningún caso se
deben usar datos reales de la empresa sin autorización"*. Un prototipo con datos simulados,
alojado fuera de la red institucional, no expone ninguna información sensible.

---

## 2. Procedimiento de despliegue

El despliegue es **continuo**: cualquier cambio publicado en la rama `main` del repositorio se
publica solo, sin pasos manuales.

```
  Repositorio GitHub (rama main)
            │
            │  cada push dispara la compilación
            ▼
  Vercel  ──────────►  https://sis-info-nine.vercel.app
            │
            └──────►  GitHub Pages (respaldo)
```

### Pasos de la configuración inicial

1. Subir `index.html` y `README.md` a la raíz del repositorio
2. En Vercel: *Add New → Project → Import* del repositorio `Smonto-06/Sistemas_Info`
3. Sin configuración adicional: al ser HTML estático, Vercel lo detecta automáticamente
4. *Deploy*

No hay proceso de compilación, variables de entorno ni dependencias que instalar. La aplicación
es un único archivo HTML con el CSS y el JavaScript incorporados.

### Para publicar un cambio

Subir el archivo modificado a `main`. Vercel genera un despliegue nuevo en menos de un minuto y
conserva el anterior, de modo que se puede volver atrás con un clic si algo sale mal.

---

## 3. Coherencia con la arquitectura diseñada

| Aspecto | Diseñado (entrega 2) | Desplegado | Diferencia |
|---|---|---|---|
| Capa de presentación | Aplicación web | Aplicación web de página única | Ninguna |
| Capa de integración | Fuentes reales de red | No implementada | **Sí** — el prototipo usa datos simulados |
| Capa de datos | Base de datos | Modelo en memoria | **Sí** — sin persistencia entre sesiones |
| Infraestructura | GitHub Pages | Vercel + GitHub Pages | **Sí** — ver justificación abajo |

### Justificación del cambio de infraestructura

En la entrega 2 el diagrama de arquitectura se corrigió para retirar Vercel y dejar GitHub Pages.
En esta entrega se volvió a Vercel.

El motivo es que la §4.3 pide documentar la **configuración del ambiente** y el procedimiento de
despliegue. Vercel expone ambos de forma explícita —proyecto, rama de origen, dominio asignado y
despliegue continuo— y permite revertir a una versión anterior. Se mantuvieron ambos ambientes
activos, de modo que la solución sigue accesible si uno de los dos falla durante la evaluación.

### Sobre las capas no implementadas

La integración y la persistencia quedaron fuera del alcance acordado para esta fase. El objetivo
de esta entrega era validar **el proceso rediseñado y la utilidad de la información**, no sustituir
la operación real. Conectar las fuentes reales exige accesos a la infraestructura de red que
corresponden a una fase posterior y requieren autorización del área.

---

## 4. Verificación del despliegue

Comprobaciones realizadas sobre el ambiente publicado:

| Comprobación | Resultado |
|---|---|
| La URL responde públicamente | HTTP 200 |
| Se sirve la versión con las 7 historias | 54.765 bytes |
| Las 8 vistas cargan contenido | Verificado |
| Funciona sin conexión tras la primera carga | Sin recursos externos |
| El ambiente de respaldo responde | HTTP 200, misma versión |
| Certificado TLS válido | Sí, provisto por Vercel |

---

## 5. Continuidad

Si el equipo deja el proyecto, la aplicación sigue publicada: no depende de ningún equipo
encendido ni de una suscripción de pago. Para retomarla basta con el acceso al repositorio, donde
está todo el código fuente y esta documentación.
