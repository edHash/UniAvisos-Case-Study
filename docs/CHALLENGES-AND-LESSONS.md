# Desafíos técnicos y aprendizajes

> Los errores visibles suelen ser los más fáciles.
> Los peligrosos son aquellos que permiten que el sistema siga funcionando… mientras crece de la manera equivocada.

Este documento reúne algunos de los principales desafíos técnicos encontrados durante el desarrollo de **UniAvisos**, las decisiones tomadas y los aprendizajes obtenidos.

Por tratarse de un proyecto oficial, no se incluyen fragmentos de código, nombres internos, configuraciones, reglas, identificadores ni información institucional restringida.

```text
[ TECHNICAL REVIEW ]

Project: UniAvisos
Current version: Beta 4.3
Focus: Architecture, integration, scalability and validation
Implementation details: Restricted
```

---

# 1. Pasar de datos locales a un sistema conectado

## Desafío

Las primeras versiones utilizaban información definida dentro de la aplicación.

Esto permitió validar rápidamente:

* Pantallas
* Navegación
* Organización por áreas
* Experiencia del usuario
* Identidad visual

Sin embargo, una aplicación oficial de avisos no podía depender permanentemente de información incluida en cada instalación.

Cualquier actualización habría requerido:

1. Modificar el proyecto.
2. Generar una nueva versión.
3. Distribuirla.
4. Esperar a que los usuarios actualizaran.

## Decisión

Separar la interfaz móvil de la información operativa y utilizar una fuente remota central.

La aplicación dejó de contener directamente toda la información y comenzó a:

* Solicitarla
* Procesarla
* Representarla
* Reaccionar ante cambios

## Resultado

El contenido pudo actualizarse sin reinstalar la aplicación y distintos dispositivos comenzaron a consultar una misma fuente de información.

## Aprendizaje

Migrar a servicios en la nube no consiste únicamente en cambiar dónde se guardan los datos.

También obliga a diseñar:

* Estados de carga
* Manejo de errores
* Integridad
* Actualización en tiempo real
* Sincronización
* Seguridad
* Control de costos

```text
Local data → Fast prototype
Remote data → Operational system
```

---

# 2. Gestionar contenido dinámico

## Desafío

Las áreas universitarias no debían permanecer completamente fijas dentro del código.

Podían necesitar cambios en:

* Nombre
* Descripción
* Orden
* Estado
* Canal oficial
* Disponibilidad

## Decisión

Representar las áreas mediante información administrable remotamente.

La interfaz debía adaptarse al contenido recibido, en lugar de depender únicamente de una lista fija.

## Resultado

Fue posible activar, desactivar, ordenar y modificar áreas sin recompilar la aplicación.

## Aprendizaje

El contenido dinámico mejora la flexibilidad, pero también introduce nuevos escenarios:

* Campos incompletos
* Datos mal formados
* Cambios mientras la pantalla está abierta
* Elementos desactivados
* Ordenamientos inesperados
* Fallas de red

La aplicación debe asumir que la información remota puede cambiar.

No debe asumir que siempre llegará perfecta.

---

# 3. Coordinar la navegación desde notificaciones

## Desafío

Una notificación puede abrir la aplicación cuando:

* Se encuentra cerrada
* Está en segundo plano
* Todavía carga información
* Aún no conoce todas las áreas disponibles

Intentar navegar inmediatamente podía provocar que el destino todavía no existiera dentro del estado cargado.

## Decisión

Coordinar el evento externo con el estado interno de la aplicación.

El flujo conceptual se convirtió en:

```text
Notificación recibida
        │
        ▼
Identificar destino
        │
        ▼
Esperar información necesaria
        │
        ▼
Validar destino
        │
        ▼
Navegar
```

## Resultado

La navegación dejó de depender únicamente del evento recibido y comenzó a considerar la disponibilidad real de los datos.

## Aprendizaje

Los eventos externos no conocen el ciclo de vida interno de la aplicación.

Una navegación correcta requiere sincronizar ambos mundos.

---

# 4. Separar contenido global y preferencias personales

## Desafío

Se necesitaba permitir que una persona ocultara un aviso sin eliminarlo para todos los demás.

## Decisión

Separar claramente:

### Información global

Pertenece al sistema y afecta a todos los usuarios.

### Preferencias locales

Pertenecen a un dispositivo y modifican únicamente su experiencia.

## Resultado

Los avisos ocultos dejaron de mostrarse localmente, pero continuaron disponibles para otros usuarios y dentro de la fuente remota.

Los contadores visibles también debían considerar esta personalización.

## Aprendizaje

No toda acción del usuario necesita convertirse en una escritura remota.

Algunas decisiones deben permanecer locales porque:

* No afectan a terceros
* Reducen operaciones
* Protegen la privacidad
* Simplifican el modelo de datos

```text
Global content remains global.
Personal choices remain personal.
```

---

# 5. Construir un panel administrativo provisional

## Desafío

Para validar el sistema completo era necesario comprobar no solo cómo se consultaba el contenido, sino cómo entraba al sistema.

## Decisión

Desarrollar herramientas internas para pruebas controladas que permitieran:

* Crear avisos
* Cambiar estados
* Administrar áreas
* Modificar orden
* Validar actualizaciones remotas

## Resultado

Se pudo probar el flujo completo:

```text
Crear → Almacenar → Actualizar → Consultar
```

## Riesgo identificado

El panel funcionaba, pero todavía no contaba con todos los controles necesarios para producción:

* Autenticación
* Roles
* Permisos
* Auditoría
* Separación administrativa
* Reglas restrictivas

## Aprendizaje

Una función administrativa no es solamente una pantalla adicional.

Es una capacidad privilegiada.

Cuando una herramienta puede modificar información global, debe diseñarse bajo un modelo de confianza distinto al de la aplicación de usuario.

---

# 6. Detectar listeners innecesarios

## Desafío

La actualización en tiempo real funcionaba correctamente, pero algunas pantallas podían mantener listeners sobre áreas que el usuario no había seleccionado.

Con pocos datos, el problema era difícil de percibir.

Con más áreas y usuarios, podía generar:

* Más lecturas
* Mayor consumo
* Uso innecesario de red
* Más procesamiento
* Costos adicionales
* Mayor complejidad de ciclo de vida

## Diagnóstico

Se revisó cuántas operaciones permanecían activas según las suscripciones del usuario.

Se detectó que el número de listeners no siempre correspondía con la información realmente necesaria.

## Decisión

Reorganizar la lógica para escuchar únicamente las áreas seleccionadas.

## Resultado

El comportamiento esperado pasó a ser:

```text
0 suscripciones → 0 listeners relacionados
1 suscripción   → 1 listener relacionado
N suscripciones → N listeners necesarios
```

## Aprendizaje

La actualización en tiempo real debe utilizarse de manera selectiva.

Escuchar todo no hace que una aplicación sea más reactiva.

Solo hace que procese más información.

```text
[ OPTIMIZATION RULE ]

Do not listen because data exists.
Listen because the user needs it.
```

---

# 7. Evitar reinicios innecesarios

## Desafío

Aunque los listeners estuvieran relacionados con las suscripciones correctas, podían reiniciarse cuando cambiaban otros datos generales.

## Decisión

Utilizar una referencia estable basada en las preferencias reales del usuario.

Los listeners debían reiniciarse cuando cambiaban las suscripciones, no cuando cualquier objeto relacionado era recreado o actualizado.

## Resultado

Se redujeron ciclos innecesarios de:

```text
Cerrar listener
      ↓
Crear listener
      ↓
Volver a cargar datos
```

## Aprendizaje

En una interfaz reactiva, dos valores pueden representar la misma información y, aun así, ser tratados como objetos distintos.

La estabilidad de las dependencias también forma parte del rendimiento.

---

# 8. Mantener consistencia entre avisos y contadores

## Desafío

Al crear un aviso activo debían actualizarse también los indicadores relacionados.

Si las operaciones se ejecutaban por separado, podían producirse estados parciales:

```text
Aviso creado
Contador sin actualizar
```

o:

```text
Contador actualizado
Aviso no creado
```

## Decisión

Coordinar las escrituras relacionadas dentro de una misma operación lógica.

## Resultado

Cuando se registra contenido activo, también se actualizan sus indicadores asociados.

Cuando el contenido se crea inactivo, el contador no debe incrementarse.

## Validación

Se realizaron pruebas diferenciadas con:

* Avisos activos
* Avisos inactivos
* Comparación de valores antes y después
* Registros de depuración
* Observación de la fuente remota

## Aprendizaje

La consistencia no depende únicamente de que cada escritura funcione.

Depende de que todas las escrituras relacionadas representen el mismo estado.

---

# 9. Diseñar pensando en el costo operativo

## Desafío

Los servicios en la nube simplifican muchas funciones, pero cada operación puede representar consumo de recursos.

## Factores considerados

* Lecturas
* Escrituras
* Listeners
* Notificaciones
* Transferencia de información
* Almacenamiento
* Número de usuarios
* Frecuencia de actualización

## Decisión

Tratar la optimización no solo como un problema de rendimiento, sino también como una responsabilidad operativa.

## Aprendizaje

Una consulta innecesaria puede parecer insignificante.

Multiplicada por:

* Muchos usuarios
* Varias áreas
* Horas de uso
* Actualizaciones constantes

puede convertirse en un problema real.

La escalabilidad técnica y la sostenibilidad operativa están conectadas.

---

# 10. Probar en dispositivos reales

## Desafío

Algunos comportamientos no se observan de la misma manera en un entorno simulado.

## Pruebas realizadas

* Navegación
* Ciclo de vida
* Suscripciones
* Persistencia local
* Notificaciones
* Apertura desde eventos externos
* Cambios remotos
* Contadores
* Contenido activo e inactivo

## Herramientas utilizadas

* Android Studio
* Dispositivo Android físico
* Logcat
* Consola de datos
* Comparación manual de estados
* Repetición de escenarios

## Resultado

Fue posible comprobar no solo si la interfaz funcionaba, sino cómo reaccionaba la aplicación ante eventos y estados reales.

## Aprendizaje

El emulador ayuda a desarrollar.

El dispositivo real ayuda a descubrir.

---

# 11. Reconocer los límites de una versión funcional

## Desafío

Una aplicación puede funcionar correctamente y aun no estar preparada para producción.

## Elementos todavía pendientes

* Autenticación formal
* Roles
* Reglas de seguridad definitivas
* Separación administrativa
* Persistencia local estructurada
* Pruebas automatizadas
* Manejo de errores más completo
* Auditoría
* Monitoreo
* Distribución formal

## Aprendizaje

“Funciona” y “está lista para producción” no significan lo mismo.

Un producto de producción necesita:

* Seguridad
* Trazabilidad
* Recuperación
* Mantenimiento
* Control de acceso
* Observabilidad
* Documentación

Reconocer lo que todavía falta también forma parte de la ingeniería.

---

# 12. Priorizar arquitectura antes que estética

## Decisión

Antes de realizar la siguiente renovación visual, se decidió atender los problemas de escalabilidad.

El orden definido fue:

```text
Beta 4.3 → Escalabilidad
Beta 4.4 → Experiencia visual
Beta 4.5 → Persistencia y sincronización
Versión 5.0 → Seguridad y producción
```

## Motivo

Construir una nueva interfaz sobre una base que todavía realiza operaciones innecesarias obligaría a corregir problemas técnicos y visuales al mismo tiempo.

## Aprendizaje

La mejora más visible no siempre es la más urgente.

A veces la decisión correcta ocurre detrás de la pantalla.

---

# Conclusiones generales

El desarrollo de UniAvisos ha permitido trabajar con desafíos relacionados con:

* Arquitectura móvil
* Datos remotos
* Estado local
* Navegación
* Notificaciones
* Consistencia
* Escalabilidad
* Seguridad
* Administración
* Pruebas
* Planeación de versiones

Cada etapa ha cambiado la forma en que se comprende el sistema.

La primera pregunta era:

> ¿Cómo mostramos avisos?

Después aparecieron otras:

* ¿Quién controla la información?
* ¿Cómo se actualiza?
* ¿Qué debe permanecer local?
* ¿Cuándo debemos consultar?
* ¿Cuándo debemos escuchar?
* ¿Cómo evitamos estados incompletos?
* ¿Qué funciones requieren mayor seguridad?
* ¿Cómo se prepara la aplicación para crecer?

```text
[ LESSONS LEARNED ]

Working software is the beginning.
Scalable, secure and maintainable software is the objective.
```

Los errores ayudaron a encontrar problemas.

Las pruebas ayudaron a comprobar soluciones.

La arquitectura ayudó a evitar que los mismos problemas regresaran con otra forma.

**edHash**
