---
title: "Night Sky Pi First Timelapse"
date: 2022-09-16T13:08:22+01:00
draft: false
sidebar: true
tags: [Night Sky Pi, Project, Python, Raspberry Pi]
hero: "hero.png"
summary: "The first generated timelapse for the night sky pi, but not using a Rasberry Pi"
---

Another period of absence working on this project. Seems to be a theme here. However, progress has been made. Night Sky Pi, now takes images throughout the night, dusk till dawn for the location and timezone that you have entered. Once the the capture of the stills has been carried out, while waiting for the next sunset to resume capture the application will scan it's data directories for missing timelapses. When a missing timelapse has been determined then a timelapse will be generated for the date using the captured stills. 

So after some refactoring to create a camera instance at application start up and pass that into the loop that takes all the stills during the night, was woke up to some success. The camera didn't crash, and was rewarded with stills throughout the night and a generated time lapse. Below is the output I've uploaded to youtube. Now I need to continue with the tidy up. 
&nbsp;

{{< youtube L86OlopdCoQ >}}
&nbsp;

I also need to get some new hardware as this project is currently only using a webcam, which is controlled by opencv. The plan is to get a new Rasberry Pi, a HQ camera module. Then this will allow me to use libcamera, giving me much more control over the exposure and longer exposures something that web cameras can't really support. However I will be keeping the possibility to use a webcam incase someone can't source a CSI-2 camera and will perform some activity.

As well as some active development on the application I have bene trying to use GitHub issues to track what I've been doing as my memory isn't great. Also I think that it keeps me focused as anyone who knows me, can confim I'm easily distracted. I'm trying to make it as lightweight as possible due to the hardware, so only time will tell if I'll be able to process the images on this device or if they will have to be offloaded to another device for processing. You can find the source code on [GitHub](https://github.com/joseph-mccarthy/night-sky-pi)
