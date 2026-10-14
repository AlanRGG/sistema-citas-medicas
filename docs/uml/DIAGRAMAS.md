# Diagramas del Sistema Digital de Citas Médicas

Estas visualizaciones se reconstruyeron a partir de la información del proyecto que se pudo recuperar. Son una base de trabajo editable y deben compararse con los modelos originales de Visual Paradigm antes de considerarlas equivalentes. El diagrama de casos de uso UML en formato PlantUML está en [01-casos-de-uso.puml](01-casos-de-uso.puml).

## 1. Casos de uso — vista general

```mermaid
flowchart LR
    P[Paciente]
    A[Administrador]
    subgraph S["Sistema Digital de Citas Médicas"]
        UC1([Registrarse])
        UC2([Iniciar sesión])
        UC3([Consultar horarios])
        UC4([Agendar cita])
        UC5([Consultar citas])
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
    UC4 -. requiere .-> UC3
```

## 2. Diagrama de clases

```mermaid
classDiagram
direction LR
class Usuario {
  +UUID id
  +String nombre
  +String correo
  +String contrasenaHash
  +String rol
  +registrarse()
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
  +UUID id
  +Date fecha
  +String hora
  +String estado
  +DateTime fechaCreacion
  +confirmar()
  +cancelar()
}
class Horario {
  +UUID id
  +Date fecha
  +String horaInicio
  +String horaFin
  +Boolean disponible
  +verificarDisponibilidad()
}
class Notificacion {
  +UUID id
  +String mensaje
  +DateTime fechaEnvio
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

```mermaid
sequenceDiagram
    autonumber
    actor Paciente
    participant UI as Interfaz (Frontend)
    participant API as Servicio de citas (Backend)
    participant DB as Base de datos
    participant NOTI as Servicio de notificaciones
    Paciente->>UI: Selecciona fecha y horario
    UI->>API: Solicitar horarios disponibles
    API->>DB: Consultar horarios libres
    DB-->>API: Lista de horarios
    API-->>UI: Mostrar disponibilidad
    Paciente->>UI: Confirma horario
    UI->>API: Crear solicitud de cita
    API->>DB: Verificar disponibilidad actual
    DB-->>API: Horario disponible
    API->>DB: Guardar cita y reservar horario
    DB-->>API: Confirmación de guardado
    API->>NOTI: Solicitar notificación
    NOTI-->>API: Resultado del envío
    API-->>UI: Cita creada
    UI-->>Paciente: Mostrar confirmación
    Note over API,DB: Si el horario ya no está disponible, el backend rechaza la reserva.
```

## 4. Diagrama de actividad: agendar una cita

```mermaid
flowchart TD
    A([Inicio]) --> B[Paciente inicia sesión]
    B --> C[Abre consulta de horarios]
    C --> D[Selecciona fecha]
    D --> E[El sistema consulta disponibilidad]
    E --> F{¿Hay horarios disponibles?}
    F -- No --> G[Mostrar aviso y permitir otra fecha]
    G --> D
    F -- Sí --> H[Paciente elige un horario]
    H --> I[Paciente confirma solicitud]
    I --> J[Backend valida sesión y disponibilidad]
    J --> K{¿Horario sigue libre?}
    K -- No --> L[Informar que el horario ya fue reservado]
    L --> C
    K -- Sí --> M[Guardar cita y actualizar horario]
    M --> N{¿Se guardó correctamente?}
    N -- No --> O[Mostrar error controlado]
    O --> C
    N -- Sí --> P[Generar confirmación y notificación]
    P --> Q[Mostrar cita confirmada]
    Q --> R([Fin])
```

## 5. Diagrama de arquitectura inicial

```mermaid
flowchart TB
    U[Paciente / Administrador] --> UI[Frontend<br/>Interfaz de usuario]
    UI -->|HTTPS + JSON mediante API| API[Backend<br/>Lógica de negocio y API]
    API --> AUTH[Autenticación y autorización]
    API --> CITAS[Gestión de citas]
    API --> HOR[Gestión de horarios]
    CITAS --> DB[(Base de datos)]
    HOR --> DB
    AUTH --> DB
    CITAS --> NOTI[Servicio de notificaciones]
    NOTI --> EXT[Correo o canal de notificación]
```

## Alcance de estos modelos

Los diagramas representan el diseño propuesto, no una aplicación implementada. Las tecnologías específicas, reglas clínicas, permisos detallados, políticas de privacidad y mecanismo final de notificaciones todavía requieren definición. La verificación de disponibilidad debe realizarse en el backend para evitar reservas duplicadas.
