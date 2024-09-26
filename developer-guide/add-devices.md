---
title: 添加设备
description: 学习如何在OpenBlock中开发并添加一个新的控制板
published: false
date: 2024-07-18T15:59:24.637Z
tags: 
editor: markdown
dateCreated: 2022-08-13T07:45:39.632Z
---

# 添加控制板
OB支持在设备列表中添加第三方控制板，添加控制板时，需要选择对应的基础板类型。目前，OB支持的基础板类型有：
- arduinoUno
- arduinoNano
- arduinoLeonardo
- arduinoMega2560
- esp32
- esp8266
- esp8266NodeMCU
- microbit
- microbitV2
- k210MaixDock
- k210Maixduino
- makeyMakey
<br/>

## 准备工作
编辑器：推荐使用Visual Studio Code
控制板的设备id
控制板图片：控制板图片需要三种类型，分别为：
- `<board name>.png`: 大小要求为600x372，模块图片位于整张图片的中心位置，具体大小如下图：
![底板.png](/底板.png)
- `<board name>-illustration.svg`: 108x87，svg格式，可通过png文件转，可使用在线格式转换的网站：aconvert.com
- `<board name>-small.svg`: 40x40，svg格式
> 注意，使用png转svg文件时，要去掉png文件的背景。
{.is-info}

<br/>

## 添加控制板
添加控制板信息时，主要修改external-resources中devices文件夹中的内容。
首先，在devices文件夹中的device.js文件中，添加控制板的名称ID。device.js文件的内容如下所示：
```js
module.exports = [
    // Buid-in device
    'arduinoUno',
    'arduinoNano',
    'arduinoLeonardo',
    'arduinoMega2560',
    'esp32',
    'arduinoEsp32',
    'microPythonEsp32',
    'esp8266NodeMCU',
    'arduinoEsp8266NodeMCU',
    'microPythonEsp8266NodeMCU',
    'microbit',
    'microbitV2',
    'k210MaixDock',
    'arduinoK210MaixDock',
    'microPythonK210MaixDock',
    'k210Maixduino',
    'arduinoK210Maixduino',
    'microPythonK210Maixduino',
    'makeyMakey',
    // Third party
    'thirdParty_esp32',
    'thirdParty_arduinoEsp32',
    'thirdParty_microPythonEsp32'
];
```
device.js文件中控制板的顺序，就是OB设备列表中设备的顺序。
添加控制板名称时，控制板名称的格式为`板子名称_基础板名称`。如，一块基于arduinoUno的板子，应命名为`demoBoard_arduinoUno`；一块基于esp8266的板子，需要它可选arduino类型或microPython类型，则需要在device.js文件文件中添加三个名称，分别为`demoBoard_esp8266`、`demoBoard_arduinoEsp8266`、`demoBoard_microPythonEsp8266`。添加控制板名称时请参照现有格式。
<br/>

接下来，添加控制板的详细信息。需要在devices目录中建立一个文件夹，层级目录如下所示：
```
external-resources
|- devices（控制板目录）
| 	|- thirdParty（制造商目录）
|       |- deviceDemo（板子目录）
|       		|- asset（图片文件夹，存放所需的三张图片）
|       				|- deviceDemo.png
|       				|- deviceDemo-illustration.svg
|       				|- deviceDemo-small.svg
|       	  |- index（控制板详细信息）.js
| 	|- device.js
```
> 目录等级中，一定要将板子文件及放在制造商文件夹中，即一定要有两层文件夹：`制造商目录/板子目录`。
{.is-warning}

建立好文件夹之后，将准备好的三张图片放在asset文件夹中，接下来，编辑index.js文件。
<br/>

index.js文件的基础格式为：
```js
const demoBoard = formatMessage => ({
    name: 'demoBoard',
    deviceId: 'demoBoard_arduinoUno',
    manufactor: 'producers', // 制作商
    learnMore: 'wiki.openblock.cc', // 学习控制板相关信息的网页
    iconURL: 'asset/demoBoard.png', // 在设备列表中显示的图片
    description: formatMessage({   // 在设备列表中显示的关于控制板的描述信息
        id: 'demoBoard.description',
        default: 'demoBoard.',
        description: 'Description for the demoBoard device'
    }),
    disabled: false, // 板子是否不可用，true为板子不可用
    bluetoothRequired: false, // 是否要求蓝牙
    serialportRequired: true, // 是否串口链接
    defaultBaudRate: '9600', // 默认通讯波特率
    pnpidList: [  // 板子的设备pnpid
        'USB\\VID_10C4&PID_EA60', // CP2102
        'USB\\VID_1A86&PID_7523' // CH340
    ],
    internetConnectionRequired: false,
    launchPeripheralConnectionFlow: true,
    useAutoScan: false,
    connectionIconURL: 'asset/demoBoard-illustration.svg', // 设备连接界面的图片
    connectionSmallIconURL: 'asset/demoBoard-small.svg', // 代码上传界面以及设备连接成功后显示的图片
    programMode: ['realtime', 'upload'], // 设备支持的编程模式，realtime（实时模式）、upload（上传模式）
    programLanguage: ['block', 'cpp'], // 设备支持的编程语言，可选项有：'block'、'cpp'、'microPython'
    tags: ['kit'], 
    deviceExtensions: ['demoBoard'], // 上传模式默认加载的插件ID列表。
    deviceExtensionsCompatible: 'arduinoUno', // 兼容的控制板类型，如：兼容arduinoUno，则支持arduinoUno的插件同样支持当前控制板
    helpLink: ' ' // 帮助链接
});

module.exports = demoBoard;

```
接下来，再到`third-party-locales.json`（位于external-resources根目录中）中添加板子相关的翻译信息。
third-party-locales.json的内容格式为：
```json
{
    "en": { // 英文
        "demoBoard.description": "An example showing how to add a third-party board."
    },
    "zh-cn": { // 简体中文
        "demoBoard.description": "演示如何添加第三方控制板的示例。"
    },
    "zh-zw": { // 繁体中文
        "demoBoard.description": "演示如何添加第三方控制板的示例。"
    }
}

```
至此，控制板的添加就完成了。
> 需要注意的时，为了不让OB将添加的内容删掉，记得删除config.json中的参数sha256，具体操作参考[addModules](/zh/addModules)中文件结构中的内容
{.is-warning}

<br/>

上述为添加只支持一种编程语言的控制板时的方式，若添加的控制板即支持arduino也支持microPython，则index.js文件的内容有所不同。添加的控制板即支持arduino也支持microPython时，index.js文件的内容如下所示：
```js
const deviceDemo = formatMessage => ({
    name: formatMessage({
        id: 'deviceDemo.name',
        default: 'Third Party Device Demo'
    }),
    deviceId: 'deviceDemo_esp32',
    manufactor: 'OpenBlock',
    learnMore: '', // A link you can learn more about the device
    typeList: ['arduino', 'microPython'],
    iconURL: 'asset/deviceDemo.png',
    description: formatMessage({
        id: 'deviceDemo.description',
        default: 'An example showing how to add a third-party board.'
    }),
    pnpidList: [
        'USB\\VID_10C4&PID_EA60', // CP2102
        'USB\\VID_1A86&PID_7523' // CH340
    ],
    connectionIconURL: 'asset/deviceDemo-illustration.svg',
    connectionSmallIconURL: 'asset/deviceDemo-small.svg',
    programMode: ['realtime', 'upload'],
    defaultProgramMode: 'upload',
    programLanguage: ['block', 'c', 'cpp', 'microPython'],
    tags: ['kit'],
    helpLink: ''
});

const deviceDemoArduino = formatMessage => {
    const device = deviceDemo(formatMessage);
    device.defaultBaudRate = '9600';
    device.deviceId = 'deviceDemo_arduinoEsp32';
    device.programMode = ['realtime', 'upload'];
    device.deviceExtensions = ['arduinoDeviceDemo'],
    device.deviceExtensionsCompatible = 'arduinoEsp32',
    device.hide = true;
    return device;
};

const deviceDemoMicroPython = formatMessage => {
    const device = deviceDemo(formatMessage);
    device.defaultBaudRate = '115200';
    device.deviceId = 'deviceDemo_microPythonEsp32';
    device.programMode = ['upload'];
    device.deviceExtensions = [], // 上传模式不加载默认插件
    device.deviceExtensionsCompatible = 'microPythonEsp32',
    device.hide = true;
    return device;
};

module.exports = formatMessage => ([
    deviceDemo(formatMessage),
    deviceDemoArduino(formatMessage),
    deviceDemoMicroPython(formatMessage)
]);

```
> 注意，在板子的具体类型的信息描述中，需要添加属性`device.hide = true`
{.is-warning}




