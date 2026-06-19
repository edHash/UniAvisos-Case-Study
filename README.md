# UniAvisos — Case Study

> Una notificación parece sencilla.
> Hasta que debe llegar a la persona correcta, desde el área correcta y en el momento correcto.

## Sobre este repositorio

Este repositorio documenta la evolución técnica, las decisiones de desarrollo y los aprendizajes obtenidos durante la construcción de **UniAvisos**, una aplicación Android oficial orientada a mejorar la distribución de avisos universitarios.

Por tratarse de un proyecto institucional, esta publicación no contiene código fuente, configuraciones internas, credenciales, capturas no autorizadas ni información operativa sensible.

El objetivo es presentar el proceso de análisis, desarrollo, pruebas, optimización y planificación sin comprometer la confidencialidad del sistema.

## Problema abordado

La comunicación universitaria puede fragmentarse entre diferentes canales, publicaciones y áreas responsables.

UniAvisos busca centralizar esta información mediante una aplicación móvil capaz de:

* Organizar avisos por áreas
* Mostrar información actualizada
* Permitir preferencias de suscripción
* Enviar notificaciones relevantes
* Facilitar el acceso a los canales oficiales
* Reducir la dependencia de búsquedas manuales en múltiples plataformas

## Mi participación técnica

Durante el desarrollo he trabajado en:

* Análisis de necesidades y requerimientos
* Diseño de flujos de navegación
* Desarrollo Android con Kotlin
* Construcción de interfaces con Jetpack Compose
* Integración con servicios de datos en la nube
* Manejo de contenido dinámico
* Suscripciones por categorías
* Navegación desde notificaciones
* Persistencia de preferencias locales
* Herramientas internas de administración para pruebas
* Optimización de consultas y listeners
* Pruebas en dispositivos Android reales
* Diagnóstico mediante Logcat
* Planeación de escalabilidad
* Documentación técnica y funcional

## Tecnologías utilizadas

* Kotlin
* Jetpack Compose
* Android Studio
* Firebase Firestore
* Firebase Cloud Messaging
* SharedPreferences
* Git
* Logcat

Los identificadores, archivos de configuración, reglas de seguridad y estructuras internas del proyecto no forman parte de esta publicación.


## Documentación técnica

> El repositorio no contiene el código del sistema.
> Contiene las decisiones que explican cómo evolucionó.

La documentación pública se encuentra organizada en los siguientes apartados:

### [Evolución completa](docs/EVOLUTION.md)

Recorrido desde la primera versión Alpha hasta la Beta 4.3 actual, incluyendo:

* Validación inicial del concepto
* Identidad institucional
* Reorganización interna
* Migración de datos locales a servicios remotos
* Avisos y personalización
* Panel administrativo provisional
* Pruebas de extremo a extremo
* Escalabilidad y optimización

### [Arquitectura y modelo operativo](docs/ARCHITECTURE-AND-OPERATING-MODEL.md)

Explicación conceptual de:

* Arquitectura local inicial
* Transición hacia una arquitectura conectada
* Separación entre información global y preferencias locales
* Componentes de la aplicación
* Modelo de servicio institucional
* Flujo de publicación de avisos
* Panel administrativo
* Escalabilidad
* Seguridad
* Estrategia de pruebas
* Arquitectura objetivo

### [Desafíos técnicos y aprendizajes](docs/CHALLENGES-AND-LESSONS.md)

Análisis de los principales problemas encontrados durante el desarrollo:

* Migración desde datos locales
* Contenido dinámico
* Navegación desde notificaciones
* Preferencias por dispositivo
* Administración provisional
* Listeners innecesarios
* Consistencia de contadores
* Operaciones coordinadas
* Costos de infraestructura
* Pruebas en dispositivos reales

### [Roadmap técnico](docs/ROADMAP.md)

Plan de evolución propuesto:

```text
Beta 4.3 → Escalabilidad
Beta 4.4 → Experiencia visual
Beta 4.5 → Persistencia y sincronización
Versión 5.0 → Seguridad y producción
```

### [Confidencialidad y alcance](docs/CONFIDENTIALITY.md)

Define los límites de esta publicación y el material que permanece protegido:

* Código fuente
* Configuraciones
* Infraestructura
* Datos institucionales
* Operaciones administrativas
* Capturas no autorizadas

---

## Estado actual

```text
[ PROJECT STATUS ]

Current version: Beta 4.3
Current focus: Scalability and listener optimization
Source code: Restricted
Official screenshots: Pending authorization
Repository type: Public technical case study
```

La Beta 4.3 se encuentra enfocada en reducir operaciones remotas innecesarias, mantener consistencia entre avisos e indicadores y preparar el sistema para una estrategia posterior de almacenamiento local y sincronización inteligente.

## Evidencia visual

Las capturas oficiales permanecen pendientes de autorización institucional.

Hasta contar con una aprobación expresa, este repositorio no mostrará pantallas reales, paneles administrativos ni recursos gráficos oficiales.

Cuando se autorice su publicación, las imágenes deberán:

* Mostrar únicamente pantallas aprobadas
* No contener datos personales
* No exponer configuraciones
* No mostrar herramientas restringidas
* Ser revisadas antes de incorporarse al repositorio

```text
[ VISUAL EVIDENCE ]

Authorization: Pending
Publication status: Restricted
Next review: Institutional approval
```

## Evolución general

### Alpha

Se definieron las primeras pantallas, categorías de información y rutas principales de navegación.

### Beta 4.0

La administración de áreas evolucionó hacia una estructura dinámica, permitiendo modificar contenido sin depender de valores completamente fijos dentro de la aplicación.

### Beta 4.1

Se incorporaron avisos en tiempo real, preferencias de usuario, suscripciones y funciones de personalización local.

### Beta 4.2

Se desarrollaron herramientas internas para administrar contenido durante las pruebas y validar el flujo completo del sistema.

### Beta 4.3

El trabajo se enfocó en escalabilidad, reducción de consultas innecesarias y actualización eficiente de información relacionada con avisos.

La evolución detallada puede consultarse en:

[`docs/EVOLUTION.md`](docs/EVOLUTION.md)

## Principal desafío técnico

Uno de los retos detectados fue que algunas pantallas podían mantener operaciones activas para categorías que el usuario no había seleccionado.

La solución consistió en reorganizar la lógica para procesar únicamente la información necesaria según las preferencias del usuario.

Esto permitió:

* Reducir operaciones innecesarias
* Mejorar el control del ciclo de vida
* Preparar la aplicación para crecer
* Mantener una experiencia más eficiente

No se publican fragmentos de código ni detalles internos de implementación.

## Arquitectura conceptual

La aplicación puede representarse de forma general así:

```text
Usuario
   │
   ▼
Aplicación Android
   │
   ├── Navegación e interfaz
   ├── Preferencias locales
   ├── Suscripciones
   └── Gestión de avisos
   │
   ▼
Servicios de datos y notificaciones
   │
   ▼
Contenido administrado por áreas autorizadas
```

La explicación completa se encuentra en:

[`docs/ARCHITECTURE-CONCEPT.md`](docs/ARCHITECTURE-CONCEPT.md)

## Evidencia visual

Las capturas oficiales se encuentran pendientes de autorización institucional.

Hasta recibir autorización expresa, este repositorio permanecerá sin imágenes reales de la aplicación.

Cuando sean aprobadas, únicamente se publicarán capturas:

* Autorizadas
* Sin datos personales
* Sin información interna
* Sin paneles restringidos
* Sin identificadores o configuraciones visibles
* Revisadas antes de su publicación

## Próximos objetivos

* Mejoras visuales y de experiencia
* Almacenamiento local estructurado
* Sincronización inteligente
* Autenticación
* Gestión de roles
* Reglas de seguridad para producción
* Reducción adicional de operaciones remotas
* Mejor control de estados y errores

Consulta el roadmap en:

[`docs/ROADMAP.md`](docs/ROADMAP.md)

## Confidencialidad

Este caso de estudio no contiene:

* Código fuente
* Archivos APK
* Credenciales
* Tokens
* Configuraciones de servicios
* Identificadores internos
* Reglas de seguridad
* Datos de usuarios
* Información administrativa
* Capturas no autorizadas
* Documentación institucional restringida

Consulta la política de publicación en:

[`docs/CONFIDENTIALITY.md`](docs/CONFIDENTIALITY.md)

---

No todos los sistemas necesitan mostrar su código para demostrar su evolución.

A veces las decisiones cuentan mejor la historia que los archivos.

**edHash**
