# Evolución de UniAvisos

> Una aplicación no evoluciona cuando cambia el número de versión.
> Evoluciona cuando deja de resolver el problema de la misma manera.

Este documento presenta la evolución funcional y técnica de **UniAvisos**, desde su primera versión Alpha hasta la Beta 4.3, versión actual de trabajo.

Por tratarse de un proyecto oficial, esta documentación se mantiene en un nivel descriptivo. No se incluyen código fuente, configuraciones internas, credenciales, identificadores de servicios, datos institucionales restringidos ni capturas sin autorización.

```text
[ DEVELOPMENT LOG ]

Project: UniAvisos
Platform: Android
Current stage: Beta 4.3
Source code: Restricted
Documentation level: Public case study
```

---

## El problema inicial

La información universitaria puede encontrarse distribuida entre diferentes áreas, publicaciones y canales oficiales.

El usuario sabe que la información existe.

El problema es encontrarla a tiempo.

UniAvisos surgió con el objetivo de centralizar avisos universitarios dentro de una aplicación Android que permitiera:

* Consultar información desde un dispositivo móvil
* Organizar avisos por áreas
* Facilitar el acceso a los detalles
* Reducir búsquedas manuales entre diferentes plataformas
* Permitir preferencias de usuario
* Preparar el sistema para incorporar notificaciones
* Mantener una experiencia sencilla y reconocible

En las primeras etapas, el objetivo no era construir todas las funciones posibles.

Era comprobar que el recorrido principal tuviera sentido.

---

# Alpha inicial — La primera señal

> Antes de optimizar un sistema, primero debe existir.

## Objetivo

Construir un primer prototipo funcional que permitiera validar la idea principal de UniAvisos desde un dispositivo Android.

## Funcionalidades desarrolladas

La primera versión incorporó:

* Pantalla de inicio
* Pantalla principal de bienvenida
* Acceso a la sección de áreas
* Selección de un área
* Consulta de avisos relacionados
* Vista de detalle
* Navegación entre las pantallas principales

## Primer flujo funcional

```text
Inicio
   │
   ▼
Áreas
   │
   ▼
Avisos
   │
   ▼
Detalle
```

## Resultado

Se obtuvo el primer recorrido completo de consulta.

La aplicación todavía era limitada, pero ya demostraba que la idea podía convertirse en un producto funcional.

## Aprendizaje

Antes de conectar servicios remotos, notificaciones o herramientas administrativas, era necesario comprobar que el usuario pudiera comprender el flujo principal sin explicaciones adicionales.

```text
[ ALPHA STATUS ]

Navigation: Operational
Remote data: Not implemented
Notifications: Not implemented
Concept validation: Successful
```

La primera Alpha no resolvía todo.

Pero ya había encontrado el camino.

---

# Alpha 2.0 — El prototipo obtiene identidad

> Un sistema puede funcionar y aun así no pertenecer todavía al lugar para el que fue diseñado.

## Objetivo

Transformar el prototipo inicial en una experiencia alineada con el contexto universitario real.

## Mejoras incorporadas

Esta versión agregó:

* Áreas institucionales reales
* Organización inicial de departamentos
* Menú lateral de navegación
* Acceso a canales oficiales
* Enlaces relacionados con cada área
* Identidad visual institucional
* Mejor conexión entre inicio, áreas y avisos
* Mayor claridad en los elementos interactivos

## Cambio principal

La aplicación dejó de sentirse como una demostración genérica.

Comenzó a representar una herramienta diseñada para un entorno universitario específico.

## Resultado

Los usuarios podían identificar con mayor facilidad:

* Qué tipo de información encontrarían
* Qué área era responsable
* Cómo navegar hacia otros departamentos
* Dónde consultar los canales oficiales relacionados

## Aprendizaje

La identidad visual no solamente modifica la apariencia.

También comunica contexto, propósito y confianza.

```text
[ INTERFACE UPDATE ]

Generic prototype: Replaced
Institutional context: Integrated
Navigation consistency: Improved
```

El sistema ya no solo funcionaba.

Ahora comenzaba a reconocerse a sí mismo.

---

# Alpha 2.5 — Orden antes de crecimiento

> Cuando un proyecto empieza a crecer, el desorden también intenta crecer con él.

## Objetivo

Reorganizar internamente el proyecto antes de incorporar funciones más complejas.

Las primeras versiones demostraron que el concepto funcionaba, pero la estructura inicial comenzaba a dificultar el mantenimiento.

## Trabajo realizado

El proyecto se reorganizó conceptualmente en:

* Modelos de información
* Fuentes de datos
* Componentes reutilizables
* Pantallas
* Navegación
* Recursos visuales
* Funciones de apoyo

También se mejoró la consistencia de versiones y responsabilidades internas.

## Resultado

Las funcionalidades de Alpha 2.0 se conservaron, pero el proyecto quedó mejor preparado para recibir:

* Datos remotos
* Nuevas pantallas
* Preferencias
* Notificaciones
* Estados dinámicos
* Mayor complejidad lógica

## Aprendizaje

Una aplicación puede funcionar correctamente y aun así necesitar una reorganización.

La deuda técnica no siempre provoca un error inmediato.

A veces solo espera a que el proyecto sea demasiado grande para ignorarla.

```text
[ INTERNAL RESTRUCTURE ]

Visible changes: Minimal
Maintainability: Improved
Future complexity: Anticipated
```

---

# Beta 4.0 — El contenido deja de estar inmóvil

> La información fija envejece dentro de la aplicación.
> La información dinámica puede cambiar sin esperar una nueva instalación.

## Objetivo

Eliminar la dependencia de áreas definidas únicamente dentro de la aplicación.

En un entorno real, las áreas pueden:

* Cambiar de nombre
* Actualizar su información
* Modificar su orden
* Activarse o desactivarse
* Cambiar sus canales relacionados

Publicar una nueva versión por cada ajuste no era una solución escalable.

## Evolución técnica

La administración de áreas pasó a una estructura dinámica conectada con servicios en la nube.

Esto permitió gestionar de manera remota:

* Nombre
* Descripción
* Estado
* Orden
* Canal oficial
* Identidad visual
* Categoría de suscripción

## Funciones incorporadas

* Carga dinámica de áreas
* Actualización en tiempo real
* Orden configurable
* Activación y desactivación
* Cuadrícula generada desde datos remotos
* Menú lateral dinámico
* Preferencias por área
* Suscripción y desuscripción a categorías de notificación

## Resultado

La aplicación dejó de depender completamente de una estructura fija.

Los cambios administrativos podían reflejarse sin modificar directamente la aplicación instalada.

## Nuevo desafío

El contenido dinámico resolvió una limitación, pero introdujo otras responsabilidades:

* Estados de carga
* Errores de conexión
* Datos incompletos
* Identificadores estables
* Ordenamiento
* Cambios mientras la aplicación permanece abierta

## Aprendizaje

Mover datos a la nube no elimina la complejidad.

Solo cambia el lugar donde debe administrarse.

```text
[ BETA 4.0 ]

Static departments: Replaced
Dynamic configuration: Active
Subscriptions: Enabled
Realtime updates: Operational
```

El sistema ya podía cambiar sin ser reinstalado.

Y con eso comenzó una etapa distinta.

---

# Beta 4.1 — La aplicación empieza a recordar

> Mostrar información es una función.
> Recordar lo que cada usuario necesita es una experiencia.

## Objetivo

Convertir la estructura dinámica de áreas en un sistema completo de avisos, preferencias y notificaciones.

## Funciones incorporadas

* Avisos organizados por área
* Contenido actualizado en tiempo real
* Vista detallada de información
* Estados activos e inactivos
* Navegación desde notificaciones
* Preferencias locales
* Ocultamiento de avisos
* Restauración de contenido oculto
* Contadores ajustados al contenido visible
* Experiencia personalizada por dispositivo

## Ocultamiento local

Se separaron dos acciones que podían parecer similares:

### Eliminar

Retirar un aviso del sistema para todos los usuarios.

### Ocultar

Dejar de mostrar un aviso únicamente en el dispositivo de una persona.

Esta decisión permitió personalizar la experiencia sin modificar la información global.

## Navegación desde notificaciones

Una notificación puede llegar antes de que la aplicación termine de cargar la información necesaria.

La navegación no podía depender únicamente de recibir el evento.

Debía esperar hasta que el estado interno permitiera localizar correctamente el contenido solicitado.

## Resultado

UniAvisos dejó de mostrar exactamente el mismo estado a todos los usuarios.

La aplicación comenzó a reaccionar según:

* Preferencias
* Suscripciones
* Avisos ocultos
* Eventos externos
* Información disponible
* Momento del ciclo de vida

## Aprendizaje

La personalización requiere coordinar datos remotos y estados locales.

Cuando ambos mundos cambian al mismo tiempo, la aplicación debe decidir cuál información conservar, cuál actualizar y cuándo actuar.

```text
[ USER STATE ]

Remote notices: Active
Local preferences: Active
Hidden notices: Device-specific
Notification navigation: Coordinated
```

La aplicación ya no solo mostraba información.

Comenzaba a entender el contexto del usuario.

---

# Beta 4.2 — Panel administrador y validación de extremo a extremo

> Una aplicación puede mostrar avisos correctamente.
> La prueba real comienza cuando el contenido recorre todo el sistema.

## Objetivo

Construir una herramienta administrativa provisional que permitiera validar el flujo completo de creación, almacenamiento, actualización y consulta de contenido.

Hasta esta versión, gran parte de las pruebas se enfocaba en el comportamiento de la aplicación de usuario.

Beta 4.2 permitió probar también el origen de la información.

## Panel administrador provisional

Se desarrollaron herramientas internas para:

* Crear avisos
* Seleccionar el área correspondiente
* Definir prioridad e información complementaria
* Publicar contenido como activo o inactivo
* Administrar avisos existentes
* Activar y desactivar publicaciones
* Crear y editar áreas
* Modificar el orden de las áreas
* Activar o desactivar departamentos
* Validar los cambios directamente contra la fuente remota

El panel se mantuvo detrás de un control de laboratorio y no fue considerado una función disponible para usuarios finales.

## Flujo de negocio validado

La versión permitió probar el recorrido completo:

```text
Administrador autorizado
          │
          ▼
Creación o modificación del contenido
          │
          ▼
Validación de los datos
          │
          ▼
Persistencia en el servicio remoto
          │
          ▼
Actualización de la aplicación
          │
          ▼
Consulta por el usuario
```

## Arquitectura funcional de la etapa

```text
Panel provisional
       │
       ▼
Lógica administrativa
       │
       ▼
Fuente remota de datos
       │
       ├── Áreas
       └── Avisos
              │
              ▼
       Aplicación del usuario
```

## Separación de responsabilidades

Aunque el panel se ejecutaba dentro del entorno de desarrollo de la aplicación, conceptualmente se identificaron dos perfiles distintos:

### Usuario final

* Consulta información
* Selecciona suscripciones
* Recibe notificaciones
* Oculta contenido localmente
* Accede a canales oficiales

### Administrador

* Crea contenido
* Cambia estados
* Administra áreas
* Controla el orden
* Mantiene la información operativa

Esta separación permitió reconocer que la solución definitiva necesitaría:

* Autenticación
* Roles
* Permisos
* Reglas de seguridad
* Registro de acciones
* Separación del entorno administrativo
* Protección de operaciones privilegiadas

## Pruebas ejecutadas

Se realizaron pruebas manuales y funcionales sobre dispositivos Android reales.

Entre los escenarios revisados se encontraron:

* Creación de un aviso
* Visualización del aviso en la aplicación
* Activación y desactivación
* Cambios reflejados en tiempo real
* Creación de áreas
* Modificación del orden
* Activación e inactivación de departamentos
* Suscripción y desuscripción
* Recepción de notificaciones
* Navegación desde notificaciones
* Ocultamiento local
* Restauración de contenido
* Comportamiento de contadores
* Persistencia de preferencias

Las validaciones fueron acompañadas por:

* Registros de Logcat
* Observación de la información remota
* Comparación del estado antes y después de cada operación
* Pruebas en dispositivo físico
* Repetición de escenarios con contenido activo e inactivo

## Resultado

Beta 4.2 demostró que UniAvisos ya podía funcionar como un sistema completo:

```text
Crear → Almacenar → Distribuir → Mostrar → Actualizar
```

El panel hizo posible validar el proceso, pero también reveló que una herramienta administrativa no debía permanecer integrada sin controles de seguridad formales.

```text
[ BETA 4.2 ]

User application: Functional
Remote content: Operational
Administration flow: Validated
End-to-end tests: Completed
Production security: Pending
```

## Aprendizaje

El panel provisional no fue solamente una nueva pantalla.

Fue la pieza que permitió probar el modelo operativo completo.

También dejó clara una regla:

> Las operaciones administrativas pueden compartir datos con la aplicación de usuario, pero no deben compartir el mismo nivel de confianza.

Por esta razón, el panel deberá retirarse o aislarse antes de una distribución formal.

---

# Beta 4.3 — Escalar sin escuchar todo

> El tiempo real es útil.
> Escuchar información que nadie necesita, no.

## Objetivo

Preparar la aplicación para manejar más áreas, más avisos y más usuarios sin incrementar innecesariamente las operaciones remotas.

Hasta esta etapa, las funciones principales trabajaban correctamente.

Pero funcionar con pocos datos no significaba estar preparado para crecer.

## Diagnóstico

Se analizaron las operaciones activas de diferentes componentes.

Se detectó que algunas pantallas podían mantener listeners o consultas para áreas que el usuario no había seleccionado.

El sistema obtenía información correctamente.

También obtenía información que no necesitaba.

## Optimización por suscripciones

La lógica fue reorganizada para procesar contadores y actualizaciones únicamente de las áreas seleccionadas por el usuario.

Esto permitió:

* Evitar listeners cuando no existían suscripciones
* Aumentar operaciones únicamente según preferencias reales
* Reducir procesamiento de categorías irrelevantes
* Utilizar de forma más eficiente los recursos remotos
* Preparar la aplicación para incorporar más áreas

## Estabilidad de listeners

También se incorporaron referencias estables para evitar reinicios innecesarios cuando se actualizaba la información general.

Las operaciones en tiempo real solo debían reiniciarse cuando realmente cambiaban las suscripciones.

No cuando cambiaba cualquier dato relacionado.

## Contadores y control de cambios

La información general comenzó a incluir indicadores agregados como:

* Cantidad de avisos activos
* Versión del contenido
* Momento del último cambio

Estos datos preparan una futura estrategia de sincronización selectiva.

## Actualizaciones coordinadas

Cuando se registra contenido activo, la creación del aviso y la actualización de sus indicadores relacionados deben mantenerse coordinadas.

El objetivo es evitar estados incompletos como:

* Aviso creado
* Contador no actualizado

o:

* Contador incrementado
* Aviso no almacenado correctamente

## Validación

Las mejoras fueron comprobadas mediante:

* Registros de depuración
* Pruebas en dispositivo Android real
* Creación de avisos activos
* Creación de avisos inactivos
* Comparación de contadores
* Observación del número de listeners
* Verificación de actualizaciones relacionadas

Se confirmó que:

* Un aviso activo actualiza los indicadores correspondientes
* Un aviso inactivo no incrementa los contadores visibles
* Un usuario sin suscripciones evita listeners innecesarios
* Las operaciones aumentan únicamente conforme se agregan preferencias

## Estado actual

Beta 4.3 es la versión actual de desarrollo.

Entre sus mejoras se encuentran:

* Áreas activas cargadas dinámicamente
* Contadores derivados de información agregada
* Menú lateral conectado con información real
* Reducción de listeners según suscripciones
* Claves estables para controlar reinicios
* Actualizaciones coordinadas
* Menor dependencia de datos simulados
* Preparación para sincronización futura

Todavía existen optimizaciones que deben extenderse a otros componentes antes de cerrar por completo esta etapa.

## Aprendizaje

Una aplicación no se vuelve escalable por utilizar servicios en la nube.

Se vuelve escalable cuando sabe:

* Cuándo consultar
* Qué consultar
* Para quién consultar
* Cuánto tiempo escuchar
* Cómo detectar cambios
* Cómo evitar estados parciales

```text
[ BETA 4.3 STATUS ]

Dynamic data: Stable
Subscriptions: Selective
Unnecessary listeners: Reduced
Aggregated counters: Active
Synchronization foundation: In progress
Current version: Beta 4.3
```

El sistema no necesitaba escuchar más.

Necesitaba escuchar mejor.

---

# Próximas versiones

## Beta 4.4 — La interfaz también comunica

El siguiente bloque de trabajo estará enfocado en:

* Jerarquía visual
* Navegación
* Consistencia de componentes
* Estados de carga
* Accesibilidad
* Claridad de acciones
* Coherencia institucional

La decisión fue optimizar primero la base técnica.

Una interfaz nueva no corrige una arquitectura que todavía realiza operaciones innecesarias.

---

## Beta 4.5 — Recordar antes de volver a preguntar

Esta versión plantea:

* Almacenamiento local estructurado
* Información disponible sin conexión
* Sincronización de cambios relevantes
* Comparación de versiones
* Menor dependencia de conexión constante
* Reducción de consultas remotas
* Estados de sincronización

```text
Remote source
      │
      ▼
Local persistence
      │
      ▼
User interface
```

El almacenamiento local no reemplazará los servicios remotos.

Evitará preguntar nuevamente por información que ya se conoce.

---

## Versión 5.0 — De proyecto funcional a producto protegido

La versión 5.0 contempla:

* Autenticación
* Roles
* Permisos
* Reglas de seguridad
* Separación administrativa
* Registro de acciones
* Manejo estructurado de errores
* Retiro de herramientas provisionales
* Preparación para distribución formal
* Revisión de seguridad

```text
[ ROADMAP ]

Beta 4.4  → Visual experience
Beta 4.5  → Local persistence and synchronization
Version 5 → Security and production readiness
```

---

# Línea de evolución

```text
Alpha inicial
Validación del recorrido principal
        │
        ▼
Alpha 2.0
Identidad institucional y áreas reales
        │
        ▼
Alpha 2.5
Reorganización interna
        │
        ▼
Beta 4.0
Contenido dinámico y suscripciones
        │
        ▼
Beta 4.1
Avisos, notificaciones y personalización
        │
        ▼
Beta 4.2
Administración interna para pruebas
        │
        ▼
Beta 4.3
Escalabilidad y optimización
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

---

# Conclusión

UniAvisos comenzó como un prototipo para consultar avisos.

Con cada versión fue incorporando nuevas responsabilidades:

* Representar un contexto institucional
* Organizar su estructura interna
* Separar los datos del código
* Actualizar contenido dinámicamente
* Personalizar la experiencia
* Recibir notificaciones
* Administrar contenido
* Reducir operaciones innecesarias
* Preparar almacenamiento local
* Diseñar una ruta hacia producción

No toda evolución es visible en una pantalla.

Algunas de las mejoras más importantes ocurren en:

* El ciclo de vida
* La sincronización
* La consistencia
* El control de estados
* La seguridad
* La arquitectura

```text
[ END OF LOG ]

The interface shows the result.
The architecture carries the weight.
```

No todos los sistemas revelan su código.

Pero todos terminan revelando la calidad de las decisiones con las que fueron construidos.

**edHash**
# Evolución de UniAvisos

> Una aplicación no evoluciona cuando cambia el número de versión.
> Evoluciona cuando deja de resolver el problema de la misma manera.

Este documento presenta la evolución funcional y técnica de **UniAvisos**, desde su primera versión Alpha hasta la Beta 4.3, versión actual de trabajo.

Por tratarse de un proyecto oficial, esta documentación se mantiene en un nivel descriptivo. No se incluyen código fuente, configuraciones internas, credenciales, identificadores de servicios, datos institucionales restringidos ni capturas sin autorización.

```text
[ DEVELOPMENT LOG ]

Project: UniAvisos
Platform: Android
Current stage: Beta 4.3
Source code: Restricted
Documentation level: Public case study
```

---

## El problema inicial

La información universitaria puede encontrarse distribuida entre diferentes áreas, publicaciones y canales oficiales.

El usuario sabe que la información existe.

El problema es encontrarla a tiempo.

UniAvisos surgió con el objetivo de centralizar avisos universitarios dentro de una aplicación Android que permitiera:

* Consultar información desde un dispositivo móvil
* Organizar avisos por áreas
* Facilitar el acceso a los detalles
* Reducir búsquedas manuales entre diferentes plataformas
* Permitir preferencias de usuario
* Preparar el sistema para incorporar notificaciones
* Mantener una experiencia sencilla y reconocible

En las primeras etapas, el objetivo no era construir todas las funciones posibles.

Era comprobar que el recorrido principal tuviera sentido.

---

# Alpha inicial — La primera señal

> Antes de optimizar un sistema, primero debe existir.

## Objetivo

Construir un primer prototipo funcional que permitiera validar la idea principal de UniAvisos desde un dispositivo Android.

## Funcionalidades desarrolladas

La primera versión incorporó:

* Pantalla de inicio
* Pantalla principal de bienvenida
* Acceso a la sección de áreas
* Selección de un área
* Consulta de avisos relacionados
* Vista de detalle
* Navegación entre las pantallas principales

## Primer flujo funcional

```text
Inicio
   │
   ▼
Áreas
   │
   ▼
Avisos
   │
   ▼
Detalle
```

## Resultado

Se obtuvo el primer recorrido completo de consulta.

La aplicación todavía era limitada, pero ya demostraba que la idea podía convertirse en un producto funcional.

## Aprendizaje

Antes de conectar servicios remotos, notificaciones o herramientas administrativas, era necesario comprobar que el usuario pudiera comprender el flujo principal sin explicaciones adicionales.

```text
[ ALPHA STATUS ]

Navigation: Operational
Remote data: Not implemented
Notifications: Not implemented
Concept validation: Successful
```

La primera Alpha no resolvía todo.

Pero ya había encontrado el camino.

---

# Alpha 2.0 — El prototipo obtiene identidad

> Un sistema puede funcionar y aun así no pertenecer todavía al lugar para el que fue diseñado.

## Objetivo

Transformar el prototipo inicial en una experiencia alineada con el contexto universitario real.

## Mejoras incorporadas

Esta versión agregó:

* Áreas institucionales reales
* Organización inicial de departamentos
* Menú lateral de navegación
* Acceso a canales oficiales
* Enlaces relacionados con cada área
* Identidad visual institucional
* Mejor conexión entre inicio, áreas y avisos
* Mayor claridad en los elementos interactivos

## Cambio principal

La aplicación dejó de sentirse como una demostración genérica.

Comenzó a representar una herramienta diseñada para un entorno universitario específico.

## Resultado

Los usuarios podían identificar con mayor facilidad:

* Qué tipo de información encontrarían
* Qué área era responsable
* Cómo navegar hacia otros departamentos
* Dónde consultar los canales oficiales relacionados

## Aprendizaje

La identidad visual no solamente modifica la apariencia.

También comunica contexto, propósito y confianza.

```text
[ INTERFACE UPDATE ]

Generic prototype: Replaced
Institutional context: Integrated
Navigation consistency: Improved
```

El sistema ya no solo funcionaba.

Ahora comenzaba a reconocerse a sí mismo.

---

# Alpha 2.5 — Orden antes de crecimiento

> Cuando un proyecto empieza a crecer, el desorden también intenta crecer con él.

## Objetivo

Reorganizar internamente el proyecto antes de incorporar funciones más complejas.

Las primeras versiones demostraron que el concepto funcionaba, pero la estructura inicial comenzaba a dificultar el mantenimiento.

## Trabajo realizado

El proyecto se reorganizó conceptualmente en:

* Modelos de información
* Fuentes de datos
* Componentes reutilizables
* Pantallas
* Navegación
* Recursos visuales
* Funciones de apoyo

También se mejoró la consistencia de versiones y responsabilidades internas.

## Resultado

Las funcionalidades de Alpha 2.0 se conservaron, pero el proyecto quedó mejor preparado para recibir:

* Datos remotos
* Nuevas pantallas
* Preferencias
* Notificaciones
* Estados dinámicos
* Mayor complejidad lógica

## Aprendizaje

Una aplicación puede funcionar correctamente y aun así necesitar una reorganización.

La deuda técnica no siempre provoca un error inmediato.

A veces solo espera a que el proyecto sea demasiado grande para ignorarla.

```text
[ INTERNAL RESTRUCTURE ]

Visible changes: Minimal
Maintainability: Improved
Future complexity: Anticipated
```

# Hito de transición arquitectónica — De prototipo local a sistema conectado

> Hasta este punto, la aplicación podía demostrar la idea.
> A partir de aquí, comenzó a operar como un sistema real.

## Contexto

Las primeras versiones de UniAvisos funcionaban principalmente con información declarada de manera local dentro de la aplicación.

Esta estrategia fue adecuada para:

* Validar pantallas
* Probar la navegación
* Revisar la experiencia del usuario
* Confirmar la organización por áreas
* Trabajar sin depender inicialmente de infraestructura externa

Sin embargo, una aplicación oficial de avisos no podía depender permanentemente de datos almacenados dentro de cada instalación.

Cada cambio de información habría requerido modificar, compilar y distribuir nuevamente la aplicación.

## Problema arquitectónico

La primera arquitectura podía representarse de forma general así:

```text
Interfaz Android
       │
       ▼
Datos definidos localmente
       │
       ▼
Contenido mostrado al usuario
```

Esta estructura presentaba varias limitaciones:

* El contenido no podía actualizarse remotamente
* Las áreas estaban vinculadas a la versión instalada
* No existía una fuente central de información
* No había sincronización entre dispositivos
* Los avisos no podían publicarse de forma operativa
* Las notificaciones todavía no estaban conectadas con contenido real
* La aplicación funcionaba como demostración, no como servicio

## Decisión técnica

Se decidió migrar hacia una arquitectura conectada, donde la aplicación dejara de ser la propietaria directa de toda la información.

La nueva visión separó:

* La interfaz móvil
* La lógica de aplicación
* Las preferencias del dispositivo
* La fuente remota de contenido
* El servicio de notificaciones
* La futura administración del sistema

La arquitectura conceptual comenzó a evolucionar hacia:

```text
Usuario
   │
   ▼
Aplicación Android
   │
   ├── Interfaz
   ├── Navegación
   ├── Estado de la aplicación
   └── Preferencias locales
   │
   ▼
Capa de acceso a datos
   │
   ├── Servicio remoto de contenido
   └── Servicio de notificaciones
```

## Implementación de servicios reales

Durante esta transición se incorporaron servicios en la nube para que la aplicación pudiera:

* Obtener información desde una fuente central
* Reflejar cambios sin reinstalarse
* Compartir el mismo estado entre distintos dispositivos
* Preparar suscripciones por categorías
* Recibir notificaciones
* Separar los datos operativos de la interfaz
* Comenzar a funcionar con información administrable

La fuente remota pasó a considerarse la autoridad principal del contenido.

La aplicación móvil se convirtió en un cliente que consulta, representa y reacciona ante los cambios.

## Cambio en la responsabilidad de la aplicación

Antes:

```text
La aplicación contiene la información.
```

Después:

```text
La aplicación solicita, interpreta y presenta la información.
```

Este cambio fue significativo porque modificó la naturaleza del proyecto.

Ya no se trataba únicamente de construir pantallas.

También era necesario controlar:

* Conectividad
* Estados de carga
* Errores
* Datos incompletos
* Actualizaciones remotas
* Ciclo de vida
* Sincronización
* Seguridad
* Costos de operaciones en la nube

## Resultado

Después de esta etapa, UniAvisos dejó de ser únicamente un prototipo local.

Comenzó a operar como una aplicación conectada capaz de trabajar con contenido real y mantener una fuente central de información.

```text
[ ARCHITECTURE TRANSITION ]

Local prototype: Completed
Remote data source: Connected
Shared information: Enabled
Cloud notifications: Integrated
Operational flow: Active
```

## Aprendizaje

Migrar a la nube no significó únicamente cambiar el lugar donde se guardaban los datos.

Significó rediseñar:

* Quién controla la información
* Cómo se actualiza
* Cuándo se consulta
* Qué sucede cuando falla la conexión
* Cómo se protege
* Cómo se evita el consumo innecesario
* Cómo se prepara el crecimiento

La aplicación ya no cargaba una simulación del sistema.

Había comenzado a formar parte de él.


---

# Beta 4.0 — El contenido deja de estar inmóvil

> La información fija envejece dentro de la aplicación.
> La información dinámica puede cambiar sin esperar una nueva instalación.

## Objetivo

Eliminar la dependencia de áreas definidas únicamente dentro de la aplicación.

En un entorno real, las áreas pueden:

* Cambiar de nombre
* Actualizar su información
* Modificar su orden
* Activarse o desactivarse
* Cambiar sus canales relacionados

Publicar una nueva versión por cada ajuste no era una solución escalable.

## Evolución técnica

La administración de áreas pasó a una estructura dinámica conectada con servicios en la nube.

Esto permitió gestionar de manera remota:

* Nombre
* Descripción
* Estado
* Orden
* Canal oficial
* Identidad visual
* Categoría de suscripción

## Funciones incorporadas

* Carga dinámica de áreas
* Actualización en tiempo real
* Orden configurable
* Activación y desactivación
* Cuadrícula generada desde datos remotos
* Menú lateral dinámico
* Preferencias por área
* Suscripción y desuscripción a categorías de notificación

## Resultado

La aplicación dejó de depender completamente de una estructura fija.

Los cambios administrativos podían reflejarse sin modificar directamente la aplicación instalada.

## Nuevo desafío

El contenido dinámico resolvió una limitación, pero introdujo otras responsabilidades:

* Estados de carga
* Errores de conexión
* Datos incompletos
* Identificadores estables
* Ordenamiento
* Cambios mientras la aplicación permanece abierta

## Aprendizaje

Mover datos a la nube no elimina la complejidad.

Solo cambia el lugar donde debe administrarse.

```text
[ BETA 4.0 ]

Static departments: Replaced
Dynamic configuration: Active
Subscriptions: Enabled
Realtime updates: Operational
```

El sistema ya podía cambiar sin ser reinstalado.

Y con eso comenzó una etapa distinta.

---

# Beta 4.1 — La aplicación empieza a recordar

> Mostrar información es una función.
> Recordar lo que cada usuario necesita es una experiencia.

## Objetivo

Convertir la estructura dinámica de áreas en un sistema completo de avisos, preferencias y notificaciones.

## Funciones incorporadas

* Avisos organizados por área
* Contenido actualizado en tiempo real
* Vista detallada de información
* Estados activos e inactivos
* Navegación desde notificaciones
* Preferencias locales
* Ocultamiento de avisos
* Restauración de contenido oculto
* Contadores ajustados al contenido visible
* Experiencia personalizada por dispositivo

## Ocultamiento local

Se separaron dos acciones que podían parecer similares:

### Eliminar

Retirar un aviso del sistema para todos los usuarios.

### Ocultar

Dejar de mostrar un aviso únicamente en el dispositivo de una persona.

Esta decisión permitió personalizar la experiencia sin modificar la información global.

## Navegación desde notificaciones

Una notificación puede llegar antes de que la aplicación termine de cargar la información necesaria.

La navegación no podía depender únicamente de recibir el evento.

Debía esperar hasta que el estado interno permitiera localizar correctamente el contenido solicitado.

## Resultado

UniAvisos dejó de mostrar exactamente el mismo estado a todos los usuarios.

La aplicación comenzó a reaccionar según:

* Preferencias
* Suscripciones
* Avisos ocultos
* Eventos externos
* Información disponible
* Momento del ciclo de vida

## Aprendizaje

La personalización requiere coordinar datos remotos y estados locales.

Cuando ambos mundos cambian al mismo tiempo, la aplicación debe decidir cuál información conservar, cuál actualizar y cuándo actuar.

```text
[ USER STATE ]

Remote notices: Active
Local preferences: Active
Hidden notices: Device-specific
Notification navigation: Coordinated
```

La aplicación ya no solo mostraba información.

Comenzaba a entender el contexto del usuario.

---

# Beta 4.2 — El sistema aprende a administrarse

> Todo contenido que aparece frente al usuario tuvo que entrar al sistema de alguna manera.

## Objetivo

Validar el recorrido completo de creación, actualización y administración de contenido durante pruebas controladas.

## Herramientas desarrolladas

Se incorporaron funciones internas para:

* Crear avisos
* Seleccionar el área relacionada
* Activar y desactivar contenido
* Administrar avisos existentes
* Crear y editar áreas
* Modificar el estado de un área
* Cambiar su orden
* Validar cambios desde servicios remotos

## Flujo validado

```text
Creación del contenido
          │
          ▼
Almacenamiento remoto
          │
          ▼
Actualización de la aplicación
          │
          ▼
Consulta por el usuario
```

## Propósito

Estas herramientas permitieron probar el sistema completo sin depender de cambios manuales aislados durante cada validación.

## Límite identificado

El panel provisional todavía no representaba una solución administrativa de producción.

Faltaban elementos como:

* Autenticación formal
* Roles
* Permisos
* Registro de acciones
* Reglas de seguridad más estrictas
* Separación de responsabilidades administrativas

## Resultado

Fue posible comprobar que el contenido podía recorrer todo el sistema, desde su creación hasta su visualización.

## Aprendizaje

Una herramienta provisional puede acelerar las pruebas.

Pero cuando una función puede modificar información real, deja de ser únicamente una pantalla.

Se convierte en una responsabilidad de seguridad.

```text
[ ADMINISTRATION MODULE ]

Purpose: Internal validation
Authentication: Pending
Roles: Pending
Production status: Restricted
```

El sistema ya podía recibir información.

Ahora debía aprender a proteger quién podía enviarla.

---

# Beta 4.3 — Escalar sin escuchar todo

> El tiempo real es útil.
> Escuchar información que nadie necesita, no.

## Objetivo

Preparar la aplicación para manejar más áreas, más avisos y más usuarios sin incrementar innecesariamente las operaciones remotas.

Hasta esta etapa, las funciones principales trabajaban correctamente.

Pero funcionar con pocos datos no significaba estar preparado para crecer.

## Diagnóstico

Se analizaron las operaciones activas de diferentes componentes.

Se detectó que algunas pantallas podían mantener listeners o consultas para áreas que el usuario no había seleccionado.

El sistema obtenía información correctamente.

También obtenía información que no necesitaba.

## Optimización por suscripciones

La lógica fue reorganizada para procesar contadores y actualizaciones únicamente de las áreas seleccionadas por el usuario.

Esto permitió:

* Evitar listeners cuando no existían suscripciones
* Aumentar operaciones únicamente según preferencias reales
* Reducir procesamiento de categorías irrelevantes
* Utilizar de forma más eficiente los recursos remotos
* Preparar la aplicación para incorporar más áreas

## Estabilidad de listeners

También se incorporaron referencias estables para evitar reinicios innecesarios cuando se actualizaba la información general.

Las operaciones en tiempo real solo debían reiniciarse cuando realmente cambiaban las suscripciones.

No cuando cambiaba cualquier dato relacionado.

## Contadores y control de cambios

La información general comenzó a incluir indicadores agregados como:

* Cantidad de avisos activos
* Versión del contenido
* Momento del último cambio

Estos datos preparan una futura estrategia de sincronización selectiva.

## Actualizaciones coordinadas

Cuando se registra contenido activo, la creación del aviso y la actualización de sus indicadores relacionados deben mantenerse coordinadas.

El objetivo es evitar estados incompletos como:

* Aviso creado
* Contador no actualizado

o:

* Contador incrementado
* Aviso no almacenado correctamente

## Validación

Las mejoras fueron comprobadas mediante:

* Registros de depuración
* Pruebas en dispositivo Android real
* Creación de avisos activos
* Creación de avisos inactivos
* Comparación de contadores
* Observación del número de listeners
* Verificación de actualizaciones relacionadas

Se confirmó que:

* Un aviso activo actualiza los indicadores correspondientes
* Un aviso inactivo no incrementa los contadores visibles
* Un usuario sin suscripciones evita listeners innecesarios
* Las operaciones aumentan únicamente conforme se agregan preferencias

## Estado actual

Beta 4.3 es la versión actual de desarrollo.

Entre sus mejoras se encuentran:

* Áreas activas cargadas dinámicamente
* Contadores derivados de información agregada
* Menú lateral conectado con información real
* Reducción de listeners según suscripciones
* Claves estables para controlar reinicios
* Actualizaciones coordinadas
* Menor dependencia de datos simulados
* Preparación para sincronización futura

Todavía existen optimizaciones que deben extenderse a otros componentes antes de cerrar por completo esta etapa.

## Aprendizaje

Una aplicación no se vuelve escalable por utilizar servicios en la nube.

Se vuelve escalable cuando sabe:

* Cuándo consultar
* Qué consultar
* Para quién consultar
* Cuánto tiempo escuchar
* Cómo detectar cambios
* Cómo evitar estados parciales

```text
[ BETA 4.3 STATUS ]

Dynamic data: Stable
Subscriptions: Selective
Unnecessary listeners: Reduced
Aggregated counters: Active
Synchronization foundation: In progress
Current version: Beta 4.3
```

El sistema no necesitaba escuchar más.

Necesitaba escuchar mejor.

---

# Próximas versiones

## Beta 4.4 — La interfaz también comunica

El siguiente bloque de trabajo estará enfocado en:

* Jerarquía visual
* Navegación
* Consistencia de componentes
* Estados de carga
* Accesibilidad
* Claridad de acciones
* Coherencia institucional

La decisión fue optimizar primero la base técnica.

Una interfaz nueva no corrige una arquitectura que todavía realiza operaciones innecesarias.

---

## Beta 4.5 — Recordar antes de volver a preguntar

Esta versión plantea:

* Almacenamiento local estructurado
* Información disponible sin conexión
* Sincronización de cambios relevantes
* Comparación de versiones
* Menor dependencia de conexión constante
* Reducción de consultas remotas
* Estados de sincronización

```text
Remote source
      │
      ▼
Local persistence
      │
      ▼
User interface
```

El almacenamiento local no reemplazará los servicios remotos.

Evitará preguntar nuevamente por información que ya se conoce.

---

## Versión 5.0 — De proyecto funcional a producto protegido

La versión 5.0 contempla:

* Autenticación
* Roles
* Permisos
* Reglas de seguridad
* Separación administrativa
* Registro de acciones
* Manejo estructurado de errores
* Retiro de herramientas provisionales
* Preparación para distribución formal
* Revisión de seguridad

```text
[ ROADMAP ]

Beta 4.4  → Visual experience
Beta 4.5  → Local persistence and synchronization
Version 5 → Security and production readiness
```

---

# Línea de evolución

```text
Alpha inicial
Validación del recorrido principal
        │
        ▼
Alpha 2.0
Identidad institucional y áreas reales
        │
        ▼
Alpha 2.5
Reorganización interna
        │
        ▼
Beta 4.0
Contenido dinámico y suscripciones
        │
        ▼
Beta 4.1
Avisos, notificaciones y personalización
        │
        ▼
Beta 4.2
Administración interna para pruebas
        │
        ▼
Beta 4.3
Escalabilidad y optimización
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

---

# Conclusión

UniAvisos comenzó como un prototipo para consultar avisos.

Con cada versión fue incorporando nuevas responsabilidades:

* Representar un contexto institucional
* Organizar su estructura interna
* Separar los datos del código
* Actualizar contenido dinámicamente
* Personalizar la experiencia
* Recibir notificaciones
* Administrar contenido
* Reducir operaciones innecesarias
* Preparar almacenamiento local
* Diseñar una ruta hacia producción

No toda evolución es visible en una pantalla.

Algunas de las mejoras más importantes ocurren en:

* El ciclo de vida
* La sincronización
* La consistencia
* El control de estados
* La seguridad
* La arquitectura

```text
[ END OF LOG ]

The interface shows the result.
The architecture carries the weight.
```

No todos los sistemas revelan su código.

Pero todos terminan revelando la calidad de las decisiones con las que fueron construidos.

**edHash**
