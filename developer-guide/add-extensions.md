---
title: 添加扩展
description: 学习如何在OpenBlock中开发并添加一个新的模块插件
published: false
date: 2024-10-12T04:27:56.058Z
tags: 
editor: markdown
dateCreated: 2022-07-21T07:02:25.615Z
---

# 添加扩展
	
以下将讲解如何为控制板添加支持的扩展模块插件，支持arduino、microbit以及microPython三种类型。添加的模块插件支持在OB的上传模式中使用。
<br/>

## 准备工作
编辑器：推荐使用Visual Studio Code
模块图片：模块图片大小要求为600*372，模块图片位于整张图片的中心位置，具体大小如下图：
![底板.png](/底板.png)
<br/>

## 文件结构
添加扩展插件需要在external-resources文件夹中添加，安装OB桌面版后，有两个位置有external-resources文件夹，分别为OB软件安装目录中，以及缓存目录中（缓存目录位于C:\Users\Adiministrator\AppData\Roaming\OpenBlockDesktop，其中Adiministrator是当前电脑系统用户的用户名）。
缓存目录中的external-resources是软件拷贝安装目录中的external-resources得来的。软件在启动时，会判断缓存目录中external-resources文件夹的sha256是否与config.json文件中的相同，若不同则会重新从安装目录中拷贝。而我们在添加扩展插件时，需要修改缓存目录中的内容以进行测试，为了不让修改的内容被软件删掉，我们需要进行的一个步骤是：删掉缓存目录中external-resources中config.json文件中的“sha256”所在的那一行，是的，直接删掉整行即可。
在开始之前，先认识下external-resources中的文件结构。以chineseTTS模块的文件结构举例如下：
```
external-resources
|- official-locales.json（插件信息翻译文件）
|- devices（控制板目录）
|- extensions（模块插件目录）
| 	|- arduino（模块支持的编程语言）
|       |- actuator（插件类型——执行器）
|       		|- chineseTTS（插件文件夹）
|       				|- asset（图片文件夹）
|       				|- lib（库文件夹）
|       				|- blocks（积木详细设计）.js
|       				|- generator（积木实际功能实现）.js
|       				|- index（插件相关信息）.js
|       				|- msg（翻译文件）.js
|       				|- toolbox（定义在OB中显示的积木）.js
|       |- communication（插件类型——通讯）
|       |- display（插件类型——显示器）
|       |- sensor（插件类型——传感器）
|       |- shield（插件类型——扩展板）
|       |- other（插件类型——其它）
|       |- kit（插件类型——第三方控制板默认插件）
| 	|- microbit
| 	|- microPython
```
<br/>

## 添加插件信息
在index.js文件中添加插件相关信息，主要包括插件ID，插件支持的控制板信息等。
```js
const chineseTTS = formatMessage => ({
    name: formatMessage({
        id: 'chineseTTS.name',
        default: 'Chinese TTS'
    }), // 插件名称
    extensionId: 'chineseTTS', // 插件ID
    version: '1.0.0',
    supportDevice: ['arduinoUno', 'arduinoNano', 'arduinoLeonardo',
        'arduinoMega2560', 'arduinoEsp32', 'arduinoEsp8266'], // 插件支持的控制板
    author: 'ArthurZheng', // 作者
    iconURL: `asset/chineseTTS.png`, // 在插件列表中显示的图片
    description: formatMessage({
        id: 'chineseTTS.description',
        default: 'Text to speech module based on SYN6288, support Chinese and English letters and numbers.'
    }), // 对插件的描述，在插件列表中显示
    featured: true,
    blocks: 'blocks.js',
    generator: 'generator.js',
    toolbox: 'toolbox.js',
    msg: 'msg.js',
    library: 'lib',
    official: true,
    tags: ['actuator'],
    helpLink: 'https://wiki.openblock.cc' // 与插件相关的帮助链接
});

module.exports = chineseTTS;
```
index.js文件完成之后，重启软件，选择arduinoUno控制板，并进入上传模式，之后点击左下角的扩展，就可以在扩展列表中看到新增的插件了。
<br/>

## 积木blockly实现
从插件列表中选中插件之后，OB会从toolbox.js中获取要加载的积木的信息（分组以及积木名称），再到blocks.js和msg.js中获取积木的详细信息。不管是arduino还是microPython的插件，toolbox.js、blocks.js和msg.js这三个文件中的语法是相同，只是在generator.js。中实现积木的实际功能时有所不同，后续讲解generator.js时再详细说明。
综上，添加一个blockly积木时，需要修改的文件有toolbox.js、blocks.js、msg.js和generator.js。
以下讲解先以添加一个积木![openblock作品-1681550847769.png](/openblock作品-1681550847769.png =150x35)的过程为例，再分别讲解每个文件的语法特点。
<br/>

### 添加一个积木![openblock作品-1681550847769.png](/openblock作品-1681550847769.png =150x35)
首先，在toolbox.js中添加积木名称`EXAMPLE_setServoOutput`，即定义积木所在位置以及`input_value`型的参数要定义参数数据类型：
```js
function addToolbox () {
    return `
<category name="%{BKY_EXAMPLE_CATEGORY}" id="BKY_EXAMPLE_CATEGORY" colour="#4C97FF" secondaryColour="#4C97FF">
    <block type="EXAMPLE_setServoOutput" id="EXAMPLE_setServoOutput">
        <value name="VALUE">
            <shadow type="math_angle">
                <field name="NUM">90</field>
            </shadow>
        </value>
    </block>
</category>
`;
}

exports = addToolbox;
```
第二步，在blocks.js中添加积木结构、描述和参数内容的定义；
```js
function addBlocks (Blockly) {
    const color = '#4C97FF';

    const ports = [
        ['A', '3'],
        ['B', '5'],
        ['C', '6'],
        ['D', '9'],
        ['E', '10'],
        ['F', '11']];

  	// 名称EXAMPLE_setServoOutput名称与toolbox.js中名称对应
    Blockly.Blocks.EXAMPLE_setServoOutput = {
        init: function () {
            this.jsonInit({
                message0: Blockly.Msg.EXAMPLE_setServoOutput_msg, // 积木的描述信息，在msg.js中定义，对应EXAMPLE_setServoOutput_msg
                args0: [ // 定义参数信息
                    {
                        type: 'field_dropdown',
                        name: 'PIN',
                        options: ports
                    },
                    {
                        type: 'input_value',
                        name: 'VALUE'
                    }
                ],
                colour: color,
                extensions: ['shape_statement']
            });
        }
    };

    return Blockly;
}

exports = addBlocks;
```
第三步，在msg.js中添加积木的描述信息和任何需要在msg.js中定义的翻译：
```js
function addMsg (Blockly) {
    Object.assign(Blockly.ScratchMsgs.locales.en, {
    	EXAMPLE_CATEGORY: 'example',
    	EXAMPLE_setServoOutput_msg: 'set port %1 servo %2'
    });
    Object.assign(Blockly.ScratchMsgs.locales['zh-cn'], {
		EXAMPLE_CATEGORY: '举例',
    	EXAMPLE_setServoOutput_msg: '设置端口 %1 舵机为 %2'
    });
	Object.assign(Blockly.ScratchMsgs.locales["zh-tw"], {
		EXAMPLE_CATEGORY: '舉例',
		EXAMPLE_setServoOutput_msg: '設置端口 %1 舵機為 %2'
    });
    return Blockly;
}

exports = addMsg;
```
到了这里，我们的积木就已经添加到积木列表了，添加插件，可以看到如下图所示效果：
![wx20230415-180116@2x.png](/wx20230415-180116@2x.png =300x90)
最后，在generator.js中添加积木的功能实现：
```js
function addGenerator (Blockly) {
  
    // 名称EXAMPLE_setServoOutput名称与toolbox.js中名称对应
    Blockly.Arduino.EXAMPLE_setServoOutput  = function() {
        var pin = this.getFieldValue('PIN'); 
        var value = Blockly.Arduino.valueToCode(this, 'VALUE', Blockly.Arduino.ORDER_ATOMIC);
        Blockly.Arduino.definitions_['define_servo'] = '#include <Servo.h>';
        Blockly.Arduino.definitions_['define_servo_' + pin] = `Servo servo${pin};`;
        var code = `servo${pin}.attach(${pin}, 544, 2400);\n`;
        code += `servo${pin}.write(${value});\n`
        return code; 
    };

    return Blockly;
}

exports = addGenerator;
```
现在，可以在OB中调用这个积木啦。
![wx20230415-180919@2x.png](/wx20230415-180919@2x.png)
接下来，分别讲解每个文件的语法规则。
<br/>

### toolbox.js文件实现
首先，在toolbox中添加要显示的积木内容，在toolbox.js文件中，主要有一个function addToolbox，返回插件要显示的积木内容,toolbox.js文件的基本结构如下所示。
```js
function addToolbox () {
    return `
<category name="%{BKY_CHINESETTS_CATEGORY}" id="CHINESETTS_CATEGORY" colour="#5A5AAD" secondaryColour="#484891">
    <label text="%{BKY_CHINESETTS_LABEL}"></label>
    <block type="chineseTTS_init"></block>
</category>`;
}

exports = addToolbox;
```
其中，每个`category`是一个分组，`label`是分界标签，可以作为在代码组中二次分组时使用，而`block`就是每个具体的积木。以上代码中定义了分组`CHINESETTS_CATEGORY`，分组标签`BKY_CHINESETTS_LABEL`，和积木`chineseTTS_init`。
<br/>

### msg.js文件实现
接下来，去msg.js中实现分组、标签的具体名称，目前，OB支持三种语言，简体中文、繁体中文和英文，msg.js文件的基本结构如下所示。
```js
function addMsg (Blockly) {

    Object.assign(Blockly.ScratchMsgs.locales["en"], // 英文翻译
        {
            "CHINESETTS_CATEGORY": "Chinese TTS",
            "CHINESETTS_LABEL": "Chinese TTS",
            "CHINESETTS_INIT": "init chinese TTS module pin RX %1 TX %2"
        }
    );

    Object.assign(Blockly.ScratchMsgs.locales["zh-cn"], // 中文翻译
        {
            "CHINESETTS_CATEGORY": "中文 TTS",
            "CHINESETTS_LABEL": "中文 TTS",
            "CHINESETTS_INIT": "初始化中文TTS模块 端口 RX %1 TX %2"
        }
    );

    Object.assign(Blockly.ScratchMsgs.locales["zh-tw"], // 繁体翻译
        {
            "CHINESETTS_CATEGORY": "中文 TTS",
            "CHINESETTS_LABEL": "中文 TTS",
            "CHINESETTS_INIT": 初始化中文TTS模組 端口 RX %1 TX %2"
        }
    );

    return Blockly;
}

exports = addMsg;
```
其中`CHINESETTS_CATEGORY`是代码组的名称，`CHINESETTS_LABEL`是分界标签的内容，`CHINESETTS_INIT`是积木`chineseTTS_init`的详细内容，将在blocks.js中使用。需要注意的是，在toolbox.js中`<label>`的id是`BKY_CHINESETTS_LABEL`，但是实际上它在msg.js中对应的id需要使用`CHINESETTS_LABEL`。
在blocks.js中调用msg.js中的内容，可以通过`Blockly.Msg.id`的形式调用，如使用`CHINESETTS_INIT`的代码为：`Blockly.Msg.CHINESETTS_INIT`。
> 需要注意的是，添加翻译内容时，三种语言形式的内容都应该添加，否则在将OB的显示语言切换到没有对应内容的语言时，积木将不能正常显示。如，如果`CHINESETTS_INIT`没有添加繁体翻译，那么当OB切换到繁体显示时，所有添加的扩展插件的积木将不能正常显示。
{.is-warning}

<br/>


### blocks.js文件实现
接下来，blocks.js中实现积木的详细设计，blocks.js文件的基本结构如下所示。
```js
function addBlocks (Blockly) {
  	const colour = '#5A5AAD';
    const secondaryColour = '#484891';
  
  	const digitalPins = Blockly.getMainWorkspace().getFlyout()
        .getFlyoutItems()
        .find(block => block.type === 'arduino_pin_setDigitalOutput')
        .getField('PIN')
        .getOptions();
    
    Blockly.Blocks.chineseTTS_init = {
        init: function () {
            this.jsonInit({
                message0: Blockly.Msg.CHINESETTS_INIT,
                args0: [
                    {
                        type: 'field_dropdown',
                        name: 'RX',
                        options: digitalPins
                    },
                    {
                        type: 'field_dropdown',
                        name: 'TX',
                        options: digitalPins
                    }
                ],
                colour: colour,
                secondaryColour: secondaryColour,
                extensions: ['shape_statement']
            });
        }
    };

    return Blockly;
}

exports = addBlocks;
```
一般情况下，在jsonInit中实现积木的具体结构，主要的参数有message0（积木的显示内容）、args0（积木的参数）、clolur（积木的显示颜色）、secondaryColour（积木的底色）、extensions（积木的显示形状），除此之外，还可以有tooltip（积木的使用提示）。
<br/>

#### 积木类型
积木类型由`extensions`中的值决定，可选类型有以下几种：
- output_boolean：布尔型 ![openblock作品-1659506708862.png](/openblock作品-1659506708862.png =150x30)
- output_number：数值型 ![openblock作品-1659506722127.png](/openblock作品-1659506722127.png =150x30)
- output_string：字符串型，形状与数值型相同
- shape_statement：指令型 ![openblock作品-1659506732495.png](/openblock作品-1659506732495.png =180x35)
- shape_hat：起始型 ![openblock作品-1659506922023.png](/openblock作品-1659506922023.png =80x50)
- shape_end： 结尾型 ![openblock作品-1659507054878.png](/openblock作品-1659507054878.png =80x35)
<br/>

#### 可选参数类型
对于积木的显示内容，由message0和args0共同决定。如，积木![openblock作品-1659236881933.png](/openblock作品-1659236881933.png =250x40)的`message0: Blockly.Msg.CHINESETTS_INIT`，`CHINESETTS_INIT`在msg.js中的中文翻译为`"初始化中文TTS模块 端口 RX %1 TX %2"`，表明这个积木包含了两个参数，参数的占位符用%+序号的形式表示，序号从1开始，如：`%1、%2`。而参数的具体内容、类型定义，则在args0中实现。
在参数定义args0中，`type`指参数类型，`name`为参数名称，当参数类型为`field_dropdown`（列表）时，`options`为列表的可选内容。以下将列举常用的参数类型：

- **列表：field_dropdown**
&nbsp;&nbsp;field_dropdown，与options组合使用，options的值是一个列表，列表的每个值是为`['显示内容', '实际值']`，如：
```js
{
  type: 'field_dropdown',
  name: 'UNIT',
  options: [['cm', '1'], ['inch', '2']]
}
```
&emsp;&emsp;需要注意的是，不管是什么类型的数据，显示内容和实际值都要以字符串的形式。

---

- **图片型：field_image**
field_image图片型参数的实现如下:
```js
{
  type: 'field_image',
  src: OLED_ICO,
  width: 30,
  height: 30
}
```
&emsp;&emsp;其中OLED_ICO是图片的base64值，如：
```
const OLED_ICO = "data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMTAyNCIgaGVpZ2h0PSIxMDI0IiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIGNsYXNzPSJpY29uIj4KIDxkZWZzPgogIDxzdHlsZSB0eXBlPSJ0ZXh0L2NzcyIvPgogPC9kZWZzPgogPGc+CiAgPHRpdGxlPmJhY2tncm91bmQ8L3RpdGxlPgogIDxyZWN0IGZpbGw9Im5vbmUiIGlkPSJjYW52YXNfYmFja2dyb3VuZCIgaGVpZ2h0PSI0MDIiIHdpZHRoPSI1ODIiIHk9Ii0xIiB4PSItMSIvPgogPC9nPgogPGc+CiAgPHRpdGxlPkxheWVyIDE8L3RpdGxlPgogIDxwYXRoIGZpbGw9IiNmZmZmZmYiIGlkPSJzdmdfMSIgZD0ibTEwMjQsNzY4bDAsLTY0MGMwLC0xNy43IC0xNC4zLC0zMiAtMzIsLTMybC05NjAsMGMtMTcuNywwIC0zMiwxNC4zIC0zMiwzMmwwLDY0MGMwLDE3LjcgMTQuMywzMiAzMiwzMmw0NDAsMGM0LjQsMCA4LDMuNiA4LDhsMCwyNGMwLDE3LjcgLTE0LjMsMzIgLTMyLDMybC0xNzYsMGMtMTcuNywwIC0zMiwxNC4zIC0zMiwzMnMxNC4zLDMyIDMyLDMybDQ4MCwwYzE3LjcsMCAzMiwtMTQuMyAzMiwtMzJzLTE0LjMsLTMyIC0zMiwtMzJsLTE3NiwwYy0xNy43LDAgLTMyLC0xNC4zIC0zMiwtMzJsMCwtMjRjMCwtNC40IDMuNiwtOCA4LC04bDQ0MCwwYzE3LjcsMCAzMiwtMTQuMyAzMiwtMzJ6bS05NjAsLTQ4bDAsLTU0NGMwLC04LjggNy4yLC0xNiAxNiwtMTZsODY0LDBjOC44LDAgMTYsNy4yIDE2LDE2bDAsNTQ0YzAsOC44IC03LjIsMTYgLTE2LDE2bC04NjQsMGMtOC44LDAgLTE2LC03LjIgLTE2LC0xNnoiLz4KICA8dGV4dCBzdHJva2U9Im51bGwiIHRyYW5zZm9ybT0ibWF0cml4KDEzLjYzNzg0NzE0NzgzOTM1MiwwLDAsMjAuNzE4NjIzMDU5NjU2MjM4LC0yNzQ2LjYwNTUzMzcyODE2MSwtNjMwMy40NDc3MTMwNjA0NzQpICIgeG1sOnNwYWNlPSJwcmVzZXJ2ZSIgdGV4dC1hbmNob3I9InN0YXJ0IiBmb250LWZhbWlseT0iSGVsdmV0aWNhLCBBcmlhbCwgc2Fucy1zZXJpZiIgZm9udC1zaXplPSIyNCIgaWQ9InN2Z18yIiB5PSIzMzQuMTg1OTgxIiB4PSIyMDYuNjc1MTg5IiBzdHJva2Utb3BhY2l0eT0ibnVsbCIgc3Ryb2tlLXdpZHRoPSIwIiBmaWxsPSIjZmZmZmZmIj5PTEVEPC90ZXh0PgogPC9nPgo8L3N2Zz4=";
```
---

- **输入型数据：input_value**
&nbsp;&nbsp;input_value是输入型数据，数据的具体类型（数字或字符串等）需要在toolbox.js中实现,如积木![openblock作品-1659425459061.png](/openblock作品-1659425459061.png =150x30)的参数定义为：
```js
{
  type: 'input_value',
  name: 'INDEX'
}
```
&emsp;&emsp;同时，须在toolbox.js中定义参数的具体类型，如下所示：
```
<block type="dht_readHumidity">
  <value name="INDEX">
    <shadow type="math_whole_number"> // 数据类型
      <field name="NUM">1</field>     // 默认值
		</shadow>
	</value>
</block>
```
&emsp;&emsp;可能的数据类型有：
1. math_number：任何数字
1. math_integer：整数
1. math_whole_number：任何数字
1. math_positive_number：正数
1. math_angle：角度
1. matrix：5x5点阵
1. text：字符串文本
1. colour_picker:颜色
<br/>

&emsp;&emsp;数字类型的参数在toolbox.js中的定义方式为：
```
<value name="INDEX"> // 参数名
    <shadow type="math_whole_number"> // 数据类型，可选不同的数字类型
      <field name="NUM">1</field>     // 默认值，field name="NUM"为固定
		</shadow>
</value>
```
---
&emsp;&emsp;`math_angle`（角度）类型的参数在toolbox.js中的定义方式为：
```
<value name="VALUE"> // 参数名
    <shadow type="math_angle"> // 数据类型math_angle
      <field name="NUM">90</field>     // 默认值，field name="NUM"为固定
		</shadow>
</value>
```
&emsp;&emsp;角度型参数的效果如下图：
&emsp;&emsp;![微信截图_20220803110116.png](/微信截图_20220803110116.png)

---
&emsp;&emsp;`matrix`（点阵）类型的参数在toolbox.js中的定义方式为：
```
<value name="VALUE"> // 参数名
    <shadow type="matrix"> // 数据类型matrix
      <field name="MATRIX">0000000000000000000000000</field> // field name="MATRIX"为固定,15个0表示全灭
		</shadow>
</value>
```
&emsp;&emsp;点阵型参数的效果如下图：
&emsp;&emsp;![微信截图_20220803110916.png](/微信截图_20220803110916.png)

---
&emsp;&emsp;`text`（字符串文本）类型的参数在toolbox.js中的定义方式为：
```
<value name="VALUE"> // 参数名
    <shadow type="text"> // 数据类型text
      <field name="TEXT">HELLO</field> // field name="TEXT"为固定, 默认值"HELLO"
		</shadow>
</value>
```
---
&emsp;&emsp;`colour_picker`（颜色）类型的参数在toolbox.js中的定义方式为：
```
<value name="VALUE"> // 参数名
    <shadow type="colour_picker"> // 数据类型colour_picker
    	<field name="COLOUR">#ff0000</field> // field name="COLOUR"为固定, 默认颜色红色
		</shadow>
</value>
```
&emsp;&emsp;颜色型参数的使用效果如下图：
&emsp;&emsp;![微信截图_20220803111455.png](/微信截图_20220803111455.png)

---
- **分支：input_statement**
&nbsp;&nbsp;分支型参数的定义只需在args0中以如下方式定义即可：
```js
{
  type: 'input_statement',
  name: 'BRANCH'
}
```
&emsp;&emsp;分支型参数的效果为：
&emsp;&emsp;![微信截图_20220803112334.png](/微信截图_20220803112334.png)
&emsp;&emsp;需要注意的是，这种分支型的参数，需要将积木内容定义分为两部分来实现，所以这个积木的内容需要两个message来实现，代码实现如下：
```js
Blockly.Blocks.button_execute = {
  init: function () {
    this.jsonInit({
      message0: Blockly.Msg.BUTTON_EXECUTE,
      message1: '%1', // 分支部分直接一个参数%1
      args0: [
        {
          type: 'field_dropdown',
          name: 'PIN',
          options: digitalPins
        }
      ],
      args1: [
        {
          type: 'input_statement',
          name: 'BRANCH'
        }
      ],
      colour: "#4C97FF",
      extensions: ['shape_statement']
    });
  }
};
```
&emsp;&emsp;每个message对应一个args（没有参数的除外），args的序号与message对应，如message0对应args0、message1对应args1。其中，msg.js中`BUTTON_EXECUTE`的定义为：`"BUTTON_EXECUTE": "如果按钮 端口 %1 按下 执行"`；toolbox.js中`button_execute`的定义为`<block type="button_execute"/>`
> 可以将积木的内容分为几个部分来实现,每一个部分对应一个messge以及args，从0开始排序，如将积木的内容分为两个部分，则有message0、message1, 对应args0、args1。
{.is-info}

---
- **变量：field_variable**
&nbsp;&nbsp;使用变量类型参数可以获取在变量代码组中定义的变量。
```js
{
  type: 'field_variable',
  name: 'VAR'
}
```
&emsp;&emsp;变量型参数的使用效果如下图：
&emsp;&emsp;![微信截图_20220803113918.png](/微信截图_20220803113918.png)

---
- **滑条型：field_slider**
&nbsp;&nbsp;使用滑条型参数时，需要先定义一个滑条型参数的积木，代码如下：
```js
Blockly.Blocks.my_slider = {
  init: function () {
    this.jsonInit({
      message0: '%1',
      args0: [
        {
          type: 'field_slider',
          name: 'NUM', // 值名称
          value: '0', // 默认值
          precision: 1,  // 精度
          min: '0', // 最小值
          max: '100' // 最大值
        }
      ],
      output: 'Number',
      outputShape: Blockly.OUTPUT_SHAPE_ROUND,
      colour: Blockly.Colours.textField,
      colourSecondary: Blockly.Colours.textField,
      colourTertiary: Blockly.Colours.textField
    });
  }
};
```
&emsp;&emsp;之后通过将参数类型设为`my_slider`来得到滑条型参数。例如，blocks.js中积木定义为：
```js
Blockly.Blocks.led_set = {
  init: function () {
    this.jsonInit({
      message0: Blockly.Msg.LED_SET,
      args0: [
        {
          type: 'field_dropdown',
          name: 'PIN',
          options: digitalPins
        },
        {
          type: 'input_value', // 滑条型参数，需要在toolbox.js中对参数类型进行具体定义
          name: 'VALUE'
        }
      ],
      colour: "#4C97FF",
      extensions: ['shape_statement']
    });
  }
};
```
&emsp;&emsp;toolbox.js中的定义为：
```
<block type="led_set">
	<value name="VALUE">
		<shadow type="my_slider"> // 数据类型
			<field name="NUM">20</field>     // 默认值
		</shadow>
	</value>
</block>
```
&emsp;&emsp;最后，到msg.js中定义`LED_SET`为`"LED_SET": "LED灯 端口 %1 设置亮度 %2"`，得到最终效果如下图：
&emsp;&emsp;![微信截图_20220803114821.png](/微信截图_20220803114821.png)

---
- **自定义类型**
&nbsp;&nbsp;积木的参数还可以是自定义的积木类型，之前的滑块型`my_slider`其实也属于自定义积木，而所有数值型的积木也都可以作为自定义参数类型来使用，只需和`my_slider`的使用方式一样在toolbox.js中指定`<shadow type="积木名称id"/>`即可。
&emsp;&emsp;如，积木![openblock作品-1659508408429.png](/openblock作品-1659508408429.png  =80x30)在blocks.js中的定义为
```js
Blockly.Blocks.high_low = {
  init: function () {
    this.jsonInit({
      message0: '%1',
      args0: [
        {
          type: 'field_dropdown',
          name: 'NUM',
          options: [['HIGH', '1'], ['LOW', '0']]
        }
      ],
      colour: '#4C97FF',
      extensions: ['output_boolean']
    });
  }
};
```
&emsp;&emsp;而积木![openblock作品-1659508414107.png](/openblock作品-1659508414107.png =250x40)用![openblock作品-1659508408429.png](/openblock作品-1659508408429.png  =80x30)作为参数时的实现方式如下：
```
<block type="relay_set">
	<value name="STATE">
		<shadow type="high_low"/> // 数据类型
	</value>
</block>
```
```js
Blockly.Blocks.relay_set = {
  init: function () {
    this.jsonInit({
      message0: Blockly.Msg.RELAY_SET,
      args0: [
        {
          type: 'field_dropdown',
          name: 'PIN',
          options: digitalPins
        },
        {
          type: 'input_value',
          name: 'STATE',
        }
      ],
      colour: '#4C97FF',
      extensions: ['shape_statement']
    });
  }
};
```

<br/>

## 积木功能代码实现
积木的功能代码实现在generator.js中实现,generator.js文件中，主要有一个function addGenerator，返回所有积木的功能代码定义。这个文件的基本结构如下所示：
```js
function addGenerator (Blockly) {
    Blockly.Arduino.chineseTTS_init = function (block) {
        const tx = block.getFieldValue('TX');
        const rx = block.getFieldValue('RX');

        Blockly.Arduino.includes_.chineseTTS_init = `#include <Openblock_chineseTTS.h>`;
        Blockly.Arduino.definitions_.chineseTTS_init = `OB_ChineseTTS chineseTTSSerial(${rx}, ${tx});`;

        return `chineseTTSSerial.begin();\n`;
    };

    return Blockly;
}

exports = addGenerator;
```
在这个文件中，需要对所支持的编程语言做区分，如，`Blockly.Arduino`表示支持的是arduino，而microbit和microPython使用的是`Blockly.Python`。
以下将从四个方面来讲解积木功能代码的具体实现：
- 获取参数值
- 引入库、建立变量和函数
- 实现初始化代码
- 不同类型积木的return返回值
<br/>

### 获取参数值
根据参数类型的不同，主要使用以下三种方式获取参数的值：
```js
// 列表型
const pin = block.getFieldValue('PIN');
// 数值型，参数类型为input_value的参数
const value = Blockly.Arduino.valueToCode(block, 'VALUE', Blockly.Arduino.ORDER_ATOMIC) || '0'; // || '0' 为默认值，可以不加
// 分支型input_statement,返回分支中所有代码的实际功能代码
const brach = Blockly.Arduino.statementToCode(block, 'BRANCH');
```
对于以上代码中的block，是从`Blockly.Arduino.chineseTTS_init = function (block)`中传进来的参数block，这个参数也可以不传，不传参数时，可以用this进行调用，如`const pin = this.getFieldValue('PIN');`
另外，如果是python插件，则将其中的`Blockly.Arduino`换成`Blockly.Python`即可。
<br/>

### 引入库、建立变量和函数
不论是引入库，还是建立变量或函数，对于arduino插件来说都使用代码`Blockly.Arduino.definitions_[名称]`，相当于给引入库这行代码或建立的变量、函数起一个名称，当遇到重复名称的代码，在OB的源码区将不再显示。如：
```js
Blockly.Arduino.includes_.chineseTTS_init = `#include <Openblock_chineseTTS.h>`;
```
而如果是python插件，则引入库需要使用`Blockly.Python.imports_[名称]`，建立变量使用`Blockly.Python.variables_[名称]`，建立函数使用`Blockly.Python.customFunctions_[名称]`，如
```js
Blockly.Python.imports_.ultrasonic_readDistance = `from hcsr04_v0_2_1 import HCSR04`;
Blockly.Python.variables_[`ultrasonic_${trig}_${echo}`] = `ultrasonic_${trig}_${echo} = HCSR04(trigger_pin = ${trig}, echo_pin = ${echo})`;
Blockly.Python.customFunctions_[`func_test`] = `def funcTest():\n`
	+ `	print('this is a test function’)\n`;
```
<br/>

### 实现初始化代码
当需要使用初始化代码时，可以使用`Blockly.Arduino.setups_[名称]`，同样，如果是python插件，则使用`Blockly.Python.setups_[名称]`。如：
```js
Blockly.Arduino.setups_[`setup_input_${pin}`] = `pinMode(${pin}, INPUT);`;
```
> 需要注意的是，无论是引入库、建立变量和函数还是初始化代码，当使用不同端口时，这个代码有所不同时，那么给这些代码赋予的名称也要有所不同，通常可以在名称中加上端口以做区分。如`setup_input_${pin}`。
{.is-warning}

<br/>

### 不同类型积木的return返回值
积木的实际功能代码一般情况下放在一个字符串变量中返回，而对于不同类型的积木，return返回值的内容有所不同，主要分数值型和命令型两种
**数值型返回的是两值，代码和值类型：**
```js
Blockly.Arduino.dht_readHumidity = function (block) {
  const no = Blockly.Arduino.valueToCode(block, 'NO', Blockly.Arduino.ORDER_ATOMIC);
  const code = `dht_${no}.readHumidity()`;
  return [code, Blockly.Arduino.ORDER_ATOMIC];
};
```
**命令型直接返回实际的功能代码：**
```js
Blockly.Arduino.chineseTTS_init = function (block) {
  const tx = block.getFieldValue('TX');
  const rx = block.getFieldValue('RX');

  Blockly.Arduino.includes_.chineseTTS_init = `#include <Openblock_chineseTTS.h>`;
  Blockly.Arduino.definitions_.chineseTTS_init = `OB_ChineseTTS chineseTTSSerial(${rx}, ${tx});`;

  return `chineseTTSSerial.begin();\n`;
};
```










