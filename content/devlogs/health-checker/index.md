---
title: "Health Checker Dev Log"
date: 2022-03-01T21:07:27Z
draft: false
sidebar: true
tags: [Python,Docker,Health Check,Project, Developer Log]
hero: "hero.png"
summary: "On going Developer Log for the Health Check Project"
---

## Problem Statement

So the premise of this project is to prepair in advance the growing of my internal services and infrastructure. Of which most will be Raspberry Pis when they are finally in stock.

So I want to be able to deploy a little service on the device that on first run will attempt to contact a server to provide information about the host device. This could be simple information such as it's host name and ip address for the time being. The server will persist this information locally in a database for future use.

The small service deployed to the device will have single endpoint at the moment that I can think off which will be __/health__. This endpoint will provide information back to the caller about the current state of the device in question. First thought about the data to be returned could be as follows.

```json
{
    "load":{
        "minute":0.43,
        "five-minutes":0.2,
        "fithteen-minutes":2.3
    },
    "memory":{
        "total": 4294967296,
        "allocated": 1073741824,
        "free": 3221225472,
        "used":"75%"  
    },
    "storage":{
        "total": 4294967296,
        "allocated": 1073741824,
        "free": 3221225472,
        "used":"75%"  
    },
    "uptime":{
        "since":{
             "time":1279871239812323,
             "pretty": "22/02/2022T13:13:32"
        },
        "duration":{
            "seconds": 121278912398712,
            "pretty": "5 days, 3 hours, 5 minutes and 43 seconds"
        }
    },
    "temperature": [
        "zone":{
            "zone": 0,
            "celsius": 84,
            "fahrenheit": 183.2
        }
    ]
}
```
