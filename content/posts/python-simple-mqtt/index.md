---
title: "Python Simple MQTT"
date: 2022-10-02T23:38:02+01:00
draft: false
sidebar: true
tags: [Python,Module,MQTT]
hero: "hero.png"
summary: "A simple example of MQTT using Python"
---
I'm starting to use Raspberry Pi for a lot of simple tasks around the home and give me notfications. So I thought it was about time to look into message brokers and MQTT is the way to go. So instead of just throwing the implmentation into a project of mine. I thought it would be more useful to create a seriously simple example project that just publishes a random number to a topic and another that subscribes to it. The two files publish.py and subscribe.py are both heavily commented with what basically each line is doing. So it's simple to follow. The source code is avaliable on my [__GitHub__](https://github.com/joseph-mccarthy/simple-python-mqtt-example).

## Brokers

In order to publish and subscribe to messages you'll require a broker. The code examples are currently set to use a free example from HiveMQ. If you are going to use HiveMQ free public broker __please remember that it's public and don't share sensitive information__. I'm personally using [__Mosquitto__](https://github.com/eclipse/mosquitto) as my broker on the network, running on a Raspberry Pi (Obviously).

### Installing Mosquitto (Raspberry Pi)

Mosquitto is already avaliable in the standard distribution so it's just a case of:

<script src="https://gist.github.com/joseph-mccarthy/ae83cd289979371a8fb6cbb4d0733577.js"></script>

This will default to always be running using port __1883__. That's all the set up that I needed to get this demo working, although the [__documentation__](https://mosquitto.org/documentation/) is great for Mosquitto.
