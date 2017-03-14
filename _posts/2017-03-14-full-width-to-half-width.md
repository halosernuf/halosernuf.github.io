---
layout: post
title: "Replace full-width characters in file name with half-width"
date:   2017-3-14 16:57:34
tags: bash full-width-characters
categories: "Unix"
---

Facing with a problem when the filename consist, especially start with, a full-width character. It is hard to locate the file using auto-complete. For example:
```
【BBC】 英国史上的弥天大谎 S01E01 【冰冰字幕组】
```
which start with `【` is hard to print out in command line. Though you can use copy-paste to deal with it, it may not be efficient when all the files in a directory consist of those characters.

My solution is to change those full-width chars to half-width. It can be done by a simple bash script:

```
#!/bin/bash
for file in *[\【,\】,\（,\）,\《,\》,\：,\，,\？,\「,\」,\ ]*
do 
	mv "$file" `echo $file| \
	tr '【】（）《》：，？「」 ' '[]()<>:,?[]_'
done
```