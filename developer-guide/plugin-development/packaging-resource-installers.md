---
title: 打包发布独立的资源安装包
description: 
published: false
date: 2025-06-03T14:25:47.980Z
tags: 开发者
editor: markdown
dateCreated: 2025-06-03T14:25:10.906Z
---

# 打包发布独立的资源安装包

## 打包指令

- MacOS

    ``` bash
    ./buildResources/build-pkg.sh VERSION="1.0.0"
    ```

- Linux

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