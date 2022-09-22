---
title: "Internet Monitor"
date: 2022-02-20T22:39:27Z
draft: false
sidebar: false
tags: [Infrastructure,Python,Flask,Docker,SqlAlchemy]
hero: "hero.png"
summary: Small and simple application to keep my ISP honest.
images: "hero.png"

---
<div class="text-center m-2">

[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/joseph-mccarthy/internet-monitor?color=green&style=for-the-badge)](https://github.com/joseph-mccarthy/internet-monitor/releases/latest)
[![GitHub](https://img.shields.io/github/license/joseph-mccarthy/internet-monitor?style=for-the-badge)](https://github.com/joseph-mccarthy/internet-monitor/blob/main/LICENCE)
[![Sonar Quality Gate](https://img.shields.io/sonar/quality_gate/joseph-mccarthy_internet-monitor?server=https%3A%2F%2Fsonarcloud.io&style=for-the-badge)](https://sonarcloud.io/project/overview?id=joseph-mccarthy_internet-monitor)
[![wakatime](https://wakatime.com/badge/github/joseph-mccarthy/internet-monitor.svg?style=for-the-badge)](https://wakatime.com/badge/github/joseph-mccarthy/internet-monitor)


</div>

I rather like the idea of keeping my Internet Service Provider honest with the service that they claim to be providing me. They charge enough for the service and it's not always apprant that we're getting it. So I created this project for my own need. It's been published to [GitHub.](https://github.com/joseph-mccarthy/internet-monitor) I'm very pleased that I was able to finall finished something, I also have a little post in my blog about the project [Blog]({{< ref "/posts/first-completed-project" >}} "Internet Monitor Done").

I basically wanted a speed test of my internet connection to run every 30 minutes and have that information stored so I can query it later and possibly see when there are times that speeds flucate. This information would probably be useful when I start pumping data to sync storage servers.

I know that there are many solutions out there that can provide this information, and can create dashboards. But I didn't want the restrictions of having to use those front ends or dashboards. So I decided that it would be made of two parts.

The fist part is just a simple python script that runs every 30 minutes that calls upon the [speed test cli](https://www.speedtest.net/apps/cli) to perform the speed test and then persist that in a sqlite database. The second component is the webservice that I can call on to get the results and other data. This again was written in python using flask.

The API exposes three endpoints for the data saved in the database

##### /latest

<script src="https://gist.github.com/joseph-mccarthy/7082da93374f60361883238134490676.js?file=latest.json"></script>


##### /last-day


<script src="https://gist.github.com/joseph-mccarthy/7082da93374f60361883238134490676.js?file=last-day.json"></script>

##### /graph


<script src="https://gist.github.com/joseph-mccarthy/7082da93374f60361883238134490676.js?file=graph.json"></script>

&nbsp;
&nbsp;

### Docker

There is also a provided Docker image that runs both the speed test and the api with an exposed port of **5000**

<script src="https://gist.github.com/joseph-mccarthy/7082da93374f60361883238134490676.js?file=run.sh"></script>

&nbsp;
&nbsp;

### Technologies

- Python
- Flask
- SqlAlchemy
- Docker
- [Speedtest.net CLI](https://www.speedtest.net/apps/cli)
