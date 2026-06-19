# Arquitectura y modelo operativo de UniAvisos

> Una pantalla muestra lo que hace una aplicación.
> La arquitectura explica por qué puede seguir haciéndolo cuando el sistema crece.

Este documento presenta la arquitectura conceptual, el modelo operativo, los actores, las decisiones de escalabilidad y la estrategia de seguridad de **UniAvisos**.

Por tratarse de un proyecto oficial, la descripción se mantiene en un nivel técnico general. No se incluyen código fuente, identificadores, nombres internos de colecciones, reglas exactas, credenciales, rutas privadas ni infraestructura restringida.

```text
[ SYSTEM PROFILE ]

Platform: Android
Language: Kotlin
UI: Jetpack Compose
Remote data: Cloud services
Notifications: Topic-based messaging
Local preferences: Device persistence
Current stage: Beta 4.3
Source code: Restricted
```

---

# 1. Contexto arquitectónico

UniAvisos comenzó como un prototipo móvil con información definida localmente.

Esa primera arquitectura permitió validar:

* Pantallas
* Navegación
* Organización por áreas
* Flujo de consulta
* Identidad visual
* Experiencia inicial del usuario

La estructura conceptual era sencilla:

```text
Aplicación Android
       │
       ▼
Datos locales
       │
       ▼
Contenido mostrado
```

Esta solución era adecuada para una prueba de concepto, pero no para un sistema oficial que debía recibir cambios sin reinstalarse.

## Limitaciones del modelo local

* La información permanecía vinculada a la aplicación instalada
* Cada modificación requería cambiar y recompilar el proyecto
* No existía una fuente central de contenido
* Los dispositivos no compartían el mismo estado
* No podían publicarse avisos de manera operativa
* Las notificaciones no estaban conectadas con contenido real
* La administración dependía del proceso de desarrollo

La aplicación podía demostrar la idea.

Todavía no podía operar como servicio.

---

# 2. Transición hacia una arquitectura conectada

> La aplicación dejó de contener el sistema.
> Comenzó a conectarse con él.

La transición principal consistió en separar la aplicación móvil de la información que cambia constantemente.

La nueva arquitectura estableció que:

* El contenido institucional debía mantenerse en una fuente remota
* La aplicación debía consultar e interpretar ese contenido
* Las preferencias individuales debían permanecer en el dispositivo cuando no afectaran a otros usuarios
* Las notificaciones debían distribuirse según categorías de interés
* Las operaciones administrativas debían diferenciarse de las funciones del usuario final

La estructura evolucionó conceptualmente hacia:

```text
Usuario
   │
   ▼
Aplicación Android
   │
   ├── Interfaz
   ├── Navegación
   ├── Estado de la aplicación
   ├── Preferencias locales
   └── Suscripciones
   │
   ▼
Capa de acceso a datos
   │
   ├── Servicio remoto de contenido
   └── Servicio de notificaciones
```

## Cambio de responsabilidad

### Antes

```text
La aplicación contiene la información.
```

### Después

```text
La aplicación solicita, procesa y presenta la información.
```

Este cambio convirtió a UniAvisos en un cliente conectado a una fuente central.

También introdujo nuevas responsabilidades:

* Conectividad
* Estados de carga
* Manejo de errores
* Actualizaciones en tiempo real
* Sincronización
* Integridad de datos
* Seguridad
* Control de operaciones remotas
* Uso eficiente de recursos

```text
[ ARCHITECTURE TRANSITION ]

Local prototype: Completed
Remote content: Integrated
Shared information: Enabled
Realtime behavior: Active
Notifications: Connected
```

---

# 3. Arquitectura conceptual actual

La arquitectura actual combina información remota con preferencias locales.

```text
                    ┌─────────────────────────┐
                    │ Administración interna │
                    │ autorizada para pruebas│
                    └────────────┬────────────┘
                                 │
                                 ▼
┌─────────────────┐    ┌─────────────────────────┐
│ Aplicación      │◄──►│ Servicio remoto de datos│
│ Android         │    └────────────┬────────────┘
└────────┬────────┘                 │
         │                          ▼
         │                 ┌──────────────────────┐
         │                 │ Servicio de          │
         │                 │ notificaciones       │
         │                 └──────────────────────┘
         ▼
┌─────────────────┐
│ Preferencias    │
│ locales         │
└─────────────────┘
```

## Principio de autoridad de los datos

El sistema diferencia entre información global y decisiones individuales.

### Información global

Es administrada de manera remota y afecta a todos los usuarios:

* Áreas disponibles
* Estado de las áreas
* Orden de presentación
* Avisos
* Estado activo o inactivo
* Indicadores de actualización
* Contadores generales

### Información local

Pertenece únicamente a la experiencia de una persona en su dispositivo:

* Preferencias de suscripción
* Avisos ocultos
* Selecciones locales
* Estados específicos de la interfaz

La regla conceptual es:

```text
Contenido institucional → Fuente remota
Preferencias personales → Dispositivo
```

Esto evita que una acción privada, como ocultar un aviso, modifique la información disponible para otros usuarios.

---

# 4. Componentes arquitectónicos

## 4.1 Capa de presentación

Construida con Kotlin y Jetpack Compose.

Sus responsabilidades incluyen:

* Mostrar áreas y avisos
* Representar estados de carga
* Presentar errores
* Gestionar interacción
* Facilitar navegación
* Mostrar contadores
* Proporcionar retroalimentación visual
* Adaptarse al contenido disponible

La interfaz no debe decidir directamente cómo se almacenan o distribuyen los datos.

Su función principal es representar el estado de la aplicación y recibir acciones del usuario.

---

## 4.2 Navegación

La navegación coordina el recorrido entre:

* Pantalla inicial
* Áreas
* Avisos
* Detalles
* Preferencias
* Herramientas internas durante pruebas

También debe responder a eventos externos, como la apertura de una notificación.

## Navegación desde notificaciones

Una notificación puede recibirse antes de que toda la información remota termine de cargarse.

Por ello, el sistema debe coordinar:

```text
Notificación recibida
        │
        ▼
Identificación del destino
        │
        ▼
Verificación del estado de los datos
        │
        ├── Datos disponibles → Navegar
        │
        └── Datos pendientes → Esperar carga
```

La navegación no depende únicamente del evento recibido.

También depende de que el estado interno sea válido.

---

## 4.3 Estado y lógica de aplicación

Esta capa conceptual es responsable de:

* Coordinar datos locales y remotos
* Procesar preferencias
* Determinar qué información solicitar
* Mantener estados de carga
* Evitar operaciones duplicadas
* Coordinar eventos externos
* Gestionar contenido visible
* Controlar el ciclo de vida de listeners

En la versión actual, algunas responsabilidades todavía se encuentran cercanas a las pantallas.

La arquitectura objetivo contempla aumentar progresivamente la separación entre:

```text
Interfaz
   │
   ▼
Estado de pantalla
   │
   ▼
Lógica de aplicación
   │
   ▼
Fuente de datos
```

---

## 4.4 Capa de datos remotos

La fuente remota mantiene el contenido que debe compartirse entre dispositivos.

Sus responsabilidades generales son:

* Proporcionar áreas activas
* Proporcionar avisos
* Reflejar cambios
* Mantener estados administrativos
* Proporcionar indicadores agregados
* Facilitar actualizaciones coordinadas

La documentación pública no incluye nombres internos, rutas, estructuras exactas ni reglas de acceso.

---

## 4.5 Persistencia local

La aplicación utiliza persistencia ligera para conservar preferencias específicas del dispositivo.

Entre sus usos se encuentran:

* Áreas seleccionadas
* Avisos ocultos
* Preferencias individuales
* Estados que no deben alterar la información global

## Evolución prevista

La estrategia futura contempla incorporar almacenamiento local estructurado para:

* Mantener contenido disponible sin conexión
* Reducir consultas repetidas
* Comparar versiones
* Sincronizar únicamente cambios
* Mejorar tiempos de carga
* Recuperarse ante interrupciones de red

La arquitectura objetivo se representa así:

```text
Interfaz
   │
   ▼
Estado / ViewModel
   │
   ▼
Repositorio
   │
   ├── Base de datos local
   └── Servicio remoto
```

Esta estructura representa una dirección arquitectónica planificada. No implica que todos sus componentes ya estén implementados en la versión actual.

---

## 4.6 Servicio de notificaciones

Las notificaciones permiten distribuir información según categorías de interés.

El modelo conceptual utiliza:

* Categorías asociadas con áreas
* Suscripción voluntaria
* Desuscripción
* Recepción de eventos
* Navegación hacia contenido relacionado

```text
Área
  │
  ▼
Categoría de notificación
  │
  ▼
Dispositivos suscritos
  │
  ▼
Aviso relevante
```

Las operaciones privilegiadas de envío no deben depender de credenciales almacenadas dentro de la aplicación móvil.

La solución definitiva requiere un entorno controlado, como un backend o funciones seguras en la nube.

---

# 5. Modelo operativo institucional

UniAvisos no utiliza un modelo comercial basado en ventas, publicidad o suscripciones de pago.

Su modelo es de **servicio institucional**.

## Propósito

* Centralizar avisos
* Reducir dispersión de información
* Segmentar comunicaciones
* Facilitar el acceso móvil
* Mejorar la oportunidad de entrega
* Conectar a los usuarios con canales oficiales

## Actores principales

### Áreas responsables

Generan información y mantienen sus avisos actualizados.

### Administradores autorizados

Validan, publican, modifican y desactivan contenido.

### Usuarios finales

Consultan avisos, seleccionan preferencias y reciben notificaciones.

### Institución

Define políticas, responsables, permisos, alcance y lineamientos de seguridad.

---

# 6. Flujo operativo

El flujo general del contenido puede representarse así:

```text
Área responsable
       │
       ▼
Creación del aviso
       │
       ▼
Validación administrativa
       │
       ▼
Publicación
       │
       ├── Consulta en la aplicación
       └── Distribución mediante notificación
                    │
                    ▼
              Usuario final
```

El ciclo continúa cuando el contenido:

* Se modifica
* Se desactiva
* Expira
* Se sustituye
* Requiere corrección

## Responsabilidades operativas

### Creación

El área genera la información.

### Validación

Una persona autorizada verifica contenido, prioridad y vigencia.

### Publicación

El aviso queda disponible para consulta.

### Distribución

Los usuarios interesados pueden recibir una notificación.

### Mantenimiento

El contenido se actualiza o desactiva según su vigencia.

---

# 7. Panel administrador provisional

> Una aplicación puede mostrar contenido correctamente.
> La prueba completa comienza cuando también puede recibirlo.

Durante Beta 4.2 se desarrollaron herramientas internas para validar el flujo administrativo.

El panel provisional permitió:

* Crear avisos
* Seleccionar el área
* Definir información complementaria
* Publicar como activo o inactivo
* Administrar avisos existentes
* Crear y editar áreas
* Modificar orden
* Activar o desactivar elementos
* Comprobar cambios en la aplicación de usuario

## Arquitectura funcional de pruebas

```text
Panel provisional
       │
       ▼
Lógica administrativa
       │
       ▼
Fuente remota
       │
       ▼
Aplicación de usuario
```

## Separación de perfiles

### Usuario final

* Consulta avisos
* Selecciona suscripciones
* Recibe notificaciones
* Oculta contenido localmente
* Accede a canales oficiales

### Administrador

* Crea contenido
* Cambia estados
* Administra áreas
* Mantiene información global

Esta diferencia confirmó que la solución de producción necesita:

* Autenticación
* Roles
* Permisos
* Reglas de seguridad
* Auditoría
* Separación de funciones
* Retiro o aislamiento del panel provisional

```text
[ ADMIN MODULE ]

Purpose: Internal validation
Production status: Restricted
Authentication: Planned
Role separation: Required
```

---

# 8. Modelo de escalabilidad

La escalabilidad del sistema se analiza en tres dimensiones.

## 8.1 Escalabilidad de datos

El sistema debe prepararse para:

* Más áreas
* Más avisos
* Mayor historial
* Más cambios
* Más contenido activo

## 8.2 Escalabilidad de usuarios

Debe considerar:

* Más dispositivos
* Diferentes suscripciones
* Mayor número de notificaciones
* Preferencias independientes
* Distintos estados locales

## 8.3 Escalabilidad administrativa

Debe contemplar:

* Más responsables
* Diferentes roles
* Permisos específicos
* Control de cambios
* Auditoría
* Separación de áreas

---

# 9. Optimización de operaciones remotas

Durante Beta 4.3 se detectó que algunos componentes podían mantener listeners para áreas que el usuario no había seleccionado.

El sistema obtenía información correctamente.

También obtenía información que no necesitaba.

## Estrategia aplicada

* Escuchar solamente áreas seleccionadas
* Evitar listeners cuando no existen suscripciones
* Utilizar claves estables
* Reducir reinicios innecesarios
* Mantener contadores agregados
* Registrar versiones de cambio
* Coordinar escrituras relacionadas

## Relación entre técnica y operación

Las operaciones remotas pueden afectar:

* Rendimiento
* Consumo de red
* Uso de batería
* Latencia
* Costos de infraestructura
* Capacidad de crecimiento

Por ello, optimizar listeners no fue únicamente una mejora de código.

También fue una decisión operativa.

```text
[ SCALABILITY RULE ]

Do not listen to everything.
Listen to what the user actually needs.
```

---

# 10. Actualizaciones coordinadas

Cuando se registra un aviso activo, deben actualizarse tanto el contenido como sus indicadores asociados.

La operación conceptual es:

```text
Crear aviso
    +
Actualizar contador
    +
Registrar cambio
    =
Operación coordinada
```

El objetivo es evitar estados parciales:

```text
Aviso guardado
Contador sin actualizar
```

o:

```text
Contador actualizado
Aviso no registrado
```

Mantener consistencia entre operaciones relacionadas es esencial para futuras estrategias de sincronización.

---

# 11. Modelo de seguridad

La seguridad final debe aplicarse en varias capas.

## Identidad

* Inicio de sesión
* Gestión de sesiones
* Recuperación de acceso
* Identificación de responsables

## Autorización

* Roles
* Permisos
* Separación entre usuario y administrador
* Restricción de operaciones privilegiadas

## Datos

* Validación
* Reglas de lectura
* Reglas de escritura
* Integridad
* Protección de información

## Operaciones privilegiadas

* Backend controlado
* Sin secretos dentro de la aplicación
* Registro de acciones
* Auditoría

## Distribución

* Firma de la aplicación
* Retiro del panel provisional
* Protección de configuraciones
* Revisión previa a publicación

## Principio central

```text
La aplicación móvil no debe contener secretos
capaces de autorizar operaciones administrativas.
```

Una aplicación instalada en dispositivos externos debe considerarse un entorno no confiable para almacenar credenciales privilegiadas.

---

# 12. Estrategia de pruebas

Las pruebas actuales se concentran en validaciones funcionales, de integración y de comportamiento.

## Pruebas funcionales

* Navegación
* Consulta de áreas
* Consulta de avisos
* Detalle
* Preferencias
* Ocultamiento local
* Restauración
* Administración interna

## Pruebas de integración

* Aplicación con fuente remota
* Actualizaciones en tiempo real
* Suscripciones
* Notificaciones
* Contadores
* Operaciones coordinadas

## Pruebas de comportamiento

* Usuario sin suscripciones
* Usuario con una suscripción
* Usuario con varias suscripciones
* Aviso activo
* Aviso inactivo
* Cambios durante la ejecución
* Navegación desde una notificación
* Contenido oculto localmente

## Herramientas

* Android Studio
* Dispositivo Android físico
* Logcat
* Consola de servicios
* Comparación de estados
* Pruebas manuales repetibles

## Evidencias técnicas

Las validaciones permitieron comprobar, entre otros casos, que:

* Un aviso activo actualiza sus indicadores
* Un aviso inactivo no incrementa contadores visibles
* Un usuario sin suscripciones evita listeners innecesarios
* Las operaciones aumentan según las preferencias seleccionadas
* Los cambios remotos se reflejan en la aplicación

## Pruebas futuras

* Pruebas unitarias
* Pruebas de interfaz
* Pruebas de repositorios
* Pruebas de sincronización
* Pruebas de seguridad
* Pruebas piloto con usuarios
* Pruebas de recuperación ante errores

---

# 13. Modelo de evolución técnica

La evolución planificada mantiene este orden:

```text
Beta 4.3
Escalabilidad base
      │
      ▼
Beta 4.4
Experiencia visual
      │
      ▼
Beta 4.5
Persistencia y sincronización
      │
      ▼
Versión 5.0
Seguridad y preparación para producción
```

La decisión de atender primero la escalabilidad evita construir una nueva interfaz sobre una base que todavía realiza operaciones innecesarias.

---

# 14. Arquitectura objetivo

La arquitectura prevista para etapas posteriores puede representarse así:

```text
┌─────────────────────────────┐
│ Interfaz Jetpack Compose    │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│ Estado de pantalla          │
│ y ViewModel                 │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│ Repositorio de datos        │
└──────────┬───────────┬──────┘
           │           │
           ▼           ▼
┌────────────────┐  ┌────────────────┐
│ Persistencia   │  │ Servicio       │
│ local          │  │ remoto         │
└────────────────┘  └────────────────┘
```

## Objetivos

* Separar responsabilidades
* Facilitar pruebas
* Reducir dependencia directa entre pantalla y servicio
* Mejorar manejo de estado
* Permitir trabajo sin conexión
* Centralizar sincronización
* Preparar la aplicación para crecer

Esta es una arquitectura objetivo y no una afirmación de que toda la estructura ya se encuentre implementada.

---

# 15. Conclusión

UniAvisos evolucionó desde una arquitectura local adecuada para validar una idea hasta un sistema conectado con:

* Contenido dinámico
* Actualización en tiempo real
* Preferencias locales
* Suscripciones
* Notificaciones
* Herramientas administrativas de prueba
* Contadores agregados
* Optimización de listeners
* Planeación de persistencia
* Estrategia de seguridad

La aplicación visible representa solo una parte del sistema.

La otra parte está formada por decisiones sobre:

* Quién controla la información
* Qué datos son globales
* Qué preferencias son locales
* Cuándo consultar
* Cuánto tiempo escuchar
* Cómo mantener consistencia
* Cómo proteger operaciones privilegiadas
* Cómo preparar el crecimiento

```text
[ SYSTEM MODEL ]

Architecture: Connected and reactive
Remote data authority: Active
Local personalization: Active
Administration: Restricted
Scalability: In progress
Production security: Planned
```

El usuario ve avisos.

La arquitectura sostiene todo lo que tuvo que ocurrir para que esos avisos llegaran correctamente.

**edHash**
