---
title: "Pi-hole"
date: 2022-03-01T20:33:23Z
draft: false
sidebar: true
tags: [Raspberry Pi, Infrastructure, Network, Pi Hole]
hero: "hero.png"
summary: Got my hands on a Raspberry Pi, first thing first block all the advertisements.
images: "hero.png"

---

So I finally got my hands on a Raspberry Pi, thanks to a work friend who wasn't using it at the time. So once I had it sent over I knew what I wanted to do with it first. I wanted to install Pi-Hole. The amount of advertising and tracking on the internet really bothers me it's not even the stuff that you see, it's the requests that you don't.

For example if a site says hey here's an advert well, I'm kinda ok with that. However a site that just takes my viewing data, and just sells that off to the highest bidder does bother me.

So like all Raspberry Pi projects it started with the flashing of an SD card with Raspberian OS lite, I don't need a Desktop experience for this project just ssh will do. Once in it was a simple onliner to get the installer going for Pi-Hole.

<script src="https://gist.github.com/joseph-mccarthy/cd3f121be58b37eb0175325c54133b52.js"></script>

Then you're just guided through the steps to setting up Pi-Hole, simple.

## Post Install

Once the installer has been run, you will need to configure your router to have DHCP clients use Pi-hole as their DNS server which ensures that all devices connecting to your network will have content blocked without any further intervention.

If your router does not support setting the DNS server, you can use Pi-hole's built-in DHCP server; be sure to disable DHCP on your router first. This was the case for my as my Internet Service Provider is Virgin, and what you're able to configure on their modem/router is rather limited.
