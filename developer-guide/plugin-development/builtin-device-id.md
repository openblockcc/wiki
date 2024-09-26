---
title: 内置设备 ID
description: 
published: true
date: 2024-07-18T10:00:15.430Z
tags: 
editor: markdown
dateCreated: 2024-07-18T09:50:19.389Z
---

# 内置设备 ID

OpenBlock 的外部资源包可以定义由内置设备衍生的设备，以此来添加第三方控制板或是产品套装。目前 OpenBlock 内置的设备 ID 如下。

| 设备 ID                   | 设备                     | 编程框架 | 备注 |
| -------------------------- | ----------------------- | ------- | ---- |
| arduinoUno                 | Arduino UNO R3          | Arduino C/C++ |      |
| arduinoNano                | Arduino Nano            | Arduino C/C++ | 使用 oldbootloader 烧写，且包含 A6, A7 引脚 |
| arduinoUnoUltra            | Arduino UNO R3 Variant1 | Arduino C/C++ | 为第三方扩展使用的包含了包含 A6, A7 引脚的 Arduino UNO R3 |
| arduinoUnoSE               | Arduino UNO R3 Variant2 | Arduino C/C++ | 为第三方扩展使用的不包含任何硬件基础积木的 Arduino UNO R3 |
| arduinoLeonardo            | Arduino Leonardo        | Arduino C/C++ |      |
| makeyMakey                 | MakeyMakey              | Arduino C/C++ |      |
| arduinoMega2560            | Arduino Mega 2560       | Arduino C/C++ |      |
| arduinoEsp32               | Esp32                   | Arduino C/C++ |      |
| arduinoEsp8266             | Esp8266                 | Arduino C/C++ |      |
| microPythonEsp8266         | Esp8266                 | Standard MicroPython |      |
| arduinoEsp8266NodeMCU      | Esp8266 Node MCU        | Arduino C/C++ |      |
| microPythonEsp8266NodeMCU  | Esp8266 Node MCU        | Standard MicroPython |      |
| arduinoK210                | K210                    | Arduino C/C++ |      |
| microPythonK210            | K210                    | Standard MicroPython |      |
| arduinoK210MaixDock        | MaixDock                | Arduino C/C++ |      |
| microPythonK210MaixDock    | MaixDock                | Standard MicroPython |      |
| arduinoK210Maixduino       | Maixduino               | Arduino C/C++ |      |
| microPythonK210Maixduino   | Maixduino               | Standard MicroPython |      |
| arduinoRaspberryPiPico     | Raspberry Pi Pico       | Arduino C/C++ |      |
| microPythonRaspberryPiPico | Raspberry Pi Pico       | Microbit MicroPython |      |
| microbit                   | Micro:bit               | Standard MicroPython |      |
| microbitV2                 | micro:bit V2            | Microbit MicroPython |      |

> 注意编程框架为 `Standard MicroPython` 的设备仅在发行版中可用。
{.is-warning}


