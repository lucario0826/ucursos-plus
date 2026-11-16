# UCursos+

Wrapper moderno y multiplataforma (Móvil y Escritorio) para [u-cursos.cl](https://www.u-cursos.cl) con arquitectura *Zero-Server* y modelo de plugins inyectados.

## 🚀 Visión General
**UCursos+** respeta la interfaz nativa original de U-Cursos, inyectando herramientas avanzadas y mejoras visuales directamente en el flujo de trabajo del estudiante, garantizando privacidad total y cero costos de infraestructura.

## 🛠️ Tecnologías Principales
- **Core / Host:** [Tauri v2](https://v2.tauri.app/) (Rust) - Multiplataforma (Android, iOS, Windows, macOS, Linux).
- **Inyección y UI:** TypeScript / CSS nativo respetando el diseño institucional de U-Cursos.
- **Filosofía de Seguridad:** *Cero credenciales en servidor*. Todas las cookies, tareas y notas se procesan exclusivamente en el dispositivo del usuario.

## 📦 Funcionalidades (v1.0)
1. **Calculadora de Notas Automática:**
   - Inyectada directamente en la tabla de notas de cada curso.
   - Ponderaciones configurables y nota objetivo deseada.
   - Cálculo automático de notas necesarias en evaluaciones restantes.
2. **Notificador de Tareas Pendientes:**
   - Monitoreo en segundo plano de tareas pendientes no entregadas.
   - Alertas y notificaciones nativas del sistema operativo antes del vencimiento.
3. **Ajustes Integrados:**
   - Panel de control de UCursos+ inyectado de forma nativa en la sección de Preferencias/Configuración de U-Cursos.

Para más detalles sobre la arquitectura de software y el ciclo de vida de los plugins, consulta [ARCHITECTURE.md](ARCHITECTURE.md).
