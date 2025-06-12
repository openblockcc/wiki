---
title: 定制设备列表
description: 
published: true
date: 2025-06-12T16:57:23.355Z
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

2. 在文件内我们通过定义一个设备数组来定制我们想要显示的控制板。

`device.js` 中的内容样例如下：
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
    'deviceDemo_arduinoUno',
    ['deviceDemo2_esp32', 'deviceDemo2_arduinoEsp32', 'deviceDemo2_microPythonEsp32']
  	// ...
];
```
> 注意这个文件中定义的 Third party 中的 `deviceId` 均为举例时虚构的设备，使用时要将其替换为真实存在的 `deviceId`。
{.is-warning}

当 `device.js` 文件存在时 OpenBlock 会根据这个文件中的定义显示设备列表。我们可以通过设置 `deviceId` 的方式来控制显示的设备。除了软件内部定义的设备外，也可以使用我们在资源包中自己添加的设备，直接在列表中添加对应的设备的 `deviceId` 即可。

列表中以数组形式定义的 `deviceId` 是多编程架构设备（如：ESP32、K210等）的特殊写法，因为对于多编程架构的设备来说我们实质上需要定义一个父类和多个子类来实现它。使用数组包裹他们只是为了方便阅读与管理，其功能与直接展开书写的结构并无任何区别。

当然多编程架构的特性仅在发行版本中生效，在社区版中不支持的设备类型会被忽略，只会显示其支持的编程架构设备。比如在社区版中 `['k210MaixDock', 'arduinoK210MaixDock', 'microPythonK210MaixDock']` 这个设备列表，只会显示 `arduinoK210MaixDock` 这个设备。

## 附件

[1] [device.js 文件样例](/developer-guide/plugin-development/customizing-device-list/device.js)