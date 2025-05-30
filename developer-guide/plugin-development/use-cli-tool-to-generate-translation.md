---
title: 使用 CLI 工具生成翻译
description: 
published: true
date: 2024-10-12T04:32:13.979Z
tags: 开发者
editor: markdown
dateCreated: 2024-07-18T15:39:59.082Z
---

# 使用 CLI 工具生成翻译

OpenBlock 官方维护的资源翻译文件均使用了 CLI 工具自动生成，工程会自动从 transifex 推送和拉取翻译并生成 `translations.js` 文件。只要是 `index.js` 文件中标识为 `official: true` 的资源都会被自动的处理。 

当然作为第三方开发者，你也可以在自己的资源中使用这个 CLI 工具，以快速的生成多语言的模板文件，加速创建翻译文件的过程，同时也可以避免在手动创建翻译文件时写错或遗漏内容。

1. 首先我们需要使用 `npm` 在全局安装 `openblock-resource` 包，我们将使用它内置的一个 CLI 命令来生成翻译文件。

```bash
npm i -g openblock-resource
```

2. 以快速开始中 [添加一个扩展](./add-a-extension) 创建的 commonLed 资源为例。为了让 CLI 工具能够自动的处理在 `blocks.js` 文件中使用的 `Blockly.Msg.XXX` 内容，我们需要创建 `msg.json` 文件，在其中定义默认的文本内容。

在 commonLed 资源路径下创建 `msg.json` 并写入以下内容。

```json
{
    "COMMONLED_CATEGORY": "COMMONLED LED",
    "COMMONLED_SETLEDSTATE": "set pin %1 LED %2",
    "COMMONLED_ON": "on",
    "COMMONLED_OFF": "off"
}
```

3. 而后我们就可以运行 CLI 指令来自动生成翻译文件了。

在 commonLed 目录下执行下方指令。

```
i18n-update --thirdParty=true
```

指令执行成功后我们可以看到 CLI 在终端输出的信息，显示 commonLed 的翻译文件已经自动生成。

```
Translations file is created in path: {...}/extensions/commonLed/translations.js
```

此时我们可以打开 `translations.js` 可以看到如下内容。

```js
// The en part of this file is automatically generated. Do not modify.
/* eslint-disable func-style */
/* eslint-disable require-jsdoc */
/* eslint-disable quotes */
/* eslint-disable quote-props */
/* eslint-disable dot-notation */
/* eslint-disable max-len */
function getInterfaceTranslations () {
    return {
        "en": {
            "commonLed.name": "Common LED",
            "commonLed.description": "This is a demo with a common led."
        },
        "ru": {
            "commonLed.name": "Common LED",
            "commonLed.description": "This is a demo with a common led."
        },
        "zh-cn": {
            "commonLed.name": "Common LED",
            "commonLed.description": "This is a demo with a common led."
        },
        "zh-tw": {
            "commonLed.name": "Common LED",
            "commonLed.description": "This is a demo with a common led."
        }
    };
}

function registerScratchExtensionTranslations () {
    return {};
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
exports = registerScratchExtensionTranslations;
exports = registerBlocksMessages;
```

可以看到 CLI 工具已经自动生成了全部的翻译文本。不过 CLI 工具在自动生成时只会生成用户在定义多语言内容时使用的默认文本，其他语言的翻译就需要我们手动修改了。


> 运行 CLI 指令时注意一定要使用 `--thirdParty=true` 参数避免 CLI 工具尝试从 transifex 获取翻译内容。
{.is-warning}

> `i18n-update --thirdParty=true` 应当在资源包的路径下执行，才能够正确的生成翻译文件。
{.is-warning}

> `i18n-update --thirdParty=true` 指令在运行后会覆盖原本的 `translations.js` 文件，如果你在修改添加多语言文本后希望更新它们的内容，请使用 `git` 工具先提交之前旧的翻译再运行该指令，这样在所有语言的翻译都被覆盖后，可以依靠 `git` 工具来手动的合并旧的翻译内容。
{.is-warning}