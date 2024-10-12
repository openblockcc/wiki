---
title: 常见的 USB 硬件 ID
description: 
published: true
date: 2024-10-12T04:31:01.061Z
tags: 
editor: markdown
dateCreated: 2024-07-18T08:51:11.224Z
---

# 常见的 USB 硬件 ID

OpenBlock 会根据设备的 `pnpidList` 属性来过滤 USB 设备，以防止无关设备选项的干扰。以下是一些常见芯片的 USB 硬件 ID。

| 芯片/控制板       | 硬件ID                   |
| ----------------- | ----------------------- |
| CH340             |  USB\\\\VID_1A86&PID_7523 |
| CH9102            |  USB\\\\VID_1A86&PID_55D4 |
| PL2303            |  USB\\\\VID_067B&PID_2303 |
| FTDI              |  USB\\\\VID_0403&PID_6001 |
| FTDI              |  USB\\\\VID_0403&PID_6010 |
| CP2102            |  USB\\\\VID_10C4&PID_EA60 |
| Arduino UNO       |  USB\\\\VID_2341&PID_0043 |
| Arduino UNO       |  USB\\\\VID_2341&PID_0001 |
| Arduino UNO       |  USB\\\\VID_2A03&PID_0043 |
| Arduino UNO       |  USB\\\\VID_2341&PID_0243 |
| Arduino Maga 2560 |  USB\\\\VID_2341&PID_0010 |
| Arduino Maga 2560 |  USB\\\\VID_2341&PID_0042 |
| Arduino Maga 2560 |  USB\\\\VID_2A03&PID_0010 |
| Arduino Maga 2560 |  USB\\\\VID_2A03&PID_0042 |
| Arduino Maga 2560 |  USB\\\\VID_2341&PID_0210 |
| Arduino Maga 2560 |  USB\\\\VID_2341&PID_0242 |
| Arduino Leonardo  |  USB\\\\VID_2341&PID_0036 |
| Arduino Leonardo  |  USB\\\\VID_2341&PID_8036 |
| Arduino Leonardo  |  USB\\\\VID_2A03&PID_0036 |
| Arduino Leonardo  |  USB\\\\VID_2A03&PID_8036 |
| Microbit          |  USB\\\\VID_0D28&PID_0204 |
| Raspberry Pi Pico |  USB\\\\VID_2E8A&PID_000A |
| Raspberry Pi Pico |  USB\\\\VID_2E8A&PID_0005 |
| Makey Makey       |  USB\\\\VID_1B4F&PID_2B74 |
| Makey Makey       |  USB\\\\VID_1B4F&PID_2B75 |
