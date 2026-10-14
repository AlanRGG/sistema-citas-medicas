# Diagramas del Sistema Digital de Citas Médicas

Esta página reúne las reconstrucciones editables de los diagramas del proyecto, con etiquetas y descripciones en español. Se elaboraron a partir de la información que pudimos recuperar; por eso, deben compararse con los modelos originales de Visual Paradigm antes de considerarlas equivalentes.

## 1. Diagrama de casos de uso

Representa las funciones principales disponibles para el paciente y el administrador. El archivo UML editable está en [01-casos-de-uso.puml](01-casos-de-uso.puml).

```mermaid
flowchart LR
    P[Paciente]
    A[Administrador]
    subgraph S["Sistema Digital de Citas Médicas"]
        UC1([Crear cuenta])
        UC2([Iniciar sesión])
        UC3([Consultar horarios])
        UC4([Agendar cita])
        UC5([Consultar mis citas])
        UC6([Cancelar cita])
        UC7([Recibir notificaciones])
        UC8([Administrar horarios])
        UC9([Gestionar citas])
        UC10([Gestionar usuarios])
    end
    P --- UC1
    P --- UC2
    P --- UC3
    P --- UC4
    P --- UC5
    P --- UC6
    P --- UC7
    A --- UC2
    A --- UC8
    A --- UC9
    A --- UC10
    UC4 -. incluye .-> UC3
```

## 2. Diagrama de clases

Describe las clases principales del sistema, sus datos, operaciones y relaciones.

```mermaid
classDiagram
direction LR
class Usuario {
  +UUID identificador
  +String nombre
  +String correo
  +String claveCifrada
  +String tipoDeUsuario
  +crearCuenta()
  +iniciarSesion()
}
class Paciente {
  +String telefono
  +consultarCitas()
  +solicitarCita()
  +cancelarCita()
}
class Administrador {
  +crearHorario()
  +actualizarHorario()
  +gestionarCitas()
}
class Cita {
  +UUID identificador
  +Date fecha
  +String hora
  +String estado
  +DateTime fechaDeCreacion
  +confirmar()
  +cancelar()
}
class Horario {
  +UUID identificador
  +Date fecha
  +String horaDeInicio
  +String horaDeFin
  +Boolean disponible
  +verificarDisponibilidad()
}
class Notificacion {
  +UUID identificador
  +String mensaje
  +DateTime fechaDeEnvio
  +String estado
  +enviar()
}
Usuario <|-- Paciente
Usuario <|-- Administrador
Paciente "1" --> "0..*" Cita : solicita
Cita "0..*" --> "1" Horario : reserva
Paciente "1" --> "0..*" Notificacion : recibe
Administrador "1" --> "0..*" Horario : administra
```

## 3. Diagrama de secuencia: agendar una cita

Muestra cómo se comunican el paciente, la interfaz, el servicio de citas, la base de datos y el servicio de notificaciones durante una reserva.

```mermaid
sequenceDiagram
    autonumber
    actor Paciente
    participant UI as Interfaz de usuario
    participant API as Servicio de citas
    participant DB as Base de datos
    participant NOTI as Servicio de notificaciones

    Paciente->>UI: Selecciona fecha y horario
    UI->>API: Solicita horarios disponibles
    API->>DB: Consulta horarios libres
    DB-->>API: Devuelve lista de horarios
    API-->>UI: Envía disponibilidad
    Paciente->>UI: Confirma el horario elegido
    UI->>API: Solicita crear la cita
    API->>DB: Verifica disponibilidad actual
    DB-->>API: Confirma que el horario está libre
    API->>DB: Guarda la cita y reserva el horario
    DB-->>API: Confirma el registro
    API->>NOTI: Solicita enviar confirmación
    NOTI-->>API: Devuelve resultado del envío
    API-->>UI: Informa que la cita fue creada
    UI-->>Paciente: Muestra la confirmación
    Note over API,DB: Si el horario ya no está disponible, el servidor rechaza la reserva.
```

## 4. Diagrama de actividad: agendar una cita

Presenta el flujo de acciones y decisiones que se siguen para registrar una cita.

```mermaid
flowchart TD
    A([Inicio]) --> B[El paciente inicia sesión]
    B --> C[Abre la consulta de horarios]
    C --> D[Selecciona una fecha]
    D --> E[El sistema consulta la disponibilidad]
    E --> F{¿Hay horarios disponibles?}
    F -- No --> G[Mostrar aviso y permitir elegir otra fecha]
    G --> D
    F -- Sí --> H[El paciente elige un horario]
    H --> I[Confirma la solicitud de cita]
    I --> J[El servidor valida la sesión y la disponibilidad]
    J --> K{¿El horario sigue libre?}
    K -- No --> L[Informar que el horario ya fue reservado]
    L --> C
    K -- Sí --> M[Guardar la cita y actualizar el horario]
    M --> N{¿Se guardó correctamente?}
    N -- No --> O[Mostrar un mensaje de error]
    O --> C
    N -- Sí --> P[Preparar la confirmación y la notificación]
    P --> Q[Mostrar la cita confirmada]
    Q --> R([Fin])
```

## 5. Diagrama de arquitectura inicial

Muestra la separación propuesta entre la interfaz, el servidor, los módulos principales y el almacenamiento de información.

```mermaid
flowchart TB
    U[Paciente / Administrador] --> UI[Interfaz de usuario<br/>Frontend]
    UI -->|Comunicación mediante API| API[Servidor de aplicación<br/>Backend]
    API --> AUTH[Autenticación y control de acceso]
    API --> CITAS[Gestión de citas]
    API --> HOR[Gestión de horarios]
    CITAS --> DB[(Base de datos)]
    HOR --> DB
    AUTH --> DB
    CITAS --> NOTI[Servicio de notificaciones]
    NOTI --> EXT[Correo electrónico u otro canal de aviso]
```

## Aclaraciones

- Los nombres, acciones y descripciones de los diagramas están en español; se conservan algunas siglas técnicas conocidas, como API, y términos entre paréntesis para reconocer frontend y backend.
- Los archivos fuente se pueden editar desde GitHub.
- Los modelos representan una propuesta de diseño; no demuestran que exista una aplicación implementada.
- Las reconstrucciones deben compararse con los archivos originales de Visual Paradigm para confirmar detalles y relaciones.
