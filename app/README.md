# SensePad — App Botonera

Aplicación Flutter para Android. Se conecta al SensePad por Bluetooth Low Energy, recibe el número de botón presionado, consulta al backend qué acción tiene asignada ese botón para ese dispositivo, y la ejecuta en el celular.

## Acciones soportadas

- `maps`: abre Google Maps con navegación al destino configurado
- `llamar`: inicia una llamada al número configurado
- `whatsapp`: abre WhatsApp con contacto y mensaje predefinidos
- `mensaje`: reproduce un mensaje por TTS

## Stack

- Flutter / Dart
- Paquetes: `flutter_blue_plus`, `http`, `url_launcher`, `flutter_tts`, `wakelock_plus`, `permission_handler`

## Comunicación con el backend

La app consulta el backend en `appsjavatest.fatimarem.edu.ar` para obtener la acción de cada botón. El backend responde en formato `numero|tipo|valor` (parseo: `partes.length >= 3`).

## Qué falta subir

Desde la máquina donde se desarrolla la app:

- Carpeta `lib/` con el código Dart
- `pubspec.yaml` y `pubspec.lock`
- Carpeta `android/` (respetando el `.gitignore`)
- Recursos gráficos si los hay

Lo que **no** se sube:

- `build/`
- `.dart_tool/`
- `.idea/`, `.vscode/`