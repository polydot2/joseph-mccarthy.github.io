---
title: "Network Domain and Nginx"
date: 2022-10-20T17:23:59+01:00
draft: false
sidebar: true
tags: [network,home lab]
hero: "hero.png"
summary: "Adding a domain name to network and setting up NGINX"
---

Today I've been playing around with adding a domain name to the machines on my local network. This is with the goal of making things more formal and eventually opening up services to the internet and setting up SSL. First I thought I'd start with a simple one which is my Raspberry Pi I used to hold data and grafanna. This is called data for the host name. To set a domain name I will be using the local DNS within [__Pi-Hole__]({{< ref "/posts/pi-hole" >}}) as that's already on my network. The first step is to reserve the ip address for the machine. This is done through Pi-Hole as well as I actively use this as my DCHP server in order for [__Pi-Hole__]({{< ref "/posts/pi-hole" >}}) to work due to limitations of my Virgin Router.

{{< bsimage src="reserve-ip.png" alt="reserve-ip">}}

Once the IP has been reserved for data.local I can then move on to assigning a domain to it. This will allow me to enter the full domain into a web browser and make life a lot easier when accessing applications outside of the home network eventually.

{{< bsimage src="adding-domain.png" alt="adding a domain">}}

This is why it was important to reserve the ip address for the machine with the hostname __data__ as the DNS entry is marked against a perticular ip address. Therefore we don't want he ip address to change if __data__ was to restart at some point. I'm now at a point where I can get to data by entering data.joemccarthy.co.uk. However there is an annoying thing which is that I don't want to keep putting port numbers in everywhere. So for example on __data.joemccarthy.co.uk__ is where I run Grafana. This runs on port 3000, and simply chaning this to port 80 is not as easy as it sounds. Also that's not really a solution either, as this would mean that I can only run a single application on a single machine. This isn't a great use of the hardware and forward thinking.

So to get round this I'll be using NGINX as a proxy. This will allow me to run multiple things on different ports while all accessing them via port 80 at __data.joemccarthy.co.uk__. I'll be using sublocations to achieve this, so the plan is to access grafana by entering __data.joemccarthy.co.uk/grafana__. The first step is to install nginx. Before doing that it's always best to do an update and upgrade

```
sudo apt update
sudo apt upgrade -y
```

It is extremely easy to install NGINX with the apt repository. Just run the command below and it will be ready!

```
sudo apt install nginx
```

Then just start it

```
sudo /etc/init.d/nginx start
```

Once the nginx has started I head over to __data.joemccarthy.co.uk__ to make sure that I'm greated with the default well to nginx bluff. The next job is to go and configure the location for nginx to forward to grafana. This is done inside the configuration file containted in __sites_enabled__

```
location /grafana/ {
    rewrite ^/route/?(.*)$ /$1 break;
    proxy_pass  http://127.0.0.1:3000;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
  }
```

Adding the above states for the given sublocation rewrite the request forwaring to same machine on port 3000 and pass along the request headers. With that being done and a quick restart of nginx I head over to __data.joemccarthy.co.uk__ to give it a test.

{{< bsimage src="grafana.png" alt="Configured">}}

Yay, it works. Going to leave it there for now.



