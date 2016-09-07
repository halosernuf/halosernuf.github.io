---
layout: post
title: "Python regular expression learning"
date: 2016-09-07 12:36:00
---

# Special Characters

```.``` any character except a newline

```^``` start of string

```$``` end of string

```*``` 0 or more repetition

```+``` 1 or more repetition

```?``` 0 or 1 repetition

**all greedy**

```{m}``` pecifies that exactly m copies of the **previous** RE should be matched
*example: a{6} = aaaaaaa*

```{m,n}``` m to n repetations of the **previous**

```\``` escape special characters

```[]``` indicate a set of characters *example [amk] will match 'a', 'm', or 'k'*

```|``` 
 *example A|B will match either A or B* 
 **from left to right**

```\d``` [0-9]

```\D``` nondigital char

```\s``` any space char

```\S``` any char other than space

```\w``` any numalpha
n
```\W``` any char other than numalpha