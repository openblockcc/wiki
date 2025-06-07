---
title: 打包发布独立的资源安装包
description: 
published: false
date: 2025-06-07T04:50:56.000Z
tags: 开发者
editor: markdown
dateCreated: 2025-06-03T14:25:10.906Z
---

# 打包发布独立的资源安装包

## 软件打包说明

- MacOS

    1. 打开终端，进入项目根目录，运行打包脚本，指定版本号：

        ``` bash
        ./buildResources/build-pkg.sh VERSION="1.0.0"
        ```

    3.脚本执行完毕后，生成的 .pkg 安装包文件位于 ./dist 目录。

- Linux

    1. 首先需要安装有 dpkg-deb 工具，如果未安装，请运行：

        ``` bash
        sudo apt install -y dpkg-deb
        ```
    2. 
已安装 dpkg-deb 工具。

如果未安装，请运行：

bash
复制
编辑
sudo apt install -y dpkg-deb

    You need to Run `sudo apt install -y dpkg-deb` to install `dpkg-deb` first.

    ``` bash
    ./buildResources/build-deb.sh -v"1.0.0"
    ```

- Windows

    You need to install [Inno Setup](https://jrsoftware.org/isinfo.php) first
    Note that you should use cmd to run instead of powershell.

    - Use CMD

        ``` bat
        "C:\Program Files (x86)\Inno Setup 6\ISCC.exe" /dVersion="1.0.0" "./buildResources/setup.iss"
        ```

    - Or Powershell

        ``` powershell
        & "C:\Program Files (x86)\Inno Setup 6\ISCC.exe" /dVersion="1.0.0" "./buildResources/setup.iss"
        ```