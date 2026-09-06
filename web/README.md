# SensePad — Backend Web

Aplicación Java que administra los usuarios, dispositivos y las acciones asignadas a cada botón. Los usuarios (o alguien de confianza) configuran acá qué hace cada botón de su SensePad.

## Stack

- Java Servlets + JSP
- JDBC para acceso a datos
- MySQL como base de datos
- Tomcat 10+ (Jakarta EE, paquete `jakarta.servlet.*`)
- Se despliega como WAR

## Formato de respuesta

Las acciones asignadas a cada botón se devuelven en formato:
numero|tipo|valor


Tipos de acción disponibles: `maps`, `llamar`, `whatsapp`, `mensaje`.

Regla de parseo en el cliente: `partes.length >= 3`.

## Despliegue

Actualmente publicado en `appsjavatest.fatimarem.edu.ar`.

## Qué falta subir

Desde la máquina donde se desarrolla el backend:

- Carpeta `src/` con los Servlets
- Carpeta `WebContent/` o `webapp/` con los JSP
- Configuración del proyecto Eclipse o `pom.xml` según corresponda
- `config.example.properties` con la estructura de conexión (sin credenciales reales)

Lo que **no** se sube:

- `target/`
- `.classpath`, `.settings/`, `.project`
- El archivo real de conexión a la base de datos