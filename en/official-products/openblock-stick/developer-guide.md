---
title: OpenBlock Stick Developer Guide
description: 
published: true
date: 2024-10-17T03:52:09.480Z
tags: developer
editor: markdown
dateCreated: 2024-10-17T03:52:09.480Z
---

# OpenBlock Programming Stick Developer Guide

## Introduction

The OpenBlock Programming Stick is equipped with the OpenBlock Distro version, which implements the external resource plugin system in the same way as the desktop version. Developers can freely modify the plugin content by accessing the filebrowser page of the programming stick, enabling customized development of the programming stick software content.

> The following operations are based on the condition that the development machine and the programming stick are on the same local area network. Therefore, please first complete the network configuration for the programming stick as instructed in the user guide.
{.is-info}

## Accessing the Filebrowser Page

Enter the address `{ip}/filebrowser` in your browser to open the filebrowser page.

### Developer Directory File Descriptions

- **log**  
  This folder stores the working logs of the software in the programming stick, used to track and troubleshoot software runtime errors.

- **.cache**  
  Equivalent to the cache directory of OpenBlockDesktop, this folder is used to store generated code and builds, and it also serves as the cache directory for external plugins.

- **firmwares**  
  Contains the firmware used, similar to the files in OpenBlockDesktop.

- **external-resources**  
  Contains external plugins and device-related extension content, similar to the files in OpenBlockDesktop.

## Custom Development

In the above content, we have discussed how to access and read files in the developer account, as well as the functions of each file. Next, we will outline the specific development steps.

### Debugging Plugins on the Desktop Version

The OpenBlock version installed on the programming stick is fully compatible with the external resource files on the computer version. Due to the limited hardware resources of the programming stick, we recommend that developers first use the conventional OpenBlock customization development method on the computer by modifying the external-resources file.

### Replacing the External-Resources in the Developer Directory

After modifying the external-resources, simply replace the `external-resources` in the programming stick's developer directory to enable the programming stick to use the customized external-resources you have developed.

### Restart the Programming Stick and Test

**After uploading, wait for a moment (about 10 seconds, to ensure data is written to the SD card from memory)**, and then restart the programming stick to see the modifications. As long as our plugins run smoothly on the desktop version, there should be no issues following the above method to replace the external-resources on the programming stick.