# Sistema Digital de Citas Médicas

## 1. Descripción general

El **Sistema Digital de Citas Médicas** es una propuesta de software orientada a facilitar la solicitud, organización y consulta de citas médicas. El proyecto se desarrolló académicamente durante la asignatura Ingeniería de Software I, documentando sus requisitos, modelos UML, arquitectura inicial y seguimiento de tareas.

> **Estado actual:** versión inicial de documentación y diseño. Este repositorio consolida la base documental del proyecto; no contiene todavía una aplicación funcional implementada ni pruebas de software ejecutadas. Las funcionalidades descritas son objetivos del sistema y deben validarse durante la implementación.

## 2. Problema que busca resolver

La coordinación manual de citas puede provocar confusiones en los horarios, dificultades para consultar la disponibilidad, pérdida de información y poca claridad sobre las citas anteriores. El sistema propone centralizar estos procesos para que los pacientes puedan consultar horarios y gestionar sus citas de forma más ordenada.

## 3. Objetivo

Diseñar una solución digital que permita organizar la gestión de citas médicas, separando la interfaz, las reglas del negocio y el almacenamiento de datos, con una estructura que pueda implementarse y mantenerse por etapas.

## 4. Funcionalidades principales previstas

- Registro de usuarios e inicio de sesión.
- Consulta de horarios disponibles.
- Creación, modificación y cancelación de citas.
- Consulta del historial de citas.
- Notificaciones y recordatorios de citas.
- Validación de formularios y control de acceso.
- Protección de los datos personales mediante medidas de seguridad apropiadas.

Estas funcionalidades representan el alcance previsto. Su presencia en esta lista no significa que ya estén programadas.

## 5. Arquitectura seleccionada

Se eligió como diseño inicial una **arquitectura por capas con separación frontend/backend**. La propuesta distingue la presentación, la lógica de negocio y el acceso a los datos. Esta separación facilita comprender las responsabilidades, probar los componentes por separado y realizar cambios sin mezclar toda la lógica en una sola parte.

### Organización frontend/backend

**Frontend (interfaz del usuario)**

- Presenta las pantallas de registro, inicio de sesión, horarios, citas e historial.
- Recoge las acciones y datos introducidos por el usuario.
- Realiza validaciones básicas de interfaz y muestra mensajes de resultado o error.
- Envía solicitudes al backend y presenta las respuestas recibidas.

**Backend (lógica y servicios)**

- Expone los servicios que permiten registrar usuarios y gestionar citas.
- Aplica las reglas del negocio, valida los datos recibidos y comprueba los permisos.
- Coordina la autenticación y autorización.
- Consulta y actualiza la base de datos.
- Devuelve respuestas claras al frontend, incluidos los errores controlados.

**Comunicación propuesta**

El frontend se comunicaría con el backend mediante una API HTTP, preferiblemente HTTPS en un entorno real, intercambiando datos en formato JSON. El backend verificaría cada solicitud, ejecutaría las reglas correspondientes y accedería a la base de datos cuando fuera necesario. Las credenciales y los datos sensibles no deben confiarse únicamente a validaciones del frontend.

La tecnología concreta para implementar la interfaz, la API y la base de datos queda pendiente de selección y validación técnica. Esta descripción documenta la arquitectura propuesta, no una integración ya construida.

## 6. Herramientas utilizadas

- **GitHub:** repositorio y control de cambios documentales.
- **GitHub Issues:** registro y seguimiento de tareas, mejoras y riesgos.
- **GitHub Projects:** organización visual del trabajo por estado.
- **Visual Paradigm Online:** elaboración de modelos UML y del diseño arquitectónico.
- **Markdown:** documentación del proyecto dentro del repositorio.

## 7. Organización documental

- `README.md`: presentación, alcance y arquitectura general.
- `docs/REGISTRO-DE-CAMBIOS.md`: resumen de cinco avances o ajustes documentados.
- `docs/NOTA-TECNICA-DE-VERSION.md`: contenido de la versión inicial, límites y siguientes pasos.
- `docs/REQUISITOS.md`: resumen inicial de requisitos funcionales y no funcionales.
- `docs/ARQUITECTURA.md`: descripción ampliada de componentes y comunicación.

Los diagramas UML originales y las capturas de GitHub Projects deben incorporarse como evidencias cuando estén disponibles. No se consideran incluidos en el repositorio hasta que sus archivos o enlaces se agreguen expresamente.

## 8. Diagramas del sistema

Se incorporaron **reconstrucciones documentales** de los diagramas a partir de la información del proyecto que se pudo recuperar. Son fuentes editables guardadas en el repositorio; no deben presentarse como capturas originales de Visual Paradigm. Antes de una entrega que exija evidencias originales, conviene compararlas con los diagramas del proyecto de Visual Paradigm y ajustar cualquier diferencia.

- [Diagrama de casos de uso (PlantUML)](docs/uml/01-casos-de-uso.puml)
- [Diagrama de clases (Mermaid)](docs/uml/02-diagrama-de-clases.mmd)
- [Diagrama de secuencia para agendar una cita (Mermaid)](docs/uml/03-diagrama-de-secuencia.mmd)
- [Diagrama de actividad para agendar una cita (Mermaid)](docs/uml/04-diagrama-de-actividad.mmd)
- [Diagrama de arquitectura inicial (Mermaid)](docs/uml/05-diagrama-de-arquitectura.mmd)

Los archivos Mermaid pueden revisarse directamente en GitHub y editarse como texto. El diagrama de casos de uso está en formato PlantUML para conservar la notación UML de actores y casos de uso.

## 9. Estado actual y próximos pasos

El proyecto se encuentra en una etapa de diseño y documentación. Hay Issues registrados para representar tareas iniciales y pendientes; la arquitectura inicial aparece documentada en el seguimiento del repositorio. No se debe considerar completada una funcionalidad solo por tener un Issue o una descripción.

Próximos pasos técnicos:

1. Comparar y validar las reconstrucciones UML con los diagramas del proyecto original.
2. Confirmar el estado real de cada tarea en GitHub Projects y mantenerlo alineado con sus Issues.
3. Elegir tecnologías concretas para frontend, backend y base de datos.
4. Implementar primero autenticación y gestión básica de citas.
5. Preparar pruebas funcionales y de seguridad antes de considerar una versión ejecutable.

## 10. Control de versión documental

**Versión documental:** 0.1.0  
**Tipo:** línea base inicial de documentación y diseño.  
**Alcance:** descripción del problema, funcionalidades previstas, arquitectura conceptual y planificación del seguimiento.  
**Limitación:** esta versión no representa una aplicación funcional desplegada.

Consulta el [registro de cambios](docs/REGISTRO-DE-CAMBIOS.md), la [nota técnica de versión](docs/NOTA-TECNICA-DE-VERSION.md), los [requisitos iniciales](docs/REQUISITOS.md) y la [arquitectura propuesta](docs/ARQUITECTURA.md).
