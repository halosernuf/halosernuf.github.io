---
layout: post
title: QuickLook and Archive Utility Not Working
date: 2016-10-03 21:12:50
categories: "MACOS"
tags: quicklook macos not working
---

# QuickLook and Archive Utility Not Working

>Original https://robertshippey.net/blog/quicklook-and-archive-utility-not-working/

I just got the error “The contents list can’t be created for compressing.”  when I compress everything & Quicklook notworking.

If anyone else has had these issues, here’s a set of terminal commands that should help.

## remove tmp folder
```
sudo rm -rf /tmp
sudo rm -rf /private/tmp
```

## Create new tmp folder 
```
sudo mkdir /private/tmp
sudo chmod 777 /private/tmp
sudo chmod +t /private/tmp
```

## link to /tmp
```
sudo ln -s /private/tmp /tmp
```


