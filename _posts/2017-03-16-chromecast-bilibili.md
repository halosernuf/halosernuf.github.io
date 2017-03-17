---
layout: post
title: "Cast bilibili to Chromecast"
date:   2017-3-16 20:37:32
tags: bilibili chromecast 
categories: "Flask"
---

Chromecast is an great product, it solves the problem of wasting computer resources while mirroring to a TV/monitor. I was using `bpashen` for casting bilibili to Chromecast. However, after a api update of bilibili, the author seems to abandom the product because the program keep getting speed limited video urls. So, DIY TIME!

# Back-end

Hacking the bilibili api is done by [biligrab](https://github.com/cnbeining/Biligrab) and [you-get](https://github.com/soimort/you-get). I use [Flask](flask.pocoo.org) to build back-end and reference [UrlPlayer](https://github.com/vickyg3/UrlPlayer) for the connection to chromecast.

# Demo

Host the app at Heroku. 
[https://bilicast.herokuapp.com/](https://bilicast.herokuapp.com/)

# Speed limit

The video source url is followed by a parameter `rate`. 
Not sure how the bilibili api decide the speed limit for each request. In my case, when deployed on Heroku the speed is limited to 120, while on my own server or locally the speed limit is 440. I tend to believe the mechanism is IP based.