---
title: Quick Start
description: 
published: true
date: 2024-10-17T04:16:51.645Z
tags: developer
editor: markdown
dateCreated: 2024-10-17T04:16:51.645Z
---

# Software Development

## Quick Start

### Requirements

Please ensure that your computer has the following software or tools installed:

- Node.js 14/16 (It is recommended to use version 16; using a version that is too high or too low may cause compilation failures in some steps.)
- Python 2.7
- Git
- Node-gyp (Also, install the necessary local compilation tools according to the [node-gyp](https://github.com/nodejs/node-gyp?tab=readme-ov-file#installation) official documentation.)

### Getting the Source Code and Installing Dependencies

1. Clone the core repository of the project.

    ```bash
    mkdir openblock
    cd openblock
    git clone https://github.com/openblockcc/openblock-gui
    git clone https://github.com/openblockcc/openblock-vm
    git clone https://github.com/openblockcc/openblock-blocks
    git clone https://github.com/openblockcc/openblock-link
    git clone https://github.com/openblockcc/openblock-resource
    ```

2. Install dependencies and link them.

    ```bash
    cd openblock-blocks
    npm install
    npm link
    cd ..
    cd openblock-vm
    npm install
    npm link
    cd ..
    cd openblock-gui
    npm install
    npm link openblock-blocks openblock-vm
    cd ..
    ```

The `npm link` command replaces the default packages in the project with local `npm` packages, allowing the modifications you make in packages like `openblock-blocks` to be used by `openblock-gui`. Otherwise, it will default to using the content downloaded from the npm server. You can verify the success of the linking by checking the `openblock-gui/node_modules` folder for the `openblock-blocks` and `openblock-vm` directories; if linked successfully, they will be linked to the project location.

### Running

1. Start the hardware interface server `openblock-link`.

```bash
cd openblock-link
npm start
```

2. Start the external resources server `openblock-resource`.

Execute this in a new terminal.

```bash
cd openblock-resource
npm start
```

3. Start `openblock-gui`.

Execute this in a new terminal.

```bash
cd openblock-gui
npm run start
```

After the webpack build of `openblock-gui` is completed, a webpage for `openblock-gui` will pop up. Of course, you can also access it by manually entering the address `http://127.0.0.1:8601/`.

> Webpack will continue to listen for changes in the source code within the project, including the code linked to local packages. This means that after modifying the code in `openblock-gui` or `openblock-vm`, you only need to save the file to trigger a webpack update and compile. This process takes much less time than restarting the webpack compilation and allows for convenient code debugging.
{.is-info}

> However, for `openblock-blocks`, due to its special compilation mode (using google-closure-compiler for compilation), after modifying its internal code, we need to execute `npm run prepublish` to recompile the code and also restart the webpack server of the GUI to make the changes effective.
{.is-warning}
