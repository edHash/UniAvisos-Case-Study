# Roadmap técnico de UniAvisos

> Un sistema sin ruta puede seguir avanzando.
> El problema es que nadie sabe hacia dónde.

Este documento presenta la planificación técnica de **UniAvisos** desde la versión actual hasta su preparación para un entorno de producción.

El roadmap no constituye una fecha de lanzamiento institucional ni compromete públicamente plazos oficiales. Representa la secuencia técnica propuesta para continuar desarrollando el sistema de forma controlada.

Por motivos de confidencialidad, no se incluyen configuraciones internas, responsables institucionales, infraestructura privada ni detalles restringidos de implementación.

```text
[ ROADMAP STATUS ]

Current version: Beta 4.3
Current focus: Scalability foundation
Next milestone: Beta 4.4
Production target: Version 5.0
Source code: Restricted
```

---

# 1. Principio de evolución

El orden de las siguientes versiones responde a una decisión arquitectónica:

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

La renovación visual no se colocó antes de la optimización técnica porque una interfaz nueva no corrige:

* Consultas innecesarias
* Reinicios de listeners
* Dependencia constante de la red
* Falta de almacenamiento local
* Ausencia de autenticación
* Operaciones administrativas sin separación formal

La prioridad es fortalecer primero la estructura sobre la que se construirá la experiencia final.

---

# 2. Beta 4.3 — Escalabilidad base

## Estado

```text
Status: En desarrollo
```

## Objetivo

Reducir operaciones remotas innecesarias y preparar una base que pueda soportar más áreas, avisos y usuarios.

## Trabajo completado

* Carga dinámica de áreas activas
* Uso de información remota real
* Eliminación progresiva de datos simulados
* Reducción de listeners según suscripciones
* Uso de referencias estables para evitar reinicios
* Actualización coordinada de avisos e indicadores
* Contadores agregados por área
* Registro conceptual de versiones de contenido
* Pruebas con avisos activos e inactivos
* Validación mediante Logcat y dispositivo real

## Trabajo pendiente

* Extender la optimización a todas las pantallas relevantes
* Revisar ciclos de vida de listeners restantes
* Centralizar más responsabilidades de acceso a datos
* Mejorar estados de error
* Documentar escenarios de recuperación
* Medir operaciones en distintos perfiles de usuario
* Validar comportamiento con mayor volumen de avisos

## Criterios de cierre

Beta 4.3 podrá considerarse cerrada cuando:

* Un usuario sin suscripciones no mantenga listeners innecesarios
* Las operaciones activas correspondan con sus preferencias
* Los contadores permanezcan consistentes
* Los avisos activos e inactivos actualicen correctamente sus indicadores
* No exista dependencia funcional de datos de prueba
* Las pantallas principales utilicen una estrategia coherente de consulta
* Los escenarios principales hayan sido repetidos en dispositivo real

```text
[ BETA 4.3 EXIT CONDITION ]

Correct data
+
Necessary listeners only
+
Consistent counters
+
Repeatable tests
```

---

# 3. Beta 4.4 — Experiencia visual y usabilidad

## Estado

```text
Status: Planificada
Dependency: Cierre técnico de Beta 4.3
```

## Objetivo

Mejorar la experiencia visual sin modificar innecesariamente la lógica establecida en la etapa de escalabilidad.

## Áreas de trabajo

### Jerarquía visual

* Diferenciar títulos, información secundaria y acciones
* Mejorar legibilidad
* Reducir saturación
* Priorizar avisos importantes
* Mantener coherencia institucional

### Componentes

* Unificar tarjetas
* Unificar botones
* Estandarizar estados vacíos
* Estandarizar indicadores de carga
* Mantener comportamiento consistente entre pantallas

### Navegación

* Clarificar rutas
* Mejorar retroalimentación
* Reducir acciones ambiguas
* Revisar comportamiento del menú lateral
* Facilitar el regreso al contexto anterior

### Accesibilidad

* Contraste
* Tamaño de objetivos táctiles
* Compatibilidad con escalado de texto
* Descripciones accesibles
* Estados comprensibles sin depender únicamente del color

### Manejo de estados

Diseñar representaciones claras para:

* Cargando
* Sin conexión
* Sin avisos
* Error temporal
* Contenido desactivado
* Actualización disponible
* Preferencias sin seleccionar

## Riesgos

* Introducir cambios visuales que alteren comportamientos ya validados
* Duplicar componentes en lugar de reutilizarlos
* Priorizar estética sobre claridad
* Aplicar identidad institucional sin revisar lineamientos

## Criterios de cierre

* Componentes principales visualmente consistentes
* Navegación comprensible
* Estados vacíos y de error definidos
* Contraste y legibilidad revisados
* Pruebas en diferentes tamaños de pantalla
* Validación institucional de elementos gráficos necesarios
* Ausencia de regresiones funcionales relevantes

```text
[ BETA 4.4 RULE ]

The interface should not require a manual
to explain its most common actions.
```

---

# 4. Beta 4.5 — Persistencia local y sincronización inteligente

## Estado

```text
Status: Planificada
Dependency: Base funcional estable
```

## Objetivo

Reducir la dependencia de conexión constante y evitar volver a solicitar información que ya se encuentra disponible localmente.

## Arquitectura propuesta

```text
Interfaz
   │
   ▼
Estado / ViewModel
   │
   ▼
Repositorio
   │
   ├── Persistencia local
   └── Servicio remoto
```

## Componentes previstos

### Base local estructurada

Se plantea incorporar persistencia mediante una solución adecuada para Android, como Room, con el objetivo de almacenar:

* Áreas
* Avisos
* Versiones
* Fechas de actualización
* Estados necesarios para sincronización

### Repositorio de datos

La interfaz no debería decidir directamente si la información proviene de memoria, almacenamiento local o servicio remoto.

El repositorio coordinará:

* Lectura local
* Consulta remota
* Actualización de caché
* Exposición de estados
* Resolución de errores

### Control de versiones

Los indicadores agregados permitirán comparar:

```text
Versión remota
      │
      ▼
Versión local
      │
      ├── Iguales → Usar información local
      └── Diferentes → Sincronizar
```

### Funcionamiento sin conexión

La aplicación deberá permitir, dentro de los límites aprobados:

* Consultar información previamente sincronizada
* Mostrar el momento de la última actualización
* Informar que el contenido puede no ser el más reciente
* Reintentar cuando regrese la conectividad

## Estrategia de sincronización

La sincronización deberá evitar dos extremos:

### Consultar siempre

Genera operaciones innecesarias.

### Nunca actualizar

Muestra información obsoleta.

El objetivo será consultar cuando exista una razón verificable:

* Cambio de versión
* Cambio de fecha
* Solicitud manual
* Recuperación de conectividad
* Evento relevante

## Riesgos

* Conflictos entre información local y remota
* Datos obsoletos
* Migraciones de base local
* Duplicados
* Actualizaciones interrumpidas
* Crecimiento descontrolado de almacenamiento

## Criterios de cierre

* Información básica disponible sin conexión
* Sincronización selectiva
* Comparación de versiones funcional
* Repositorio de datos definido
* Manejo de errores y reintentos
* Pruebas de migración
* Pruebas con conexión intermitente
* Recuperación tras una sincronización incompleta

```text
[ BETA 4.5 OBJECTIVE ]

Do not request the entire system again
when only one part has changed.
```

---

# 5. Versión 5.0 — Seguridad y preparación para producción

## Estado

```text
Status: Futura
Dependency: Arquitectura, experiencia y sincronización estables
```

## Objetivo

Transformar el sistema funcional en una solución preparada para distribución formal y operación institucional controlada.

## Autenticación

La versión deberá contemplar:

* Inicio de sesión
* Gestión de sesiones
* Recuperación de acceso
* Validación de identidad
* Revocación de acceso
* Manejo seguro de credenciales

## Roles y permisos

El sistema deberá diferenciar capacidades.

Ejemplo conceptual:

```text
Usuario
  └── Consultar y personalizar

Editor
  └── Crear o modificar contenido autorizado

Administrador
  └── Gestionar áreas, permisos y operaciones globales
```

Los roles exactos dependerán de las políticas institucionales.

## Separación administrativa

El panel provisional deberá:

* Retirarse de la aplicación de usuario, o
* Sustituirse por una solución administrativa controlada

Las operaciones privilegiadas no deben depender de secretos incluidos dentro de la aplicación instalada.

## Reglas de seguridad

Se requerirá definir y validar:

* Quién puede leer
* Quién puede escribir
* Qué campos pueden modificarse
* Qué operaciones requieren privilegios
* Cómo se evita la modificación no autorizada
* Cómo se registra una acción administrativa

## Auditoría

Las operaciones relevantes deberán poder asociarse con:

* Actor
* Acción
* Momento
* Recurso afectado
* Resultado

La auditoría no debe recopilar más información personal de la necesaria.

## Manejo de errores

Se deberá fortalecer:

* Registro controlado
* Mensajes para usuario
* Diferenciación entre error local y remoto
* Recuperación
* Reintentos
* Prevención de exposición de detalles internos

## Distribución

Antes de una publicación formal se deberá revisar:

* Firma de la aplicación
* Configuraciones de producción
* Eliminación de herramientas de laboratorio
* Protección de archivos sensibles
* Reglas de acceso
* Política de privacidad
* Permisos solicitados
* Canales de soporte
* Procedimiento de actualización

## Criterios de cierre

La versión 5.0 no deberá considerarse terminada únicamente porque la aplicación funcione.

También deberá demostrar:

* Autenticación funcional
* Roles aplicados
* Reglas verificadas
* Panel provisional retirado o aislado
* Operaciones privilegiadas protegidas
* Auditoría básica
* Manejo de errores
* Pruebas de seguridad
* Documentación operativa
* Proceso de distribución definido

```text
[ VERSION 5.0 ]

Functional is not enough.
The system must also be controlled,
traceable and recoverable.
```

---

# 6. Estrategia de pruebas por versión

## Beta 4.3

* Conteo de listeners
* Suscripciones
* Avisos activos e inactivos
* Consistencia de contadores
* Cambios remotos
* Ciclo de vida

## Beta 4.4

* Navegación
* Accesibilidad
* Tamaños de pantalla
* Estados visuales
* Regresiones funcionales

## Beta 4.5

* Sin conexión
* Conectividad intermitente
* Sincronización
* Migraciones
* Caché
* Recuperación ante fallos

## Versión 5.0

* Autenticación
* Roles
* Permisos
* Intentos no autorizados
* Auditoría
* Protección de funciones administrativas
* Revisión de configuraciones de producción

---

# 7. Riesgos generales

## Riesgo técnico

Agregar funciones antes de separar responsabilidades.

## Riesgo operativo

Incrementar operaciones remotas conforme crece el número de usuarios.

## Riesgo de seguridad

Mantener capacidades administrativas dentro de un cliente distribuido.

## Riesgo institucional

Publicar información, recursos o capturas sin autorización.

## Riesgo de mantenimiento

Permitir que las decisiones provisionales se conviertan en permanentes.

## Estrategia de mitigación

* Evolución incremental
* Documentación
* Pruebas repetibles
* Separación de responsabilidades
* Revisión de seguridad
* Control de versiones
* Aprobación institucional
* Publicación limitada del caso de estudio

---

# 8. Matriz resumida

| Versión     | Enfoque                                 | Estado        |
| ----------- | --------------------------------------- | ------------- |
| Beta 4.3    | Escalabilidad, listeners y consistencia | En desarrollo |
| Beta 4.4    | Interfaz, accesibilidad y experiencia   | Planificada   |
| Beta 4.5    | Room, caché y sincronización            | Planificada   |
| Versión 5.0 | Autenticación, roles y producción       | Futura        |

---

# 9. Definición de avance

Una versión no se considerará terminada únicamente porque se haya agregado una función.

Cada etapa deberá cumplir cuatro condiciones:

```text
Implementación
     +
Validación
     +
Documentación
     +
Ausencia de riesgos críticos conocidos
```

La evolución de UniAvisos no busca acumular versiones.

Busca reducir la distancia entre un prototipo funcional y un sistema institucional sostenible.

```text
[ END OF ROADMAP ]

Next milestone: Beta 4.4
Current priority: Close Beta 4.3 correctly
Production shortcut: Not available
```

No existe una ruta rápida hacia producción.

Solo decisiones que permiten llegar sin convertir cada versión en una deuda para la siguiente.

**edHash**
