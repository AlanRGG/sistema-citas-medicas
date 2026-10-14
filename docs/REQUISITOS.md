# Requisitos iniciales

## Propósito

Este documento resume las capacidades que el Sistema Digital de Citas Médicas debe contemplar. Es una base de análisis y no una afirmación de que dichas capacidades ya estén implementadas.

## Requisitos funcionales

- **RF-01 — Registro:** permitir que un paciente cree una cuenta con los datos necesarios.
- **RF-02 — Inicio de sesión:** permitir la autenticación de usuarios registrados.
- **RF-03 — Horarios disponibles:** mostrar los horarios habilitados para solicitar una cita.
- **RF-04 — Gestión de citas:** permitir crear, consultar, modificar y cancelar citas conforme a las reglas del sistema.
- **RF-05 — Historial:** permitir consultar las citas anteriores asociadas al usuario.
- **RF-06 — Notificaciones:** contemplar recordatorios o avisos sobre citas y actualizaciones.
- **RF-07 — Validación:** comprobar que los datos obligatorios y los formatos sean válidos antes de procesarlos.

## Requisitos no funcionales iniciales

- **RNF-01 — Seguridad:** proteger las credenciales y restringir el acceso a información según permisos.
- **RNF-02 — Integridad:** evitar citas duplicadas para el mismo horario y mantener consistencia de los datos.
- **RNF-03 — Usabilidad:** ofrecer una navegación comprensible y mensajes claros.
- **RNF-04 — Mantenibilidad:** separar interfaz, reglas de negocio y acceso a datos.
- **RNF-05 — Privacidad:** limitar el acceso y uso de datos personales a lo necesario para el servicio.

## Validación pendiente

Los requisitos deberán revisarse con los interesados, transformarse en criterios de aceptación y vincularse con casos de uso y pruebas. Las tecnologías, los niveles de servicio y los controles concretos de seguridad aún deben definirse.
