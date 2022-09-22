---
title: "Night Sky Pi Devlog"
date: 2022-03-28T22:47:03+01:00
draft: false
sidebar: true
tags: [Project, Developer Log,Raspberry Pi]
hero: "hero.png"
summary: "Developer Log for Night Sky Pi Project with rolling updates."
images: "hero.png"
---
<div class="text-center m-2">

  [![GitHub Workflow Status](https://img.shields.io/github/workflow/status/joseph-mccarthy/night-sky-pi/Build?style=for-the-badge)](https://github.com/joseph-mccarthy/night-sky-pi/actions/workflows/python-app.yml)
  [![Codecov](https://img.shields.io/codecov/c/gh/joseph-mccarthy/night-sky-pi?style=for-the-badge)](https://app.codecov.io/gh/joseph-mccarthy/night-sky-pi)
  [![Sonar Quality Gate](https://img.shields.io/sonar/quality_gate/joseph-mccarthy_night-sky-pi/main?server=https%3A%2F%2Fsonarcloud.io&style=for-the-badge)](https://sonarcloud.io/project/overview?id=joseph-mccarthy_night-sky-pi)
  [![GitHub](https://img.shields.io/github/license/joseph-mccarthy/night-sky-pi?style=for-the-badge)](https://github.com/joseph-mccarthy/night-sky-pi/blob/main/licence)
  [![wakatime](https://wakatime.com/badge/github/joseph-mccarthy/night-sky-pi.svg?style=for-the-badge)](https://wakatime.com/badge/github/joseph-mccarthy/night-sky-pi)

</div>

So I now have myself a Raspberry Zero 2W. This means I can now begin a project that I have been holding off for a while, which is my night sky pi. The princple of the project is rather straight forward I want a device that I can place outside which will just look up.

During the night it will record the sky not sure if it's going to be pictures or video. Then during the day it will process those images or video to try and detect and meteors or other objects. I'm expecting a lot of planes while I tweak the code.

I'm trying to make it as lightweight as possible due to the hardware, so only time will tell if I'll be able to process the images on this device or if they will have to be offloaded to another device for processing. You can find the source code on [__GitHub__](https://github.com/joseph-mccarthy/night-sky-pi)

----

## 28/03/2022

So making a start on the project like all the others start with an empty repository. Have decided to write this with Python because it's lightweight for the hardware, and there is a standard library for the Pi camera, which I still need to look into.

But before any code can be written I needed to build the pi and load an OS. This was simple, just standard 32bit lite OS, and the Zero snapped into it's case with the camera hole nicely aligned after changing the ribbon cable for the shorter version which came with the case. Once that was completed it was time to boot it up and give it the general once over and update everything.

I also took this time to update the version of python installed to 3.10.3 which I'll be using the application. Another thing was installing git, because this will allow me to quickly pull changes down to the device for testing. Once the application is completed I'll be researching a more formal way to distribute it.

Now for some development, first thing first is setting up the readme file, then the requirements.txt. Then the creating of the main module entry point. Simple enough. So there are a few things I need to do, which I'm going to call the loop! This loop will get the current datetime, then for a given date, along with a coordinate it will then get the sunrise and sunset. This is to work out where we are in the cycle. So do we need to capture images or process images and wait for sunset. There is a an edge case to this which is the current datetime could be the next day, however we are still in the preious night. For example, it could be 2am which is before sunrise and sunset for that given datetime, however really we are on the pervious cycle.

So we need to check the datetime being after the sunset and before the next day sunrise. If this is the case then we capture images, however we also need to check if this false, then check if the datetime is between yesterday sunset and todays sunrise, which would be true if the time was past 00:00. If neither of the above are true, then it can be certain that we are between the sunrise and sunset of the current datetime, and we should either be processing images or waiting for sunset.

----

## 29/03/2022

Today has been a rather productive day in my eyes. I haven't done much code, but spent some time doing all the admin stuff around the project. So the progress today has been setting up a unit test, which at the moment tests nothing. But this test was needed to set up a github action to build the code base and run tests.

The next step was to set up codecov and sonar cloud for the project, then modify the action to provide code coverage, which at this point is zero, and also send violations and quality metrics to sonar cloud.

With these completed I was then able to do the all important adding of badges to the readme file. So now at a glace I can see the build, coverage, quality gate and the important licence information MIT what else.

Aswell as some of the admin and code quality work I did manage to get some coding done. I created some functions for dates, rather simple, just getting today, previous and next. This are simple to do inline, however it's just my preference to split these out into methods and place them in a module. The next thing I done was create a module to get sunrise and sunset data. I found a great module to do this for me called __suntime__.

<script src="https://gist.github.com/joseph-mccarthy/513a0b2dbf7c10ec9bd56615162f06d6.js?file=sunrise.py"></script>

All it requires is the latitude, longitude and a datetime, then it's able to return the datetime of the sunrise and sunset. I was thinking of using a rest api to get this information for me, however this is a nicer solution in my eyes. So I imported this module and wrapped it within my own sun module. The only modification I done to the datetime returned is to remove the timezone information as this is something I'm not interested in and allows me to compare the datetimes returned here with those from my datetime functions.

Lastly I adding some command line arguements to the program so I was able to provide information here rather than looking into configuration files at the moment.

<script src="https://gist.github.com/joseph-mccarthy/513a0b2dbf7c10ec9bd56615162f06d6.js?file=arg-parse.py"></script>

The arguements being passed is the latitude and longitude of the camera, which are required for this program to execute. Then an optional debug level, which defaults to __WARNING__, this just allows me to quickly debug the application while I develop it.

----

## 30/03/2022

So today I didn't do much in features or extending the code base to the end goal, as I was playing clean up on my previous cowboy work. So tonight I spent the evening unit testing the functions that I have already written which isn't great, I should have written the tests first, and saved the time. I was also distracted because I wrote a post about [__GitHub Sponsers__]({{< ref "/posts/github-sponsers" >}}), which in my opinion is a great way to support open source. So carrying on with the unit testing of what I had previously done, I'm now up to __53%__ coverage, which is not a bad start.

For the testing of the time_functions I had to do a little bit of refactoring as I wasn't able to mock the datetime module. So I have added ___get_now()__ which only returns the current datetime.

<script src="https://gist.github.com/joseph-mccarthy/513a0b2dbf7c10ec9bd56615162f06d6.js?file=now.py"></script>

This allowed me to write predictable unit tests for my time_functions as I was able to mock out this method within my module. As this method calls upon the core python library of datetime, there is really no need to test it. With this being mocked I was able to test the other methods within the module to ensure expected results.

### Refactoring

I also took the opertunity once I had some unit tests to do a little bit of refactoring. Previously I had many little variables laying around and methods that took a few arguements. So what I have done is created some dataclasses, to encapsulate the core concepts of the application data.

<script src="https://gist.github.com/joseph-mccarthy/513a0b2dbf7c10ec9bd56615162f06d6.js?file=dataclasses.py"></script>

Once we have decided what the observation date is for the capture run in the evening, we can create the Observation object. This contains all the data that's needed for the rest of the run and the capturing of images for the time being. It contains a SunData object, that just has the boundaries of the capture, being the sunset from and the run till sunrise (these are also different dates). Then there is the location information, where latitude and longitude have just been wrapped for easy reference.

----

## 24/05/2022

So I have taken a break from my projects recently due to family holidays, events and the car failing on us, so have been sorting that out. That being said I'm starting to work on this again, I have decided to set a series of milestones for the project in order to simplify the development and not get dishearted at the possible lack of progress. You'll be able to see these milestones in GitHub, but I'll summerise them here.

- Caputre images at night, then create a time lapse
- Add information to the images during the timelapse
  - Time stamp information
  - Weather data
  - Other Sensor information
- Ability to completed timelapses to remote location
  - ftp
  - youtube
- Streak Detection
  - Notification of Streak
- Monitoring
  - Software Monitioring endpoint
  - Auto Delete Tidy Up
- Image masking
  - Mask areas of the image to help with Streak Detection to avoid false posisitives
- Calculation of area of sky covered by camera
  - Show this coverage on a map
- Ability to connect to a flight scanner to monitor aircraft to negate this from streak detection

As you can see this is going to be a long term project for myself, and any help would be awesome.

----

## 15/09/2022

So another period of absence working on this project. Seems to be a theme here. However, progress has been made. Night Sky Pi, now takes images throughout the night, dusk till dawn for the location and timezone that you have entered. Once the the capture of the stills has been carried out, while waiting for the next sunset to resume capture the application will scan it's data directories for missing timelapses. When a missing timelapse has been determined then a timelapse will be generated for the date using the captured stills. 

As well as some active development on the application I have bene trying to use GitHub issues to track what I've been doing as my memory isn't great. Also I think that it keeps me focused as anyone who knows me, can confim I'm easily distracted.

----

## 16/09/2022

So after some refactoring to create a camera instance at application start up and pass that into the loop that takes all the stills during the night, was woke up to some success. The camera didn't crash, and was rewarded with stills throughout the night and a generated time lapse. Below is the output I've uploaded to youtube. Now I need to continue with the tidy up.

{{< youtube L86OlopdCoQ >}}

----

## 19/09/2022

There has been some exciting progress since the time lapse a few days ago. I had a trip to the Cambridge [__Raspberry Pi Shop__]({{< ref "/posts/pi-shopping" >}}) and purchased a Raspberry Pi 4. The intention of this device is to connect it to the Raspberry Pi HQ Camera Module and this be the test hardware I use for this project going forward.

This comes with some extra challenges that I haven't had to face yet, however knew were coming. Currently the project has been using a web camera, which is configured by the camera id, linking to the usb video id within the OS. But the Pi Camera, uses the CSI interface, and has far more options that the web camera was able to provide. For example with the web camera I was using OpenCV-Python to capture the frame, this gave me no control over the exposure of the image, as it was basically a frame from a video feed. 

Now the Pi HQ camera uses [__libcamera__](https://www.libcamera.org/) on bullseye. This means that I have to call an external command line to capture an image, as there isn't a python wrapper for it at the moment, however you can follow beta the progress [__here on GitHub__](https://github.com/raspberrypi/picamera2). Once this is release I will be refactoring the application to use that, as it will probably be simplier going forward. 

Now that I can control exposure this raises another issue, I have to determine if an image is correctly exposed. This raises many questions as there are a few ways to measure exposure, I could do an entire post on it which I think I will at some point. However I have got a rough, hacky process in place while I iron out the details.

So when starting up Night Sky Pi, the camera id can be set to -1, to indicate that we want to use the CSI camera interface. This is due to zero or more being valid usb device identifiers. Using -1 will create a new camera instance, and therefore use [__libcamera__](https://www.libcamera.org/)  to capture images. Once an image has been captured, the I use numpy to determine the entire average light value after converting to grayscale. If the returned value is in the range 110-135 then this is considered acceptable and no alterations are done to the exposure value of the next image.

This has worked in principle, but it's rather rough around the edges causing the exposure to jump around between frames. Also this is taking the entire frame into account, which I believe is the reason for the jumps. I need to adapt this to either use [__spot metering__](https://en.wikipedia.org/wiki/Metering_mode#Spot_metering) or [__center weighted__](https://en.wikipedia.org/wiki/Metering_mode#Center-weighted_average_metering) which is a more reasonible approach to image exposure. However that's for another udate.

## 22/09/2022

Following the issues that I had on the __19/09/2022__ I've started another project in an attempt to resolve it. It's a python module that emulates the behavour of a camera light meter. I've created the repository on [__GitHub__](https://github.com/joseph-mccarthy/lightmeter-py) and have also created a [__developer log__]({{< ref "/devlogs/lightmeter-py" >}}) to track and discuss it's progress and details.
