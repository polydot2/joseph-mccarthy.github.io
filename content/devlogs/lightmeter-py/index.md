---
title: "Lightmeter Py"
date: 2022-09-20T18:55:03+01:00
draft: false
sidebar: true
tags: [Paython, OpenCV, Numpy, Light Meter Py]
hero: "hero.png"
summary: "Reads an image behave as a light meter and recommend an exposure."
---

<div class="text-center m-2">

  [![GitHub Workflow Status](https://img.shields.io/github/workflow/status/joseph-mccarthy/lightmeter-py/Build?style=for-the-badge)](https://github.com/joseph-mccarthy/lightmeter-py/actions/workflows/python-app.yml)
  [![Codecov](https://img.shields.io/codecov/c/gh/joseph-mccarthy/lightmeter-py?style=for-the-badge)](https://app.codecov.io/gh/joseph-mccarthy/lightmeter-py)
  [![Sonar Quality Gate](https://img.shields.io/sonar/quality_gate/joseph-mccarthy_lightmeter-py/main?server=https%3A%2F%2Fsonarcloud.io&style=for-the-badge)](https://sonarcloud.io/project/overview?id=joseph-mccarthy_lightmeter-py)
  [![GitHub](https://img.shields.io/github/license/joseph-mccarthy/lightmeter-py?style=for-the-badge)](https://github.com/joseph-mccarthy/lightmeter-py/blob/main/licence)
  [![wakatime](https://wakatime.com/badge/github/joseph-mccarthy/lightmeter-py.svg?style=for-the-badge)](https://wakatime.com/badge/github/joseph-mccarthy/lightmeter-py)

</div>

While working on the [__Night Sky Pi__]({{< ref "/devlogs/night-sky-pi" >}}) project ran into an issue. The issue was with the exposure value of the images taken with the __Pi HQ__ camera. I started playing around and found that I would have to compensate the image exposure from one image to another. I got a rustic solution working, however it was causing the exposure to bounce around the place between frames and wasn't consistant. Finding that this problem was larger than I though and would make more sense as an indepenant module I created a new [__GitHub__](https://github.com/joseph-mccarthy/lightmeter-py) Repository, hoping that this would make solving the issue much simplier.

## Overview

The principle of the module is to behave similar to a light meter that's built into cameras. The main purpose is to examine areas of an image with an known exposure, the calculate the new exposure to bring the image to the best suitable exposure for the image. There are many ways to exposure an image, the first increment of the lightmeter module is to either examine the entire frame known as either [__Evaluative or Average Metering__](https://en.wikipedia.org/wiki/Metering_mode#Average_metering), which isn't great as this can cause the exposure to be inconsistant but for simplicity it's there. However I'm also going to implement spot metering, first spot metering in the center of the frame.s

## Metering Modes

Each of the exposure modes cover different areas of the view in order to evaluate the exposure, this is a simple approach there's more to it than that but I will go into futer detail later. Here are the metering modes that I intend to support.

* Spot Metering *(5% coverage)*
* Partial Metering *(15% coverage)*
* Centre Weighted Metering *(75% coverage)*
* Matric Metering *(Determined by desired metering points - generally 75%-100%)*
* Evaluative Metering *(100% coverage)*
* Highlight Meetering *(No Coverage, exposure is based purely on the lightest parts of the image)*

The first task I have for this project is to determine all the zones for a given image and it's metering method, and from the above list, this might take a little while to get going. However seems it's going to be a fun project, and will greatly help the [__Night Sky Pi__]({{< ref "/devlogs/night-sky-pi" >}}) Project. Also after a little while of searching I couldn't find a Python library to do this, so maybe it will help someone else as well.
