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

&nbsp;
&nbsp;

##### /latest

```json
{
    "download": 3296755.0,
    "upload": 2175216.0,
    "ping": 62.496,
    "time": 1645789388.759391
}
```

&nbsp;
&nbsp;

##### /last-day

```json
{
    "download": {
        "high": 3852744.0,
        "average": 3629769.4166666665,
        "low": 3296755.0
    },
    "upload": {
        "high": 2331189.0,
        "average": 1883408.0416666667,
        "low": 1215527.0
    },
    "ping": {
        "high": 62.496,
        "average": 16.989,
        "low": 12.594
    }
}
```

&nbsp;
&nbsp;

##### /graph

```json
[
    {
        "id": 1,
        "download": 3364494.0,
        "upload": 1085589.0,
        "ping": 15.426,
        "time": 1645710501.983828
    },
    {
        "id": 2,
        "download": 3330109.0,
        "upload": 822428.0,
        "ping": 17.148,
        "time": 1645712303.276396
    },
    {
        "id": 3,
        "download": 3316571.0,
        "upload": 1076903.0,
        "ping": 15.835,
        "time": 1645714140.544144
    },
    {
        "id": 4,
        "download": 3261149.0,
        "upload": 1134400.0,
        "ping": 15.76,
        "time": 1645715986.757451
    }
]
```

&nbsp;
&nbsp;

### Docker

There is also a provided Docker image that runs both the speed test and the api with an exposed port of **5000**

```sh
docker pull joemccarthy/internet-monitor:latest
docker run -d -p 5000:5000 joemccarthy/internet-monitor:latest
```

&nbsp;
&nbsp;

### Technologies

- Python
- Flask
- SqlAlchemy
- Docker
- [Speedtest.net CLI](https://www.speedtest.net/apps/cli)
