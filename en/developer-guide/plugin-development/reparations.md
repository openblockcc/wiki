---
title: Reparations
description: 
published: true
date: 2024-10-17T04:27:56.431Z
tags: developer
editor: markdown
dateCreated: 2024-10-17T04:27:56.431Z
---

# Preparations

## Requirements

Please ensure that the following software or tools are installed on your computer.

- Node.js 14/16 (versions that are too high or too low may cause unknown errors)
- git
- Code editor (VSCode is recommended)

## Steps

1. Obtain the external resource project code

```bash
git clone https://github.com/openblockcc/external-resources-v3.git external-resources-v3
```

2. Install Node.js dependencies

```bash
cd external-resources-v3
npm ci
```

3. Add the current resource path to the environment variables

### Tab {.tabset}
#### Windows

Open PowerShell with administrator privileges and run `./setup.sh`, or you can right-click the `setup.sh` script and run it as an administrator.

#### MacOS/Linux

```bash
sudo ./setup.sh
```

Due to the nature of Unix-like systems, after execution, we need to restart the system or log out and log back in for the environment variable settings to take effect.

### {.tabset}

4. Verify whether the environment variables are effective

After the script runs, the current resource path has been set to the system's environment variables and can be scanned by the Resource Server. We can open a new terminal to verify this.

### Tab {.tabset}
#### Windows

```bash
echo $env:OPENBLOCK_EXTERNAL_RESOURCES
```

#### MacOS/Linux

```bash
echo $OPENBLOCK_EXTERNAL_RESOURCES
```

### {.tabset}

If everything is normal, it will output the path of the current resource project.

5. Verify that OpenBlock prioritizes using the current resource project

Open the `./extensions/apds9960/translations.js` file and modify all language `apds9960.description` entries in the `getInterfaceTranslations` function to test data.

```js
function getInterfaceTranslations () {
    return {
        "en": {
            "apds9960.description": "Test."
        },
        "ru": {
            "apds9960.description": "Test."
        },
        "zh-cn": {
            "apds9960.description": "Test."
        },
        "zh-tw": {
            "apds9960.description": "Test."
        }
    }
    ;
}
```

Then, use the command line to open OpenBlock, adjusting the command according to your actual path.

### Tab {.tabset}
#### Windows

```bash
/your/openblock/installation/path/OpenBlockDesktop.exe
```

#### MacOS

```bash
/Application/OpenBlockDesktop.app/Content/MacOS/OpenBlockDesktop
```

#### Linux

```bash
/opt/OpenBlockDesktop/openblock-desktop
```

### {.tabset}

In the opened software, select the Arduino Uno mainboard, switch to upload mode, and open the plugin selection interface. You should see that the description of APDS9960 has changed to the content we modified.

![apds9960demo.png](/developer-guide/plugin-development/reparations/apds9960demo.png)

At the same time, you can see the terminal displaying the current resource path used by the Resource Server (applicable to versions 2.5.3 and above).

```bash
...
env OPENBLOCK_EXTERNAL_RESOURCES: "your/resource/path/OpenBlockExternalResources"
cached external resources path: "cache/path/external-resources"
builtin external resources path: "your/resource/path/OpenBlockExternalResources"
Openblock resource server start successfully, socket listen on: http://0.0.0.0:20112
...
```

At this point, our development environment has been set up, and we can proceed with the subsequent development.
