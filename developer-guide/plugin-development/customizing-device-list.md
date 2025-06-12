---
title: 定制设备列表
description: 
published: true
date: 2025-06-12T16:27:18.031Z
tags: 开发者
editor: markdown
dateCreated: 2025-06-12T16:27:18.031Z
---

# 定制设备列表

有时我们可能希望在设备选择界面中只显示我们希望显示的设备内容。OpenBlock 插件框架允许我们通过自定义一个设备列表来控制设备选择界面中的内容。

1. 首先在资源包的 `devices` 路径下创建文件 `device.js`。（如果你的资源包路径下没有 `devices` 这个文件夹那么先创建它即可。）

``` bash
cd ./devices
touch device.js
```

2. 在文件内我们通过定义一个设备数组来定制我们想要显示的控制板。当 `device.js` 文件存在时 OpenBlock 资源系统会根据这个文件中的定义显示设备列表。

`device.js` 中写入的内容样例如下：
```js
module.exports = [
    // Buid-in device
    'arduinoUno',
    'arduinoNano',
    'arduinoLeonardo',
    'arduinoMega2560',
    ['esp32', 'arduinoEsp32', 'microPythonEsp32'],
    ['esp8266NodeMCU', 'arduinoEsp8266NodeMCU', 'microPythonEsp8266NodeMCU'],
    'microbit',
    'microbitV2',
    'makeyMakey',
    ['k210MaixDock', 'arduinoK210MaixDock', 'microPythonK210MaixDock'],
    ['k210Maixduino', 'arduinoK210Maixduino', 'microPythonK210Maixduino'],
    ['raspberryPiPico', 'arduinoRaspberryPiPico', 'microPythonRaspberryPiPico'],
    // Third party
    'deviceDemo_esp32',
    'deviceDemo_arduinoEsp32',
    'deviceDemo_microPythonEsp32',
    'deviceDemo2',
    'arduinoDeviceDemo2',
    'microPythonDeviceDemo2'
];
```

通过设置 `deviceId` 的方式来控制我们希望现实的设备内容。OpenBlock资源系统会根据这个文件中的定义来提供