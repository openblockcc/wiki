---
title: Raspberry Pi Pico W
description: Raspberry Pi Pico W User Guide
published: true
date: 2025-05-05T15:17:37.876Z
tags: boards
editor: markdown
dateCreated: 2025-05-05T15:17:37.876Z
---

# Raspberry Pi Pico W

## Introduction

### Pin Diagram

![picow-pinout.svg](/general-hardware-guidelines/boards/raspberry-pi-picow/picow-pinout.svg)

## Arduino Programming Guide

### First Use

When using the Arduino programming framework for the first time, you need to manually flash the Arduino Bootloader firmware. Follow these steps:

1. Download the `picow.ino.uf2` file:

	- [picow.ino.uf2](/general-hardware-guidelines/boards/raspberry-pi-picow/picow.ino.uf2)
  
2. Press and hold the BOOTSEL button, then insert the Pico into the USB port of your computer. Release the BOOTSEL button after connecting the Pico.
3. It will be recognized as a mass storage device named RPI-RP2.
4. Drag and drop the `.uf2` file into RPI-RP2, and your Pico will automatically restart.
5. You can now use OpenBlock to connect to the board and start programming.

> Note: In the current version, OpenBlock cannot automatically switch the firmware of the Raspberry Pi Pico W. You need to manually download the corresponding firmware each time you switch programming frameworks.
{.is-warning}

## MicroPython Programming Guide (Distro Version Only)

### First Use

When using the MicroPython programming framework for the first time, you need to manually flash the MicroPython firmware. Follow these steps:

1. Download the MicroPython firmware from the link below:

	- [https://micropython.org/download/RPI_PICO_W/](https://micropython.org/download/RPI_PICO_W/)
  
2. Press and hold the BOOTSEL button, then insert the Pico into the USB port of your computer. Release the BOOTSEL button after connecting the Pico.
3. It will be recognized as a mass storage device named RPI-RP2.
4. Drag and drop the `.uf2` file into RPI-RP2, and your Pico will automatically restart.
5. You can now use OpenBlock to connect to the board and start programming.

> Note: In the current version, OpenBlock cannot automatically switch the firmware of the Raspberry Pi Pico W. You need to manually download the corresponding firmware each time you switch programming frameworks.
{.is-warning}