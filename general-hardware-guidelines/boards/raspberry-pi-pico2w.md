---
title: Raspberry Pi Pico 2 W
description: 树莓派 Pico 2 W 使用指南
published: true
date: 2025-05-05T15:42:33.247Z
tags: 控制板
editor: markdown
dateCreated: 2025-05-05T15:42:33.247Z
---

# Raspberry Pi Pico 2 W

## 介绍

### 引脚图

![pico2w-pinout.svg](/general-hardware-guidelines/boards/raspberry-pi-pico2w/pico2w-pinout.svg)

## Arduino 编程指南

### 首次使用

在首次使用 Arduino 编程框架时需要预先手动烧录 Arduino Bootloader 固件，步骤如下：

1. 下载 pico2w.ino.uf2 文件：

	- [pico2w.ino.uf2](/general-hardware-guidelines/boards/raspberry-pi-pico2w/pico2w.ino.uf2)
  
2. 按住 BOOTSEL 按钮并将 Pico 插入计算机的 USB 端口，连接 Pico 后松开 BOOTSEL 按钮。
3. 它将识别为名称是 RP2350 的大容量存储设备。
4. 将 .uf2 文件拖放到 RP2350 中，而后您的 Pico 将自动重新启动。
5. 现在就可以使用 OpenBlock 连接主板开始编程了。

> 注意目前版本下 OpenBlock 还无法自动切换 Raspberry Pi Pico 2 W 的固件，在每次切换编程框架后都需要手动下载一次对应的固件。
{.is-warning}


## MicroPython 编程指南（仅适用于Distro版本）

### 首次使用

在首次使用 MicroPython 编程框架时需要预先手动烧录 MicroPython 固件，步骤如下：

1. 从下方链接中下载 MicroPython 固件：

	- [https://micropython.org/download/RPI_PICO2_W/](https://micropython.org/download/RPI_PICO2_W/)
  
2. 按住 BOOTSEL 按钮并将 Pico 插入计算机的 USB 端口，连接 Pico 后松开 BOOTSEL 按钮。
3. 它将识别为名称是 RP2350 的大容量存储设备。
4. 将 .uf2 文件拖放到 RP2350 中，而后您的 Pico 将自动重新启动。
5. 现在就可以使用 OpenBlock 连接主板开始编程了。

> 注意目前版本下 OpenBlock 还无法自动切换 Raspberry Pi Pico 2 W的固件，在每次切换编程框架后都需要手动下载一次对应的固件。
{.is-warning}