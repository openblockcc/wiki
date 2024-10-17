---
title: Old Version External Resource Migration Guide
description: 
published: true
date: 2024-10-17T04:46:01.390Z
tags: developer
editor: markdown
dateCreated: 2024-10-17T04:46:01.390Z
---

# Migration Guide for Older Versions of External Resources

In the new OpenBlock 2.5.0 update, there has been a significant structural change to the external-resource system. The official external-resource repository has now been migrated to [external-resources-v3](https://github.com/openblockcc/external-resources-v3).

## Overview of Changes in the New Framework

### Better Support for Customized external-resource

OpenBlock now reads the `OPENBLOCK_EXTERNAL_RESOURCES` environment variable at startup. If the path specified by this variable exists, it will load the contents from that path instead of using the built-in external-resource. This way, we can avoid third-party custom content being overwritten during official software updates.

Additionally, OpenBlock will scan the `OpenBlockExternalResources` directory at the same level as the installation path. If this directory exists, it will load its contents.
> The latter method has a lower priority than the environment variable method and can only be used on Windows systems.
{.is-warning}

### No Longer Copies external-resource to Cache Directory

The software will no longer copy the external-resources from the installation path or third-party customized resources to the cache directory at startup. Therefore, when modifying or writing external-resources, you no longer need to worry about caching issues. Simply modify the original files directly.

### No Longer Provides `device.js` File by Default

The official `external-resources/devices` directory no longer includes the `device.js` file by default. Devices will now be listed based on definitions in the source code. However, third parties can still create `device.js` to customize their device list.

### Flattened Path Structure

In the new version of `external-resources`, both `extensions` and `devices` are no longer placed in separate subfolders according to categories. Instead, they are all placed in the same directory. This helps avoid ID conflicts and makes management easier.

### Changed Registration Functions

In the new version, the registration functions in each file have been modified:

- The `addBlocks` function in `blocks.js` has been renamed to `registerBlocks`
- The `addGenerator` function in `generator.js` has been renamed to `registerGenerators`
- The `addToolbox` function in `toolbox.js` has been renamed to `registerToolboxs`

With these changes, the new names are more consistent with their actual functionality.

### Consolidated Translation Content

In the new version, the translations previously defined in the `official-locales.json` and `third-party-locales.json` files located in the outermost directory of external-resources have been moved to the `translations.js` file within each resource directory. This makes maintaining and updating translation files more convenient and modular.

## Migration Steps

### Flattened Path Structure

Refer to the structure of external-resources-v3 and move the resources from the subdirectories of each category into the `extensions` and `devices` directories.

### Replace Registration Functions

Use an editor to perform batch replacements as follows:
- Replace `addBlocks` with `registerBlocks`
- Replace `addGenerator` with `registerGenerators`
- Replace `addToolbox` with `registerToolboxs`

### Create New Translation File

In each `extensions` and `devices` directory, create a `translations.js` file according to the following template:

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
    };
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
