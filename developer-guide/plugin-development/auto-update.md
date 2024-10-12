---
title: 自动更新
description: 
published: false
date: 2024-10-12T04:32:37.690Z
tags: 开发者
editor: markdown
dateCreated: 2024-07-19T13:59:13.172Z
---

# 自动更新

OpenBlock 的资源框架允许第三方开发者配置指定自己的更新源，来实现资源的自动更新功能。我们可以在官方的资源路径下看到资源的配置文件 `config.json` ，其中的内容如下：

```
{
    "updater": {
        "default": {
            "provider": "github",
            "repo": "openblockcc/external-resources-v3"
        },
        "cn": {
            "provider": "gitee",
            "repo": "openblockcc/external-resources-v3"
        }
    },
    "version": "x.x.x"
}
```

- updater 属性包含了两个对象，其中 `default` 为默认更新源地址， `cn` 则将在用户选择语言为 `简体中文` 时被使用。其中 `default` 为必须项，`cn` 为可选项，如果它不存在时将自动使用 `default` 配置。
- provider 可选值为 `github`，`gitee`。
- repo 为对应的仓库的 `{owner}/{repo}`
- version 为当前版本号。版本号应当遵循 npm 版本号规范，否则程序可能无法正确的比对版本号从而导致出错。

OpenBlock 会通过读取 updater 仓库中的最新的 release 的 tag 将其与本地资源中的 version 比对，以此来确定是否存在更新的版本，如果存在则弹出更新提示。

## 创建 Release

1. 将 `config.json` 文件中的版本号修改为当前版本号

2. 创建新的 tag 并推送，tag 名称应当与版本一致

3. 在资源路径下压缩除 `.git` `.github` `node_modules` `.buildResources` 等无用内容以外的文件，并将压缩包名称命名为 `external-resources-${version}.zip`，注意版本号要与 tag 保持一致，否则会导致程序无法找到有效的资源。

4. 生成 `external-resources-${version}.zip` 的校验和。

{可能还是应当引导用户使用 action}