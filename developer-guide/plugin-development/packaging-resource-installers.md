---
title: 打包发布独立的资源安装包
description: 
published: true
date: 2025-06-12T15:15:14.132Z
tags: 开发者
editor: markdown
dateCreated: 2025-06-03T14:25:10.906Z
---

# 打包发布独立的资源安装包

## 资源包更新机制

在我们参考上个资源部

## 软件打包说明

### MacOS

1. 在项目根目录打开终端，运行打包脚本：

    > 注意修改使用你实际的版本号。
    {.is-info}

    ``` bash
    ./buildResources/build-pkg.sh VERSION="1.0.0"
    ```

2. 脚本执行完毕后，生成的 `.pkg` 安装包文件位于 `./dist` 目录。

### Linux

1. 首先需要安装有 `dpkg-deb` 工具，如果未安装，请运行：

    ``` bash
    sudo apt install -y dpkg-deb
    ```

2. 在项目根目录打开终端，运行打包脚本：

    > 注意修改使用你实际的版本号。
    {.is-info}

    ``` bash
    ./buildResources/build-deb.sh VERSION="1.0.0"
    ```

3. 脚本执行完毕后，生成的 `.deb` 安装包文件位于 `./dist` 目录。

### Windows

1. 首先需要安装有 [Inno Setup](https://jrsoftware.org/isinfo.php)

    > 如果你需要保证对 Windows7 甚至更低版本系统的兼容性，推荐下载 v5.x.x 的版本。 
    {.is-info}
    
    如果你使用 choco 包管理器，可以使用以下指令安装:

    ``` bash
    choco install innosetup --version=5.6.1 --allow-downgrade
    ```

2. 在项目根目录打开终端，运行打包脚本：

    > 注意修改使用你实际的版本号，并将路径修改为你真实的 Inno Setup 安装路径。
    > 由于安装路径可能存在空格所以在执行该指令时 CMD 与 PowerShell 的命令是不同的。
    {.is-info}

    - CMD
    
        ``` bash
        "C:\Program Files (x86)\Inno Setup 5\ISCC.exe" /dVERSION="1.0.0" "./buildResources/setup.iss"
        ```

    - PowerShell
    
        ``` bash
        & "C:\Program Files (x86)\Inno Setup 5\ISCC.exe" /dVERSION="1.0.0" "./buildResources/setup.iss"
        ```

3. 脚本执行完毕后，生成的 `.exe` 安装包文件位于 `./dist` 目录。
