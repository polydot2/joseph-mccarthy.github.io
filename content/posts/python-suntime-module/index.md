---
title: "Python Suntime Module"
date: 2022-03-30T22:45:56+01:00
draft: false
sidebar: true
tags: [Python,Module]
hero: "hero.png"
summary: "Module to calculate Sunrises and Sunsets for a given location a date."
images: "hero.png"
---

So while working on the [__Night Sky Pi__](https://github.com/joseph-mccarthy/night-sky-pi) I needed a way to get the sunrise and sunset for dates. Firstly I thought I should use a webservice, however I really didn't like the fact of making more rest calls than I really needed to. Also there could be a possibiliy that device might run somewhere without a connection or reliable one at that. So I had to look elsewhere. This is when I came across the suntime python module on [pypi](https://pypi.org/project/suntime/).

The module is really simple and clean to use. The only requirement in order to use the module is to create an instance of the Sun class passing in the latitude and longitude that you want the sunrise and sunset information from.

<script src="https://gist.github.com/joseph-mccarthy/acd300383c255e68b026d3e70869aea7.js?file=sun.py"></script>

Above is the most simple usecase for the module, just getting the sunrise and sunset for today. If no date is passed in then todays date is defaulted. When calling this method it will return the datetime of both the sunrise and sunset as UTC rather than local time. Obviously if you pass a datetime into the methods it will return you the sunrise and sunset for that date.

If you would rather have the datetimes of the sunrise and sunset returned in localtime, then there are specific methods for that, below is an example of doing so.

<script src="https://gist.github.com/joseph-mccarthy/acd300383c255e68b026d3e70869aea7.js?file=sun-date.py"></script>
