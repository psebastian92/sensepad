# Planificación

Documento estratégico del proyecto SensePad rumbo a la instancia nacional de la Feria de Educación, Ciencias, Artes y Tecnología en Córdoba (23 al 27 de noviembre de 2026).

Esta es la vista de conjunto: equipo, ejes de trabajo, decisiones cerradas y prioridades. Las tareas concretas viven en [Issues](../../issues) y su estado se sigue en el [Project](../../projects) del repositorio.

## Equipo estudiantil y roles

Cuatro estudiantes de 5° año Técnico en Computación se reparten el trabajo en frentes complementarios:

- **Allison**: parte física del dispositivo. Hardware, plaqueta, alimentación.
- **Agustina**: firmware del dispositivo. Código Arduino y comunicación BLE.
- **Rodrigo**: backend, servicios y configuración de la app. Base de datos, autenticación, endpoints, integración con el firmware.
- **Mayerly**: frontend, identidad visual, folletos y stand.

Los frentes se cruzan a propósito. Agustina y Allison trabajan juntas el dispositivo. Agustina y Rodrigo definen y mejoran las acciones que dispara cada botón. Rodrigo y Mayerly ajustan la configuración de la app. La información del dispositivo que llega a la app pasa después por Mayerly para lo visual.

Coordinación docente: Sebastián (web/backend) y Mariano (app y base de datos).

## Ejes de trabajo

### 1. Dispositivo y firmware

Cierre del hardware: definición final de GPIOs, esquematización de la plaqueta en EasyEDA, definición del tamaño final de la botonera y revisión del sistema de alimentación (TP4056, LiPo en paralelo, BMS y step-down). Elección del método de medición de batería: MAX17048 (pequeño, entrega porcentaje directo) vs. lectura ADC del ESP32-C3.

En firmware: continuidad del código Arduino de comunicación BLE, exposición de un parámetro que la app pueda leer (batería y estado de conexión), confirmación de pulsación por doble tap e integración de las credenciales generadas por `fabricar.py` a través de `credenciales.h`.

### 2. Aplicación Flutter

Simplificación general de la app y trabajo sobre cuatro frentes:

- **Roles y autenticación**: la app maneja dos perfiles, usuario no vidente y usuario asistente. Vinculación con Google como método de login, y auto-registro por dispositivo. Al parear por BLE, la app lee el `id_dispositivo` y el token, y crea o asocia la cuenta contra el backend.
- **Acciones que dispara el dispositivo**: mejora de las acciones actuales y llamado automático. Hoy al apretar el botón la app abre el marcador con el número cargado pero no ejecuta la llamada. Corresponde que el botón dispare la llamada directa. Además, permisos para WhatsApp directo y llamadas desde la app.
- **Integración con el dispositivo**: fixes BLE pendientes (`setNotifyValue`, `autoConnect`, `mode=w` en Maps, TTS duplicado al conectar), lectura del estado y batería, y replanteo del sistema SOS.
- **Ubicación**: validación del GPS del teléfono, registro de última ubicación conocida (cubre pérdida o robo sin costo de hardware) y alerta de proximidad BLE ante desconexión.

Sobre el final del recorrido, y solo si el resto está estable, se evalúa la incorporación de un asistente con IA en la app. Es la última decisión de alcance del proyecto y no condiciona nada de lo anterior.

### 3. Backend y web

Decisión de arquitectura pendiente: Spring Boot vs. continuidad en Servlet/JSP. Punto de no retorno el 28 de septiembre de 2026. Si Spring Boot no está devolviendo JSON básico para esa fecha, se aborta y se sigue con la stack actual.

En paralelo: migración del nombre (SenseBagpack a SensePad, con ambos endpoints conviviendo durante la transición), setup de Google OAuth, tabla `dispositivos_precargados` en MySQL integrada con `fabricar.py`, endpoint para configurar el nombre BLE por dispositivo y definición de qué campos puede modificar el usuario final.

Sobre la web pública: actualización del contenido con datos reales, decisión sobre estática vs. dinámica según su función, publicación (dominio y hosting) y mejoras visuales coordinadas con diseño.

### 4. Diseño y presentación

Continuidad de la identidad visual, diseño del stand para Córdoba, folletos más claros y en mayor cantidad, y material gráfico para la feria.

Los soportes de la presentación se preparan aparte y con peso propio: la metodología de trabajo del equipo (cómo se organizaron las decisiones, las duplas, la iteración), qué aprendimos durante el desarrollo y las alternativas descartadas con su justificación. Es lo que se lleva a exponer frente a los evaluadores.

### 5. Organización y feria nacional

Pasaje de todos los pendientes a Issues y Projects para el seguimiento real del trabajo, documentación del flujo de datos entre dispositivo, app, backend y servicios externos, y los entregables formales de la feria: Carpeta de Campo, informe del proyecto, registro pedagógico y video del proceso.

Logística de Córdoba: confirmación de cuántos alumnos viajan.

Corrección de los errores del artículo publicado por el GCBA (botones descritos como "braille", GPS integrado en el dispositivo) antes de cualquier salida a prensa.

## Decisiones cerradas

Estas alternativas se evaluaron y se descartaron. Se documentan porque son parte del hilo argumental que se lleva a la feria: cada decisión razonada es una fortaleza del proyecto.

**MAC address como identificador del dispositivo.** Descartada por la aleatorización de direcciones que hacen Android e iOS por privacidad y por las restricciones de Core Bluetooth. Reemplazada por un `id_dispositivo` público (por ejemplo `SensePad_007`) más un token secreto hasheado en MySQL.

**GPS o GNSS embebido en el dispositivo.** Descartado por redundancia arquitectónica, obstrucción de la antena dentro del bolso y porque el GPS del teléfono es superior (multiconstelación GNSS, A-GPS, posicionamiento por WiFi y sensor fusion). Reemplazado por el registro de última ubicación conocida vía teléfono.

**Gafas de conducción ósea.** Descartadas tras la visita a la Escuela N° 35 "José Manuel Estrada". El feedback de los usuarios confirmó que alcanza con un auricular.

**Registro manual de cuenta.** Reemplazado por auto-registro BLE al parear el dispositivo. La configuración accesible es parte de la accesibilidad: cualquier tecnología que requiera un técnico vidente para configurarla no es accesible por sí misma, es tecnología que se puede hacer accesible con ayuda externa.

## Hitos

- **28 de septiembre de 2026**: punto de no retorno de la decisión Spring Boot. Milestone `Deadline Spring Boot`.
- **22 al 28 de noviembre de 2026**: instancia nacional de la feria en Córdoba. Milestone `Feria Nacional`.

## Prioridades hasta la feria

**Alto.** Firmware estable y BLE confiable, llamado automático desde el botón, auto-registro por dispositivo, sistema SOS replanteado, ubicación (última conocida y alerta de proximidad), stand, folletos y video.

**Medio.** Google OAuth (condicionado a la decisión Spring Boot), permisos de WhatsApp y llamadas, publicación de la web.

**A decidir al cierre.** Incorporación o no de un asistente con IA en la app.

## Cómo se trabaja en el repo

- Cada tarea concreta es un **Issue** con responsable, labels y milestone.
- El **Project** (vista kanban) muestra en qué está trabajando cada uno: Backlog, Esta semana, En curso, Bloqueado, Hecho.
- Los **Milestones** agrupan issues por fecha objetivo.
- Este documento se toca cuando cambia algo estratégico: un rol, una decisión cerrada, un hito. Las tareas del día a día no viven acá.
