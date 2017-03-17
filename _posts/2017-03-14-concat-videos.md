---
layout: post
title: "Concat flv video parts to mp4"
date:   2017-3-14 20:25:49
tags: python ffmpeg
categories: "Python"
---

Video downloaded by [bilibili for mac](http://bilimac.eqoe.cn/) can be segments of video in flv files, which is not suitable for storage or transmit afterwards. 

File tree example:
```
.
├── 6335305-1.flv
├── 6335305-10.flv
├── 6335305-11.flv
├── 6335305-12.flv
├── 6335305-13.flv
├── 6335305-14.flv
├── 6335305-15.flv
├── 6335305-16.flv
├── 6335305-17.flv
├── 6335305-18.flv
├── 6335305-19.flv
├── 6335305-2.flv
├── 6335305-3.flv
├── 6335305-4.flv
├── 6335305-5.flv
├── 6335305-6.flv
├── 6335305-7.flv
├── 6335305-8.flv
├── 6335305-9.flv
└── 6335305.xml
```

Can use ffmpeg to concat the video segments to a single file

``` Python
#!/usr/bin/python
# -*- coding: UTF-8 -*- 
import os
import sys
import re
import subprocess

def tryint(s):
    try:
        return int(s)
    except:
        return s

def alphanum_key(s):
    """ Turn a string into a list of string and number chunks.
        "z23a" -> ["z", 23, "a"]
    """
    return [ tryint(c) for c in re.split('([0-9]+)', s) ]

def sort_nicely(l):
    """ Sort the given list in the way that humans expect.
    """
    l.sort(key=alphanum_key)

def writeInput(items):
    with open('input.txt','w') as f:
        for i in items:
            f.write("file '"+i+"'\n")

def removeItmes(items):
    for item in items:
        os.remove(item)
        
if __name__=="__main__":
    path = sys.argv[1];
    if os.path.exists(path):
        os.chdir(path)
        items=os.listdir('.')
        items=[files for files in items if 'flv' in files]
        sort_nicely(items)
        writeInput(items)
        string='ffmpeg -y -f concat -i input.txt -c copy "%(output)s.mp4"' % {'output':os.path.basename(os.path.abspath(path))}
        subprocess.call(string,shell=True)
        os.remove('input.txt')
        removeItmes(items) //auto remove flv files
```
Reference: 
* [http://stackoverflow.com/questions/4623446/how-do-you-sort-files-numerically](http://stackoverflow.com/questions/4623446/how-do-you-sort-files-numerically)
* [https://trac.ffmpeg.org/wiki/Concatenate#demuxer](https://trac.ffmpeg.org/wiki/Concatenate#demuxer)