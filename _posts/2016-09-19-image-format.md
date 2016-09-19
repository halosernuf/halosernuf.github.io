---
layout: post
title: "Image Format Compare"
date: 2016-09-19 13:15:31
tags: image format compare
---

Source: [http://stackoverflow.com/questions/2336522/png-vs-gif-vs-jpeg-vs-svg-when-best-to-use](http://stackoverflow.com/questions/2336522/png-vs-gif-vs-jpeg-vs-svg-when-best-to-use)

You should be aware of a few key factors...

First, there are two types of compression: Lossless and Lossy.

Lossless means that the image is made smaller, but at no detriment to the quality.
Lossy means the image is made (even) smaller, but at a detriment to the quality. If you saved an image in a Lossy format over and over, the image quality would get progressively worse and worse.
There are also different colour depths (palettes): Indexed color and Direct color.

Indexed means that the image can only store a limited number of colours (usually 256), controlled by the author, in something called a Color Map
Direct means that you can store many thousands of colours that have not been directly chosen by the author

## BMP - Lossless / Indexed and Direct

This is an old format. It is Lossless (no image data is lost on save) but there's also little to no compression at all, meaning saving as BMP results in VERY large file sizes. It can have palettes of both Indexed and Direct, but that's a small consolation. The file sizes are so unnecessarily large that nobody ever really uses this format.

**Good for** : Nothing really. There isn't anything BMP excels at, or isn't done better by other formats.

BMP vs GIF
[<img src="/images/imageformat/BG.png">](/images/imageformat/BG.png)

## GIF - Lossless / Indexed only

GIF uses lossless compression, meaning that you can save the image over and over and never lose any data. The file sizes are much smaller than BMP, because good compression is actually used, but it can only store an Indexed palette. This means that for most use cases, there can only be a maximum of 256 different colours in the file. That sounds like quite a small amount, and it is.

GIF images can also be animated and have transparency.

**Good for** : Logos, line drawings, and other simple images that need to be small. Only really used for websites.

GIF vs JPEG
[<img src="/images/imageformat/GJ.png">](/images/imageformat/GJ.png)

## JPEG - Lossy / Direct

JPEGs images were designed to make detailed photographic images as small as possible by removing information that the human eye won't notice. As a result it's a Lossy format, and saving the same file over and over will result in more data being lost over time. It has a palette of thousands of colours and so is great for photographs, but the lossy compression means it's bad for logos and line drawings: Not only will they look fuzzy, but such images will also have a larger file-size compared to GIFs!

**Good for** : Photographs. Also, gradients.

JPEG vs GIF
[<img src="/images/imageformat/JG.png">](/images/imageformat/JG.png)

## PNG-8 - Lossless / Indexed

PNG is a newer format, and PNG-8 (the indexed version of PNG) is really a good replacement for GIFs. Sadly, however, it has a few drawbacks: Firstly it cannot support animation like GIF can (well it can, but only Firefox seems to support it, unlike GIF animation which is supported by every browser). Secondly it has some support issues with older browsers like IE6. Thirdly, important software like Photoshop have very poor implementation of the format. (Damn you, Adobe!) PNG-8 can only store 256 colours, like GIFs.

**Good for** : The main thing that PNG-8 does better than GIFs is having support for Alpha Transparency.

PNG-8 vs GIF
[<img src="/images/imageformat/PG.png">](/images/imageformat/PG.png)

**Important Note** : Photoshop does not support Alpha Transparency for PNG-8 files. (Damn you, Photoshop!) There are ways to convert Photoshop PNG-24 to PNG-8 files while retaining their transparency, though. One method is PNGQuant, another is to save your files with Fireworks.

## PNG-24 - Lossless / Direct

PNG-24 is a great format that combines Lossless encoding with Direct color (thousands of colours, just like JPEG). It's very much like BMP in that regard, except that PNG actually compresses images, so it results in much smaller files. Unfortunately PNG-24 files will still be much bigger than JPEGs, GIFs and PNG-8s, so you still need to consider if you really want to use one.

Even though PNG-24s allow thousands of colours while having compression, they are not intended to replace JPEG images. A photograph saved as a PNG-24 will likely be at least 5 times larger than a equivalent JPEG image, with very little improvement in visible quality. (Of course, this may be a desirable outcome if you're not concerned about filesize, and want to get the best quality image you can.)

Just like PNG-8, PNG-24 supports alpha-transparency, too.

## SVG - Lossless / Vector

A filetype that is currently growing in popularity is SVG, which is different than all the above in that it's a vector file format (the above are all raster). This means that it's actually comprised of lines and curves instead of pixels. When you zoom in on a vector image, you still see a curve or a line. When you zoom in on a raster image, you will see pixels.

For example:

SVG vs PNG
[<img src="/images/imageformat/SP.png">](/images/imageformat/SP.png)
[<img src="/images/imageformat/SP2.png">](/images/imageformat/SP2.png)

This means SVG is perfect for logos and icons you wish to retain sharpness on Retina screens or at different sizes. It also means a small SVG logo can be used at a much larger size -- something that would require a separate larger file with raster formats.

SVG file sizes are often tiny, even if they're visually very large, which is great. It's worth bearing in mind, however, that it does depend on the complexity of the shapes used. SVGs require more computing power than raster images because mathematic calculations are involved in drawing the curves and lines. If your logo is especially complicated it could slow down a user's computer, and even have a very large file size. It's important that you simplify your vector shapes as much as possible.

Additionally, SVG files are written in XML, and so can be opened and edited in a text editor(!). This means its values can be manipulated on the fly. For example, you could use JavaScript to change the colour of an SVG icon on a website, much like you would some text (ie. no need for a second image), or even animate them.

In all, they are best for simple flat shapes like logos or graphs.

I hope that helps!