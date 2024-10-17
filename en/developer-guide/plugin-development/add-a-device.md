---
title: Add a Device
description: 
published: true
date: 2024-10-17T04:34:33.003Z
tags: developer
editor: markdown
dateCreated: 2024-10-17T04:34:33.003Z
---

# Adding a Device

Next, we will demonstrate how to write a device resource by creating a fictional motherboard derived from Arduino UNO called Hoho.

1. Create Device Folder

First, create a new folder under the `./devices` directory named after the motherboard, following camel case: `hoho`.

```bash
mkdir ./devices/hoho
cd ./devices/hoho
```

2. Create `index.js` File

The `index.js` file is used to describe various attributes of the device. Create this file and write the following content.

```js
const hoho = formatMessage => ({
    name: formatMessage({
        id: 'hoho.name',
        default: 'Hoho',
        description: 'Name for the hoho device'
    }),
    deviceId: 'hoho_arduinoUno',
    manufactor: 'Hoho inc.',
    learnMore: 'www.openblock.cc',
    iconURL: 'assets/hoho.png',
    description: formatMessage({
        id: 'hoho.description',
        default: 'This is a device demo.',
        description: 'Description for the hoho device'
    }),
    disabled: false,
    bluetoothRequired: false,
    serialportRequired: true,
    defaultBaudRate: '9600',
    pnpidList: [
        'USB\\VID_10C4&PID_EA60', // CP2102
        'USB\\VID_1A86&PID_7523' // CH340
    ],
    internetConnectionRequired: false,
    launchPeripheralConnectionFlow: true,
    useAutoScan: false,
    connectionIconURL: 'assets/hoho-illustration.svg',
    connectionSmallIconURL: 'assets/hoho-small.svg',
    programMode: ['realtime', 'upload'],
    programLanguage: ['block', 'cpp'],
    tags: ['kit'],
    deviceExtensionsCompatible: 'arduinoUno',
    helpLink: 'wiki.openblock.cc'
});

module.exports = hoho;
```

The `deviceId: 'hoho_arduinoUno'` attribute indicates that it is a device inheriting from arduinoUno, which has all the block content and functions of Arduino UNO, with only some attributes modified.

3. Add Device Images

According to the definitions in the `index.js` file, create an `assets` folder and download the three images below into it.

- [hoho.svg](/developer-guide/plugin-development/add-a-device/hoho.png)

![hoho.png](/developer-guide/plugin-development/add-a-device/hoho.png)

- [hoho-illustration.svg](/developer-guide/plugin-development/add-a-device/hoho-illustration.svg)

![hoho-illustration.png](/developer-guide/plugin-development/add-a-device/hoho-illustration.svg)

- [hoho-small.svg](/developer-guide/plugin-development/add-a-device/hoho-small.svg)

![hoho-small.png](/developer-guide/plugin-development/add-a-device/hoho-small.svg)

4. Create `translations.js` File

This file is used to provide multilingual translation content. Create the `translations.js` file and write the following content.

```js
function getInterfaceTranslations () {
    return {
        "en": {
            "hoho.name": "Hoho",
            "hoho.description": "This is a device demo."
        },
        "ru": {
            "hoho.name": "Hoho",
            "hoho.description": "Это демо-версия устройства."
        },
        "zh-cn": {
            "hoho.name": "Hoho",
            "hoho.description": "这是一个设备演示。"
        },
        "zh-tw": {
            "hoho.name": "Hoho",
            "hoho.description": "這是一個設備演示。"
        }
    };
}

if (typeof module !== 'undefined') {
    module.exports = {getInterfaceTranslations};
}
```

5. Finally, restart OpenBlock, and we will be able to see and select this newly added device in the device selection interface.

![demodevoceselection.png](/developer-guide/plugin-development/add-a-device/demodevoceselection.png)
![demodeviceconnected.png](/developer-guide/plugin-development/add-a-device/demodeviceconnected.png)

## Attachment

[1] [hoho Device Resource Package.zip](/developer-guide/plugin-development/add-a-device/hoho.zip)
