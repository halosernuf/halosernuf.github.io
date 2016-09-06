---
layout: post
title: "Beaglebone Cam"
date:   2016-09-06 14:00:21 
categories: "Beaglebone"
---

# Using beaglebone as a security camera 

Based on this [project](http://phoboslab.org/log/2013/09/html5-live-video-streaming-via-websockets)

# Build FFMPEG on Beaglebone [[Origin]](http://derekmolloy.ie/building-ffmpeg-for-beaglebone-from-source/)
```
git clone git://git.videolan.org/x264.git
cd x264
./configure --enable-shared --prefix=/usr
make
make install
```
```
git clone git://git.videolan.org/ffmpeg.git
./configure --enable-shared --enable-libx264 --enable-gpl
git remote set-url origin git://source.ffmpeg.org/ffmpeg
make
make install
```

# Start ffmpeg stream over HTTP 

```
ffmpeg -s 640x480 -f video4linux2 -i /dev/video0 -f mpeg1video \
-b 800k -r 30 http://example.com:8082/yourpassword/640/480/
```

# Use websocket to receive and distribute

```
npm install ws
node stream-server.js yourpassword
```


