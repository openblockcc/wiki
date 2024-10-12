---
title: Raspberry Pi Pico
description: 树莓派 Pico 使用指南
published: true
date: 2024-10-12T04:06:16.409Z
tags: 主板
editor: markdown
dateCreated: 2022-10-06T11:52:32.452Z
---

# Raspberry Pi Pico

## 介绍

### 引脚图

![pico.png](/general-hardware-guidelines/boards/raspberry-pi-pico/pico.png)

## Arduino 编程指南

### 首次使用

在首次使用 Arduino 编程框架时需要预先手动烧录 Arduino Bootloader 固件，步骤如下：

1. 下载 sketch.ino.uf2 文件：

	- [sketch.ino.uf2](/general-hardware-guidelines/boards/raspberry-pi-pico/sketch.ino.uf2)
  
2. 按住 BOOTSEL 按钮并将 Pico 插入计算机的 USB 端口，连接 Pico 后松开 BOOTSEL 按钮。
3. 它将识别为名称是 RPI-RP2 的大容量存储设备。
4. 将 .uf2 文件拖放到 RPI-RP2 中，而后您的 Pico 将自动重新启动。
5. 现在就可以使用 OpenBlock 连接主板开始编程了。

> 注意目前版本下 OpenBlock 还无法自动切换 Raspberry Pi Pico 的固件，在每次切换编程框架后都需要手动下载一次对应的固件。
{.is-warning}


## MicroPython 编程指南（仅适用于Distro版本）

### 首次使用

在首次使用 MicroPython 编程框架时需要预先手动烧录 MicroPython 固件，步骤如下：

1. 下载 sketch.ino.uf2 文件：

	- [RPI_PICO-20240602-v1.23.0.uf2](/general-hardware-guidelines/boards/raspberry-pi-pico/RPI_PICO-20240602-v1.23.0.uf2)
  
2. 按住 BOOTSEL 按钮并将 Pico 插入计算机的 USB 端口，连接 Pico 后松开 BOOTSEL 按钮。
3. 它将识别为名称是 RPI-RP2 的大容量存储设备。
4. 将 .uf2 文件拖放到 RPI-RP2 中，而后您的 Pico 将自动重新启动。
5. 现在就可以使用 OpenBlock 连接主板开始编程了。

> 注意目前版本下 OpenBlock 还无法自动切换 Raspberry Pi Pico 的固件，在每次切换编程框架后都需要手动下载一次对应的固件。
{.is-warning}