---
title: Create Standard Resource Images
description: 
published: true
date: 2024-10-17T04:37:32.373Z
tags: developer
editor: markdown
dateCreated: 2024-10-17T04:37:32.373Z
---

# Creating Standard Resource Images

All official resource images in OpenBlock follow a unified standard to ensure consistency across interface elements.

## Creating the Main Resource Image (iconURL)

This image is displayed in the device or extension selection interface. The standard image parameters are as follows:

- **iconURL**
  - Standard name: [Device ID]
  - Format: png
  - Resolution: 600x372
  - Background color: white

There should be a specified margin around the image. You can download the image below and modify it. Scale the content proportionally, center it, and try to fill the green area in the middle. Then, replace the background color with white.

- [standardimage.png](/developer-guide/plugin-development/create-standard-resource-images/standardpimage.png)

![standardimage.png](/developer-guide/plugin-development/create-standard-resource-images/standardimage.png)

For example, the image below (the gray border is for illustration only and does not appear in the actual image).

![standardimagedemo.png](/developer-guide/plugin-development/create-standard-resource-images/standardimagedemo.png)

## Creating the connectionIconURL and connectionSmallIconURL

These images are displayed in the interface during device connection. The parameters for the two images are as follows:

- **connectionIconURL**
  - Standard name: [Device ID]-illustration
  - Format: svg
  - Default size: 108x87

- **connectionSmallIconURL**
  - Standard name: [Device ID]-small
  - Format: svg
  - Default size: 40x40

To create these two `svg` images, start by preparing a device image with the background removed. Resize it to `108x87px`, center the control board, and scale the image proportionally to fill the space as much as possible. Save it as a transparent background `png`. Then, resize the image to `40x40px`, repeat the process, and save it as a new `png`.

The results are as follows:

- [standarddeviceimagedemo108x87.png](/developer-guide/plugin-development/create-standard-resource-images/standarddeviceimagedemo108x87.png)

![standarddeviceimagedemo108x87.png](/developer-guide/plugin-development/create-standard-resource-images/standarddeviceimagedemo108x87.png)

- [standarddeviceimagedemo40x40.png](/developer-guide/plugin-development/create-standard-resource-images/standarddeviceimagedemo40x40.png)

![standarddeviceimagedemo40x40.png](/developer-guide/plugin-development/create-standard-resource-images/standarddeviceimagedemo40x40.png)

Finally, visit the online format conversion website [https://www.aconvert.com/image/](https://www.aconvert.com/image/), upload the two images, and convert them to **SVG** format. In the **Resize image** option, select **Change width and height**, and set the dimensions to `108x87` and `40x40` respectively. Once converted, right-click the **OUTPUT FILE** and select **Save link as...**. Rename the `108x87` image as `[Device ID]-illustration` and the `40x40` image as `[Device ID]-small`.

The specific files are as follows:

- [standarddeviceimagedemo-illustration.svg](/developer-guide/plugin-development/create-standard-resource-images/standarddeviceimagedemo-illustration.svg)

![standarddeviceimagedemo-illustration.svg](/developer-guide/plugin-development/create-standard-resource-images/standarddeviceimagedemo-illustration.svg)

- [standarddeviceimagedemo-small.svg](/developer-guide/plugin-development/create-standard-resource-images/standarddeviceimagedemo-small.svg)

![standarddeviceimagedemo-small.svg](/developer-guide/plugin-development/create-standard-resource-images/standarddeviceimagedemo-small.svg)

> The SVG images generated this way are technically SVG files containing embedded PNG images, not true vector graphics. However, this method is sufficient for this purpose. You can also use professional vector editing software to create them.
{.is-info}
