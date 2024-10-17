---
title: Raspberry Pi Pico
description: 
published: true
date: 2024-10-17T03:58:18.007Z
tags: boards
editor: markdown
dateCreated: 2024-10-17T03:58:18.007Z
---

# Raspberry Pi Pico

## Introduction

### Pin Diagram

![pico.png](/general-hardware-guidelines/boards/raspberry-pi-pico/pico.png)

## Arduino Programming Guide

### First Use

When using the Arduino programming framework for the first time, you need to manually flash the Arduino Bootloader firmware. Follow these steps:

1. Download the `sketch.ino.uf2` file:

	- [sketch.ino.uf2](/general-hardware-guidelines/boards/raspberry-pi-pico/sketch.ino.uf2)
  
2. Press and hold the BOOTSEL button, then insert the Pico into the USB port of your computer. Release the BOOTSEL button after connecting the Pico.
3. It will be recognized as a mass storage device named RPI-RP2.
4. Drag and drop the `.uf2` file into RPI-RP2, and your Pico will automatically restart.
5. You can now use OpenBlock to connect to the board and start programming.

> Note: In the current version, OpenBlock cannot automatically switch the firmware of the Raspberry Pi Pico. You need to manually download the corresponding firmware each time you switch programming frameworks.
{.is-warning}

## MicroPython Programming Guide (Distro Version Only)

### First Use

When using the MicroPython programming framework for the first time, you need to manually flash the MicroPython firmware. Follow these steps:

1. Download the `RPI_PICO-20240602-v1.23.0.uf2` file:

	- [RPI_PICO-20240602-v1.23.0.uf2](/general-hardware-guidelines/boards/raspberry-pi-pico/RPI_PICO-20240602-v1.23.0.uf2)
  
2. Press and hold the BOOTSEL button, then insert the Pico into the USB port of your computer. Release the BOOTSEL button after connecting the Pico.
3. It will be recognized as a mass storage device named RPI-RP2.
4. Drag and drop the `.uf2` file into RPI-RP2, and your Pico will automatically restart.
5. You can now use OpenBlock to connect to the board and start programming.

> Note: In the current version, OpenBlock cannot automatically switch the firmware of the Raspberry Pi Pico. You need to manually download the corresponding firmware each time you switch programming frameworks.
{.is-warning}