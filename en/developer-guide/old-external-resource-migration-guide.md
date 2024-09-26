---
title: External Resource Migration Guide for Older Versions
description: 
published: true
date: 2024-07-08T11:22:29.582Z
tags: 
editor: markdown
dateCreated: 2024-07-05T14:38:31.179Z
---

# External Resource Migration Guide for Older Versions

In the new OpenBlock 2.5.0 update, external-resource has undergone a significant structural change. The official external-resource repository has now been migrated to [external-resources-v3](https://github.com/openblockcc/external-resources-v3).

## Summary of New Framework Changes

### Better Customization Support for External Resources

OpenBlock now scans for an `OpenBlockExternalResources` directory at the same level as the installation path during startup. If this path exists, it will load the content from this directory as the external resource instead of using the built-in external resource. This approach avoids overwriting third-party custom content when updating the main software.

### No Longer Copying External Resources to Cache Directory

The software will no longer copy the external resources from the installation path or third-party customizations to the cache directory after startup. This means you can directly modify the original files without worrying about cache issues.

### Device.js File No Longer Provided by Default

The official `external-resources/devices` directory no longer includes a `device.js` file by default. Devices will be arranged based on definitions in the source code. Third parties can still create a `device.js` file to customize their device list.

### Flattened Directory Structure

In the new version of `external-resources`, both `extensions` and `devices` are no longer placed in separate directories by category but are instead placed in a single directory. This helps avoid ID conflicts and makes management easier.

### Changes to Registration Functions

In the new version, the registration functions in various files have changed.

- The `addBlocks` function in `blocks.js` has been renamed to `registerBlocks`.
- The `addGenerator` function in `generator.js` has been renamed to `registerGenerators`.
- The `addToolbox` function in `toolbox.js` has been renamed to `registerToolboxs`.

These new names better reflect their actual functions.

### Integration of Translation Content

In the new version, the translations originally defined in the `official-locales.json` and `third-party-locales.json` files in the external-resources directory have been moved to `translations.js` files in each resources directory. This eliminates the need to maintain a combined translation file, allowing for independent addition and removal of resources.

## Migration Steps

### Place Custom External Resources in the OpenBlockExternalResources Directory

You can place the `OpenBlockExternalResources` directory as follows:

```bash
|- C:/
	|- OpenBlockDesktop/
  	|- ...
	|- OpenBlockExternalResources/
    |- devices/
    |- extensions/
    |- config.json
    |- ...
```

After startup, the software will load the resources in the `OpenBlockExternalResources` directory.

### Flatten Directory Structure

Refer to the structure of external-resources-v3 and move all resources from the subdirectories of each category into the `extensions` and `devices` directories.

### Replace Registration Functions

Use an editor to batch replace the following:
- Replace `addBlocks` with `registerBlocks`.
- Replace `addGenerator` with `registerGenerators`.
- Replace `addToolbox` with `registerToolboxs`.

### Create New Translation Files

Create a `translations.js` file in each extensions and devices directory according to the following template:

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

In the `registerBlocksMessages` function, place the content originally in the `msg.js` file. 
In the `getInterfaceTranslations` function, place the translations originally defined in the `*locales.json` file.
Keep the `registerScratchExtensionTranslations` function blank; this part will be used in the hot loading feature of the release version.

Add the `translations` property in the `index.js` file as follows:

Replace the `msg: 'msg.js',` property in the index.js file with `translations: 'translations.js'`

Finally, delete the unused files: `official-locales.json`, `third-party-locales.json`, and `msg.js`.

By completing these steps, you will have successfully migrated all external resources and can use them in the new version of OpenBlock.