---
title: 准备工作
description: 
published: true
date: 2024-10-12T04:30:11.114Z
tags: 
editor: markdown
dateCreated: 2024-07-17T06:33:01.278Z
---

# 准备工作

## 要求

请确保你的计算机已经安装好了以下软件或工具。

- Node.js 14/16 （过高或过低的版本可能会导致一些未知的错误）
- git
- 代码编辑器（推荐使用VSCode)

## 步骤

1. 获取外部资源的工程代码

```bash
git clone https://github.com/openblockcc/external-resources-v3.git external-resources-v3
```

2. 安装 nodejs 依赖

```bash
cd external-resources-v3
npm ci
```

3. 将当前的资源路径添加到环境变量中

### Tab {.tabset}
#### Windows

以管理员权限打开 powershell 运行 `./setup.sh`，或者也可以直接右键脚本 `setup.sh` 以管理员方式运行。

#### MacOS/Linux

```bash
sudo ./setup.sh
```
由于类 Unix 系统的特殊性，执行完成后我们还需要重启系统或者注销用户重新登陆，设置的环境变量才会生效。
  
### {.tabset}

4. 验证环境变量是否生效 

在脚本运行完成后，当前的资源路径就已经被设置到了系统的环境变量中了，可以被 Resource Server 扫描到了，我们可以重新打开一个新的终端来验证以下。

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

如果正常的话，将会输出当前资源工程的路径。

4. 验证 OpenBlock 是否会优先使用当前的资源工程

打开 `./extensions/apds9960/translations.js` 文件，将 `getInterfaceTranslations` 函数中的所有语言的 `apds9960.description` 修改为一个测试数据。

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

而后使用命令行打开 OpenBlock，具体的命令需要根据实际情况调整路径。

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

在打开的软件中选择 Arduino Uno 主板，切换到上传模式并打开插件选择界面，可以看到 APDS9960 的描述已经变成了我们修改的内容。

![apds9960demo.png](/developer-guide/plugin-development/reparations/apds9960demo.png)

同时可以看到终端中显示了当前 Resource Server 使用的资源路径。(适用于v2.5.3 以上版本)

```bash
...
env OPENBLOCK_EXTERNAL_RESOURCES: "your/resource/path/OpenBlockExternalResources"
cached external resources path: "cache/path/external-resources"
builtin external resources path: "your/resource/path/OpenBlockExternalResources"
Openblock resource server start successfully, socket listen on: http://0.0.0.0:20112
...
```

到此我们的开发环境就搭建完成，可以进行接下来的开发了。

