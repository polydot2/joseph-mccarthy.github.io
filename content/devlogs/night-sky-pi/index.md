---
title: "Night Sky Pi Devlog"
date: 2022-03-28T22:47:03+01:00
draft: false
sidebar: true
tags: [Project, Developer Log,Rasberry Pi]
hero: "hero.png"
summary: "Developer Log for Night Sky Pi Project with rolling updates."
images: "hero.png"
---
  ![GitHub Workflow Status](https://img.shields.io/github/workflow/status/joseph-mccarthy/night-sky-pi/Build?style=for-the-badge)
  ![Codecov](https://img.shields.io/codecov/c/gh/joseph-mccarthy/night-sky-pi?style=for-the-badge)
  ![Sonar Quality Gate](https://img.shields.io/sonar/quality_gate/joseph-mccarthy_night-sky-pi/main?server=https%3A%2F%2Fsonarcloud.io&style=for-the-badge)
  ![GitHub](https://img.shields.io/github/license/joseph-mccarthy/night-sky-pi?style=for-the-badge)
  ![wakatime](https://wakatime.com/badge/github/joseph-mccarthy/night-sky-pi.svg?style=for-the-badge)

So I now have myself a Raspberry Zero 2W. This means I can now begin a project that I have been holding off for a while, which is my night sky pi. The princple of the project is rather straight forward I want a device that I can place outside which will just look up.

During the night it will record the sky not sure if it's going to be pictures or video. Then during the day it will process those images or video to try and detect and meteors or other objects. I'm expecting a lot of planes while I tweak the code.

I'm trying to make it as lightweight as possible due to the hardware, so only time will tell if I'll be able to process the images on this device or if they will have to be offloaded to another device for processing. You can find the source code on [GitHub](https://github.com/joseph-mccarthy/night-sky-pi)

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

```python
def get_rise_and_set(date: datetime, coorindates: tuple()) -> tuple():
    latitude, longitude = coorindates
    sun = Sun(latitude, longitude)
    sr = sun.get_sunrise_time(date).replace(tzinfo=None)
    ss = sun.get_sunset_time(date).replace(tzinfo=None)
    return (sr, ss)
```

All it requires is the latitude, longitude and a datetime, then it's able to return the datetime of the sunrise and sunset. I was thinking of using a rest api to get this information for me, however this is a nicer solution in my eyes. So I imported this module and wrapped it within my own sun module. The only modification I done to the datetime returned is to remove the timezone information as this is something I'm not interested in and allows me to compare the datetimes returned here with those from my datetime functions.

Lastly I adding some command line arguements to the program so I was able to provide information here rather than looking into configuration files at the moment.

```python
parser = argparse.ArgumentParser()
parser.add_argument("--lat",type=float,required=True,help="Latitude")
parser.add_argument("--lon",type=float,required=True,help="Longitude")
parser.add_argument("--log",type=str,help="Level",default=logging.WARNING)
args = parser.parse_args()
```

The arguements being passed is the latitude and longitude of the camera, which are required for this program to execute. Then an optional debug level, which defaults to __WARNING__, this just allows me to quickly debug the application while I develop it.

----