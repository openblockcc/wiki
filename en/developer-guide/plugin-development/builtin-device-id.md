---
title: Built-In Device IDs
description: 
published: true
date: 2024-10-17T04:43:31.984Z
tags: developer
editor: markdown
dateCreated: 2024-10-17T04:43:31.984Z
---

# Built-in Device IDs

OpenBlock external resource packages can define devices derived from built-in devices, allowing for the addition of third-party control boards or product kits. The currently built-in device IDs in OpenBlock are as follows.

| Device ID                  | Device                   | Programming Framework    | Remarks |
| -------------------------- | ------------------------ | ----------------------- | ------- |
| arduinoUno                 | Arduino UNO R3           | Arduino C/C++            |         |
| arduinoNano                | Arduino Nano             | Arduino C/C++            | Uses old bootloader, includes A6, A7 pins |
| arduinoUnoUltra            | Arduino UNO R3 Variant1  | Arduino C/C++            | For third-party extensions, includes A6, A7 pins on Arduino UNO R3 |
| arduinoUnoSE               | Arduino UNO R3 Variant2  | Arduino C/C++            | For third-party extensions, excludes any hardware-based blocks on Arduino UNO R3 |
| arduinoLeonardo            | Arduino Leonardo         | Arduino C/C++            |         |
| makeyMakey                 | MakeyMakey               | Arduino C/C++            |         |
| arduinoMega2560            | Arduino Mega 2560        | Arduino C/C++            |         |
| arduinoEsp32               | Esp32                    | Arduino C/C++            |         |
| arduinoEsp8266             | Esp8266                  | Arduino C/C++            |         |
| microPythonEsp8266         | Esp8266                  | Standard MicroPython      |         |
| arduinoEsp8266NodeMCU      | Esp8266 Node MCU         | Arduino C/C++            |         |
| microPythonEsp8266NodeMCU  | Esp8266 Node MCU         | Standard MicroPython      |         |
| arduinoK210                | K210                     | Arduino C/C++            |         |
| microPythonK210            | K210                     | Standard MicroPython      |         |
| arduinoK210MaixDock        | MaixDock                 | Arduino C/C++            |         |
| microPythonK210MaixDock    | MaixDock                 | Standard MicroPython      |         |
| arduinoK210Maixduino       | Maixduino                | Arduino C/C++            |         |
| microPythonK210Maixduino   | Maixduino                | Standard MicroPython      |         |
| arduinoRaspberryPiPico     | Raspberry Pi Pico        | Arduino C/C++            |         |
| microPythonRaspberryPiPico | Raspberry Pi Pico        | Microbit MicroPython      |         |
| microbit                   | Micro:bit                | Standard MicroPython      |         |
| microbitV2                 | micro:bit V2             | Microbit MicroPython      |         |

> Note: Devices with the programming framework listed as `Standard MicroPython` are only available in the release version.
{.is-warning}
