---
layout: post
title: "Watchface Dev 1"
date: 2016-09-27 16:06:25
categories: "Android"
tags: android wear
---

# MyWatchFaceService.java

Our watch face and it has a watch face engine called MyWatchFaceService.Engine. This file is located in the directory 1-base/java/com/android/example/watchface. In Android Studio, this is located under 1-base/java/com.android.example.watchface. Within the Engine class, we will mainly be working on three methods:

# onCreate

We will initiate new classes such as the bitmap image object for our background, etc. This code is run once when the Engine is first started.

# onSurfaceChanged

This is the first time when we have the dimension of the screen. Armed with this new information, we can resize any screen element required for drawing. This code is also expected to only be run once at the start.

# onDraw

The core of what we will be doing. It renders every frame on the watch face canvas. Since it runs on every frame, we will try to keep this as fast as possible - no image resizing or object creation here!

```
Pro-tip
To achieve a high frame rate which results in smooth animations no intense computations should happen in here. We can load images and resize them before we start drawing in onCreate and onSurfaceChanged.
```

# res/drawable-nodpi/

This is the directory where we will be placing some additional image files.