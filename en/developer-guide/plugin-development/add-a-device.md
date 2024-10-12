---
title: 添加一个设备
description: 
published: true
date: 2024-10-12T04:28:36.569Z
tags: 开发者
editor: markdown
dateCreated: 2024-07-17T11:05:31.263Z
---

# 添加一个设备

接下来我们会以创建一个虚构的衍生自 Arduino UNO 的主板 Hoho 的资源为例，演示如何编写添加设备资源。

1. 创建设备文件夹

首先在 `./devices` 文件夹下创建一个新的文件夹以主板名称命名并遵循驼峰规则：`hoho`

```bash
mkdir ./devices/hoho
cd ./devices/hoho
```

2. 创建 `index.js` 文件

`index.js` 是用来描述设备各个属性的文件，创建这个文件，并写入以下内容。

```js
const hoho = formatMessage => ({
    name:  formatMessage({
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

其中 `deviceId: 'hoho_arduinoUno'` 属性表明了它是一个继承自 arduinoUno 的设备，它拥有 Arduino UNO 全部的积木内容及功能，只是修改了其部分属性。

3. 添加设备图片

按照 `index.js` 文件中的定义，创建 `assets` 文件夹并下载放入下方的3张图片。

- [hoho.svg](/developer-guide/plugin-development/add-a-device/hoho.png)

![hoho.png](/developer-guide/plugin-development/add-a-device/hoho.png)

- [hoho-illustration.svg](/developer-guide/plugin-development/add-a-device/hoho-illustration.svg)

![hoho.png](/developer-guide/plugin-development/add-a-device/hoho-illustration.svg)

- [hoho-small.svg](/developer-guide/plugin-development/add-a-device/hoho-small.svg)

![hoho.png](/developer-guide/plugin-development/add-a-device/hoho-small.svg)

4. 创建 `translations.js` 文件

此文件用于提供多语言翻译内容，创建 `translations.js` 文件，并将以下内容写入。

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

5. 最后重启 OpenBlock，我们就可以在设备选择界面中看到并选择这个新添加的设备了。

![demodevoceselection.png](/developer-guide/plugin-development/add-a-device/demodevoceselection.png)
![demodeviceconnected.png](/developer-guide/plugin-development/add-a-device/demodeviceconnected.png)

## 附件

[1] [hoho 设备资源包.zip](/developer-guide/plugin-development/add-a-device/hoho.zip)