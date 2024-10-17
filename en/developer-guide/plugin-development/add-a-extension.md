---
title: Add an Extension
description: 
published: true
date: 2024-10-17T04:32:57.324Z
tags: developer
editor: markdown
dateCreated: 2024-10-17T04:32:57.324Z
---

# Adding an Extension

Next, we will demonstrate how to write an extension resource by creating an LED module resource compatible with Arduino UNO as an example.

1. Create an Extension Folder

First, create a new folder in the `./extensions` directory named after the extension, following camel case: `commonLed`.

```bash
mkdir ./extensions/commonLed
cd ./extensions/commonLed
```

2. Create `index.js` File

The `index.js` file is used to describe various attributes of the extension. Create this file and write the following content.

```js
const commonLed = formatMessage => ({
    name: formatMessage({
        id: 'commonLed.name',
        default: 'Common LED',
        description: 'name of common led extension'
    }),
    extensionId: 'commonLed',
    version: '0.0.1',
    supportDevice: ['arduinoUno', 'arduinoNano', 'arduinoLeonardo', 'arduinoMega2560'],
    author: 'Your Name',
    iconURL: `assets/commonLed.png`,
    description: formatMessage({
        id: 'commonLed.description',
        default: 'This is a demo with a common led.',
        description: 'Description of common led'
    }),
    featured: true,
    blocks: 'blocks.js',
    generator: 'generator.js',
    toolbox: 'toolbox.js',
    translations: 'translations.js',
    tags: ['actuator'],
    helpLink: 'https://wiki.openblock.cc'
});

module.exports = commonLed;
```

Then, according to the `iconURL` attribute, create an `assets` folder, download the image below, and place it inside.

- [commonled.png](/developer-guide/plugin-development/add-a-extension/commonled.png)

![commonled.png](/developer-guide/plugin-development/add-a-extension/commonled.png)

3. Create `blocks.js` File

This file describes the style structure of the blocks. Create it and write the following content.

```js
function registerBlocks (Blockly) {
    const color = '#A1C057';
    const secondaryColour = '#82A14C';

    Blockly.Blocks.commonLed_setLEDState = {
        init: function () {
            this.jsonInit({
                message0: Blockly.Msg.COMMONLED_SETLEDSTATE,
                args0: [
                    {
                        type: 'input_value',
                        name: 'pin'
                    },
                    {
                        type: 'field_dropdown',
                        name: 'state',
                        options: [
                            [Blockly.Msg.COMMONLED_ON, '1'],
                            [Blockly.Msg.COMMONLED_OFF, '0']]
                    }
                ],
                colour: color,
                secondaryColour: secondaryColour,
                extensions: ['shape_statement']
            });
        }
    };

    return Blockly;
}

exports = registerBlocks;
```
The contents of `Blockly.Msg.XXX` are multilingual support texts, and their actual content is defined in the `translations.js` file.

4. Create `toolbox.js` File

This file defines the style of the blocks in the left toolbox. Create it and write the following content.

```js
function registerToolboxs () {
    return `
<category name="%{BKY_COMMONLED_CATEGORY}" id="COMMONLED_CATEGORY" colour="#A6D200" secondaryColour="#A1C057">
    <block type="commonLed_setLEDState" id="commonLed_setLEDState">
        <value name="pin">
            <shadow type="math_number">
                <field name="NUM">2</field>
            </shadow>
        </value>
    </block>
</category>`;
}

exports = registerToolboxs;
```

The `BKY_COMMONLED_CATEGORY` toolbox category name is a multilingual support text, and its actual content is defined in the `translations.js` file.

5. Create `translations.js` File

This file serves as a translation file for multilingual support. Create it and write the following content.

```js
function getInterfaceTranslations () {
    return {
        "en": {
            "commonLed.name": "Common LED",
            "commonLed.description": "This is a demo with a common led."
        },
        "ru": {
            "commonLed.name": "Общий светодиод",
            "commonLed.description": "Это демо с общим светодиодом."
        },
        "zh-cn": {
            "commonLed.name": "普通 LED",
            "commonLed.description": "这是一个通用 LED 的演示。"
        },
        "zh-tw": {
            "commonLed.name": "普通 LED",
            "commonLed.description": "這是一個一般 LED 的演示。"
        }
    }
    ;
}

function registerBlocksMessages (Blockly) {
    Object.assign(Blockly.ScratchMsgs.locales["en"],
        {
            "COMMONLED_CATEGORY": "COMMONLED LED",
            "COMMONLED_OFF": "off",
            "COMMONLED_ON": "on",
            "COMMONLED_SETLEDSTATE": "set pin %1 LED %2"
        }
    );

    Object.assign(Blockly.ScratchMsgs.locales["ru"],
        {
            "COMMONLED_CATEGORY": "COMMONLED LED",
            "COMMONLED_OFF": "off",
            "COMMONLED_ON": "on",
            "COMMONLED_SETLEDSTATE": "set pin %1 LED %2"
        }
    );

    Object.assign(Blockly.ScratchMsgs.locales["zh-cn"],
        {
            "COMMONLED_CATEGORY": "COMMONLED LED",
            "COMMONLED_OFF": "off",
            "COMMONLED_ON": "on",
            "COMMONLED_SETLEDSTATE": "set pin %1 LED %2"
        }
    );

    Object.assign(Blockly.ScratchMsgs.locales["zh-tw"],
        {
            "COMMONLED_CATEGORY": "COMMONLED LED",
            "COMMONLED_OFF": "off",
            "COMMONLED_ON": "on",
            "COMMONLED_SETLEDSTATE": "set pin %1 LED %2"
        }
    );

    return Blockly;
}

if (typeof module !== 'undefined') {
    module.exports = {getInterfaceTranslations};
}
exports = registerBlocksMessages;
```

6. Create `generator.js` File

The `generator.js` file defines the code generation rules for the blocks of this resource. Create it and write the following content.

```js
function registerGenerators (Blockly) {
    Blockly.Arduino.commonLed_setLEDState = function (block) {
        const pin = Blockly.Arduino.valueToCode(block, 'pin', Blockly.Arduino.ORDER_ATOMIC);
        const state = this.getFieldValue('state');

        Blockly.Arduino.setups_[`commonLed_init${pin}`] = `pinMode(${pin}, OUTPUT);`;

        return `digitalWrite(${pin}, ${state});\n`;
    };

    return Blockly;
}

exports = registerGenerators;
```

7. Completion

Finally, we restart or open OpenBlock, select Arduino UNO, switch to upload mode, and we can use the new module we just created in the extension selection interface.

![commonledselection.png](/developer-guide/plugin-development/add-a-extension/commonledselection.png)
![commonleduseage.png](/developer-guide/plugin-development/add-a-extension/commonleduseage.png)

## Attachment

[1] [commonLed Extension Resource Package.zip](/developer-guide/plugin-development/add-a-extension/commonled.zip)
