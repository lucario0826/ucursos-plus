# Arquitectura del Sistema: UCursos+ (v1.0)

## 1. Visión y Principios de Diseño
* **Wrapper Transparente:** La app embebe la web original `u-cursos.cl` sin alterar su diseño de fondo, inyectando selectivamente estilos y componentes nativos donde sea necesario.
* **Zero-Server / Privacidad Total (v1.0):** Cero envío de datos a servidores externos. No hay proxies, bases de datos remotas ni almacenamiento de credenciales institucionales fuera del dispositivo.
* **Multiplataforma:** Móvil (Android/iOS) y Escritorio (Windows/Linux/macOS) basados en la misma base de código.

---

## 2. Stack Tecnológico
* **Host Nativo:** **Tauri v2 (Rust)**
  * Control del WebView nativo del sistema operativo.
  * Tareas en segundo plano (Background Workers) para sondeo de tareas pendientes.
  * API nativa de notificaciones locales.
  * Almacenamiento seguro persistente (Plugins/Tauri Store).
* **Capa Inyectada:** **TypeScript / Vanilla JS + CSS**
  * Script inyectado al cargar las páginas de U-Cursos.
  * Detección de rutas y ciclo de vida del DOM (vía `MutationObserver`).
  * Inyección de widgets que imitan el CSS nativo de U-Cursos.

---

## 3. Arquitectura de Inyección y Plugins

```
+-------------------------------------------------------------+
|                     Tauri v2 (Rust Host)                    |
|  - Background Fetch Worker (Monitoreo de tareas)            |
|  - API de Notificaciones Nativas                            |
|  - Almacenamiento Local (Configuración y Ponderaciones)     |
+------------------------------+------------------------------+
                               | Inyección & IPC Bridge
+------------------------------v------------------------------+
|                     WebView (u-cursos.cl)                   |
|                                                             |
|  [Core Router / Inyector]                                   |
|   |--> /notas/*       ==> Plugin: Calculadora de Notas      |
|   |--> /perfil/*      ==> Inyección en Menú Configuración   |
|                                                             |
|  [U-Cursos Original DOM]                                    |
+-------------------------------------------------------------+
```

---

## 4. Especificación de Plugins Confirmados

### A. Calculadora de Notas
* **Ubicación:** Se inyecta en `/notas/` de cada ramo.
* **Lógica:**
  * Lee la tabla de notas renderizada por U-Cursos.
  * Añade inputs interactivos para ponderaciones (%) y nota meta de aprobación.
  * Calcula y proyecta la nota mínima necesaria en las evaluaciones restantes.
* **Persistencia:** Guarda las ponderaciones por ramo localmente en el dispositivo.

### B. Sistema de Notificaciones de Tareas
* **Ubicación:** Proceso en segundo plano coordinado por Rust / Tauri.
* **Lógica:**
  * Con la cookie de sesión activa del WebView, consulta periódicamente las tareas pendientes.
  * Comprueba si el estado de la entrega está incompleto.
  * Emite notificaciones nativas en el sistema cuando falten ventanas de tiempo configurables (ej. 24h, 3h).

---

## 5. Roadmap v2.0 (Salas de Horario Compartidas)
* Integración de backend propio en **Rust (Axum + SQLite)**.
* Sistema de salas para compartir calendarios (`.ics`) entre amigos y grupos de estudio.
* Cálculo en servidor de matrices de disponibilidad horaria grupal.
