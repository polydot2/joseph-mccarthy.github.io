---
title: "Health Check Dev Log"
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
        "native" : {
            "minute":0.43,
            "fiveMinutes":0.2,
            "fithteenMinutes":2.3
        },
        "core" : {
            "minute":0.01,
            "five-Minutes":0.01,
            "fithteenMinutes":0.5
        }
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

### 2022/03/03 

So today I have started implementing the agent service using Python and FastApi as it's not going to do anything complicated. However since then I have decided to add an additional two end points which 
will provide some extra operations. First is the __/__ endpoint also known as root. I generally like to provide something here to give some information about the service that they are attempting to 
consume. Not sure about the content at the moment, however it will probably be some sort of descriptive json or even swagger documentation. The next end point I've decided to add is the __/device__ which 
will just return the following at the moment:

```json
{
	"hostname":"name",
	"address":"12.32.123.2",
	"name":"my server",
	"apiVersion": "2.1"
}
```

The reason for this my thinking is that the server might want to go check back every now and then to see if it's changed.
