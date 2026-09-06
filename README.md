# SensePad

Wearable BLE de 5 botones para personas con discapacidad visual. Permite disparar acciones del celular (navegación, llamadas, mensajes de WhatsApp) con el teléfono guardado en un bolso o mochila, pantalla apagada, audio privado por un auricular.

Tres ejes: **rápido, seguro, privado**.

## Componentes

El sistema tiene tres piezas que se comunican entre sí:

- **Firmware** (`firmware/`): código C++ para el ESP32-C3 que corre en el dispositivo físico. Detecta los botones y emite el número por Bluetooth Low Energy.
- **App móvil** (`app/`): "Botonera", una app Flutter para Android que se conecta al dispositivo por BLE, recibe el número de botón y dispara la acción correspondiente en el celular.
- **Backend web** (`web/`): aplicación Java (Servlet + JSP + JDBC + MySQL sobre Tomcat 10) donde se configuran los botones de cada usuario. Devuelve las acciones a la app en formato `numero|tipo|valor`.

## Arquitectura

[SensePad físico] --BLE--> [App Botonera en el celular] --HTTP--> [Backend web]
ESP32-C3 Flutter Servlet + MySQL

## Equipo

Proyecto desarrollado por estudiantes de 5° año Técnico en Computación del Instituto Técnico Nuestra Señora de Fátima (CABA).

Docentes coordinadores: Sebastián (web/backend), Mariano (app Android y base de datos).

## Instituciones colaboradoras

- Escuela N° 35 "José Manuel Estrada" (pruebas con usuarios)
- UTN, cátedra de Diseño Tecnológico (refinamiento del producto)
- Escuela N° 37 D.E. 3 (pruebas planificadas)

## Reconocimientos

Mención destacada en la instancia jurisdiccional CABA de la Feria Nacional de Educación, Ciencias, Artes y Tecnología 2026. Único proyecto de Educación Media distinguido en el eje Tecnología (405 proyectos presentados).

Clasificado a la instancia nacional en Córdoba, 22 al 28 de noviembre de 2026.

## Documentación

En la carpeta `docs/` está la Carpeta de Campo, el Informe del proyecto, el registro pedagógico y material audiovisual.
