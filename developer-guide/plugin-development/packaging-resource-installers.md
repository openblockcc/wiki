---
title: 打包发布独立的资源安装包
description: 
published: false
date: 2025-06-07T09:42:19.251Z
tags: 开发者
editor: markdown
dateCreated: 2025-06-03T14:25:10.906Z
---

# 打包发布独立的资源安装包

## 软件打包说明

- MacOS

    1. 在项目根目录打开终端，运行打包脚本：

        注意修改使用你实际的版本号。
        ``` bash
        ./buildResources/build-pkg.sh VERSION="1.0.0"
        ```

    2. 脚本执行完毕后，生成的 `.pkg` 安装包文件位于 `./dist` 目录。

- Linux

    1. 首先需要安装有 `dpkg-deb` 工具，如果未安装，请运行：

        ``` bash
        sudo apt install -y dpkg-deb
        ```

    2. 在项目根目录打开终端，运行打包脚本：

        注意修改使用你实际的版本号
        ``` bash
        ./buildResources/build-deb.sh -v"1.0.0"
        ```
        注意修改使用你实际的版本号。

    3. 脚本执行完毕后，生成的 `.deb` 安装包文件位于 `./dist` 目录。

- Windows

    1. 首先需要安装有 [Inno Setup](https://jrsoftware.org/isinfo.php)，如果你需要保存对win7系统的兼容性，推荐下载v5.x.x 的版本。
    
    2. 在项目根目录打开终端，运行打包脚本：

        注意修改使用你实际的版本号，并将路径修改为你真实的 Inno Setup 安装路径。
        ``` bat
        "C:\Program Files (x86)\Inno Setup 5\ISCC.exe" /dVersion="1.0.0" "./buildResources/setup.iss"
        ```

    3. 脚本执行完毕后，生成的 `.exe` 安装包文件位于 `./dist` 目录。
