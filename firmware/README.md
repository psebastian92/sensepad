# SensePad — Firmware

Código del dispositivo físico. Corre en un ESP32-C3 Super Mini y expone 5 botones por Bluetooth Low Energy.

## Hardware

- ESP32-C3 Super Mini
- 5 tact switches 6x6x5mm en GPIO 12, 13, 14, 27 y 26 (INPUT_PULLUP)
- Módulo de carga TP4056 USB-C
- Pack LiPo 602535 en paralelo (1200 mAh total)
- PCB adaptable universal 45x76mm
- Conectores JST XH 2.54 de 2 pines por botón

## Software

Se compila con Arduino IDE. Cada dispositivo tiene un identificador único (formato `SensePad_007`) que se anuncia por BLE.

## Credenciales por dispositivo

Al compilar se necesita un archivo `credenciales.h` que contiene el ID del dispositivo y su token secreto. Ese archivo lo genera el script `fabricar.py` en el momento de producción y **no se sube al repositorio**.

En su lugar se incluye `credenciales.example.h` como referencia de la estructura.

## Qué falta subir

Desde la máquina donde se desarrolla el firmware:

- El `.ino` principal
- Módulos auxiliares si los hay
- `credenciales.example.h`
- Esquema del PCB cuando esté listo en EasyEDA