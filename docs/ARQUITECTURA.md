# Arquitectura propuesta

## Enfoque

La propuesta inicial utiliza una arquitectura por capas y separa frontend, backend y persistencia de datos. La finalidad es mantener responsabilidades claras y facilitar pruebas y mantenimiento.

## Componentes

### Frontend
Gestiona las pantallas y la interacción con el usuario: registro, autenticación, horarios, citas e historial. Envía solicitudes al backend y muestra los resultados. No debe ser la única capa encargada de aplicar controles de seguridad.

### Backend
Expone una API para las operaciones del sistema. Valida solicitudes, aplica reglas de negocio, verifica identidad y permisos, y coordina el acceso a los datos.

### Servicio de autenticación
Forma parte de la responsabilidad del backend y verifica la identidad del usuario. Las credenciales deben manejarse con prácticas seguras y nunca almacenarse como texto plano.

### Capa de datos
Almacena la información necesaria para usuarios, disponibilidad y citas. El diseño físico de la base de datos, las restricciones y las copias de seguridad quedan pendientes de definición.

## Comunicación propuesta

1. El usuario realiza una acción en el frontend.
2. El frontend envía una solicitud a la API del backend.
3. El backend valida los datos y los permisos.
4. Si la operación lo requiere, el backend consulta o modifica la base de datos.
5. El backend devuelve una respuesta y el frontend presenta el resultado.

Se propone HTTP con HTTPS en entornos reales y JSON para intercambiar datos. La tecnología concreta y los endpoints todavía no están definidos.

## Estado

Este documento describe el diseño conceptual elaborado durante la asignatura. No acredita que los componentes estén programados ni conectados. Los diagramas UML originales de Visual Paradigm deben conservarse como evidencia complementaria.
