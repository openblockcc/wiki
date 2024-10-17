---
title: Building OpenBlock Desktop
description: 
published: true
date: 2024-10-17T04:20:33.770Z
tags: devedeve
editor: markdown
dateCreated: 2024-10-17T04:20:33.770Z
---

# Building OpenBlock Desktop

## Preparation

1. First, obtain the source code for the desktop version.

```bash
git clone https://github.com/openblockcc/openblock-desktop
cd openblock-desktop
```

2. Install the dependencies.

```bash
npm ci
```

## Running and Debugging

Compile the code and start.

```bash
cd openblock-desktop
npm run compile
npm run start
```

After Electron starts, you can use the following shortcuts to open the web console.

### Tab {.tabset}

#### Windows/Linux

<kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>i</kbd>

#### MacOS

<kbd>Command</kbd> + <kbd>Option</kbd> + <kbd>i</kbd>

### Tab {.tabset}

## Using Local Dependencies

1. Switch to the `openblock-gui` branch and link to the local dependencies.

Note that when packaging the desktop version, we need to switch `openblock-gui` to the `desktop` branch. This branch has some adjustments related to handling static images and other content compared to the `main` branch, to accommodate local execution. If you have made changes in the `develop` branch before this, don't worry; use the `git commit` command to submit those changes, and then merge them after switching to the `desktop` branch using the `git merge` command.

```bash
git checkout desktop
npm link openblock-blocks openblock-vm
npm link
```

2. Link `openblock-gui` in `openblock-desktop`.

```bash
npm link openblock-gui
```

Similarly, if you have other local packages, you can link them in this way.

## Packaging

```bash
npm run dist
```

Once the packaging is complete, you can find the packaged software in the `dist` folder.

> If you need to package different system versions (e.g., MacOS, Linux), just execute the packaging command in the respective system.
{.is-info}
