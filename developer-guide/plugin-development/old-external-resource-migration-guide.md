---
title: 旧版本外部资源迁移指南
description: 
published: true
date: 2024-07-18T15:55:45.220Z
tags: 
editor: markdown
dateCreated: 2024-07-05T13:48:54.515Z
---

# 旧版本外部资源迁移指南

在新的 OpenBlock2.5.0 的更新中，external-resource 迎来了一次较大构架调整，目前官方 external-resource 仓库地址已经迁移到了 [external-resources-v3](https://github.com/openblockcc/external-resources-v3)。

## 新框架改动内容简述

### 更好的客制化的 external-resource 支持

目前 OpenBlock 在启动时会读取环境变量 `OPENBLOCK_EXTERNAL_RESOURCES` ，如果该路径存在则会加载路径中的内容，而非使用软件内自带的 external-resource。通过这样的方式我们就可以避免在官方软件主体更新时覆盖掉第三方客制化的内容了。   
   
其次 OpenBlock 还会扫描在安装路径同级目录下的 `OpenBlockExternalResources` 目录，如果该路径存在则会加载路径中的内容。
> 后者的方式优先级要弱于设置的环境变量方式，且仅能够在 Windows 系统中使用
{.is-warning}
   
### 不再拷贝 external-resource 到缓存目录

软件启动后不再将安装路径或第三方客制化的 external-resources 拷贝到缓存目录中。因此我们在修改与编写 external-resources 时不必再考虑缓存问题，直接修改原文件即可。

### 默认不再提供 device.js 文件

官方的 `external-resources/devices` 目录中默认不再放置 `device.js` 文件，将根据源代码中的定义排列设备。不过第三方仍然可以通过创建 `device.js` 来客制化自己的设备列表。

### 扁平化路径

新版本的 `external-resources` 中的 `extensions` 与 `devices` 都不再按照大类放置于不同的文件夹内，而是统一的放置在同一个目录下，这将有助于避免 id 重合和便于管理。

### 变更注册函数
	
新版本中，各个文件的注册函数均有所变化。

`blocks.js` 中的 `addBlocks` 函数名称变更为了 `registerBlocks`
`generator.js` 中的 `addGenerator` 函数名称变更为了 `registerGenerators`
`toolbox.js` 中的 `addToolbox` 函数名称变更为了 `registerToolboxs`

在调整这些函数名称后，新的名称更加贴切实际功能。

### 整合翻译内容

在新版本中，原本定义在 external-resources 最外层目录中的 `official-locales.json` 与 `third-party-locales.json` 文件中的翻译与积木的 MSG 翻译被转移到了各 resources 目录下的 `translations.js` 文件中。这样我们就避免了维护一个交织在一起的翻译文件可以更加便捷的增减的资源包了。

## 迁移操作

### 扁平化路径

参照 external-resources-v3 的结构，将原本各个大类下的子目录中的 resources 全部移动到 extensions 与 devices 目录下即可。

### 替换注册函数

通过编辑器按照下方批量替换即可
`addBlocks` 替换为 `registerBlocks`
`addGenerator` 替换为 `registerGenerators`
`addToolbox` 替换为 `registerToolboxs`

### 创建新的翻译文件

在每个 extensions 与 devices 中参照下方模板创建 `translations.js` 文件

```js
// This file was automatically generated. Do not modify.
/* eslint-disable func-style */
/* eslint-disable require-jsdoc */
/* eslint-disable quotes */
/* eslint-disable quote-props */
/* eslint-disable dot-notation */
/* eslint-disable max-len */
function getInterfaceTranslations () {
    return {
        "en": {
            ...
        },
        "ru": {
            ...
        },
        "zh-cn": {
            ...
        },
        "zh-tw": {
            ...
        }
    }
    ;
}

function registerScratchExtensionTranslations () {
    return {};
}

function registerBlocksMessages (Blockly) {
    Object.assign(Blockly.ScratchMsgs.locales["en"],
        {
            ...
        }
    );

    Object.assign(Blockly.ScratchMsgs.locales["ru"],
        {
            ...
        }
    );

    Object.assign(Blockly.ScratchMsgs.locales["zh-cn"],
        {
            ...
        }
    );

    Object.assign(Blockly.ScratchMsgs.locales["zh-tw"],
        {
           ...
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

`registerBlocksMessages` 函数中放置原本的 `msg.js` 文件中的内容。
`getInterfaceTranslations` 放置原本定义在 `*locales.json`  中的 index.js 的翻译。
`registerScratchExtensionTranslations` 保持空白即可，这部分内容将在发行版的热加载功能中启用。

将 index.js 文件中的 `msg: 'msg.js',` 属性替换为 `translations: 'translations.js'`

最后删除不再使用的文件：`official-locales.json`， `third-party-locales.json`， `msg.js`。

至此我们就完成了全部的 external-resources 迁移操作，可以在新版本的 OpenBlock 中使用了。

