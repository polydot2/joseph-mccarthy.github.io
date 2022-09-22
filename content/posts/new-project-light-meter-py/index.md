---
title: "New Project Light Meter Py"
date: 2022-09-22T21:45:03+01:00
draft: false
sidebar: true
tags: [Python, Project, Night Sky Pi, Light Meter Py]
hero: "hero.png"
summary: "Have started a new project to support Night Sky Pi"
---

While working on the [__Night Sky Pi__]({{< ref "/devlogs/night-sky-pi" >}}) project ran into an issue. The issue was with the exposure value of the images taken with the __Pi HQ__ camera. I started playing around and found that I would have to compensate the image exposure from one image to another. I got a rustic solution working, however it was causing the exposure to bounce around the place between frames and wasn't consistant. Finding that this problem was larger than I though and would make more sense as an indepenant module I created a new [__GitHub__](https://github.com/joseph-mccarthy/lightmeter-py) Repository, hoping that this would make solving the issue much simplier.

The principle of the module is to behave similar to a light meter that's built into cameras. The main purpose is to examine areas of an image with an known exposure, the calculate the new exposure to bring the image to the best suitable exposure for the image. There are many ways to exposure an image, the first increment of the lightmeter module is to either examine the entire frame known as either [__Evaluative or Average Metering__](https://en.wikipedia.org/wiki/Metering_mode#Average_metering), which isn't great as this can cause the exposure to be inconsistant but for simplicity it's there. However I'm also going to implement spot metering, first spot metering in the center of the frame. As with all my projects recently you can also follow the progress here on it's [__developer log__]({{< ref "/devlogs/lightmeter-py" >}}).
 