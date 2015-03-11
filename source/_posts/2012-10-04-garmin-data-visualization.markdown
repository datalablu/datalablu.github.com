---
layout: post
title: "Garmin Data Visualization"
date: 2012-10-04 14:38
comments: true
categories: [EN, R-language, data analysis] 
---

People go on rage, when governments initiate surveillance projects like [CleanIT][clean], nevertheless share very private data without a doubt.

I have to admit, that some data leaks are well buried in the process. Take for example Garmin which produces GPS training devices for runners. In order to see your workouts you are forced to upload sensitive data on internet. In response you are given a visualization tool and a storage facility. What are alternatives? It seems, that in the past there was a desktop version, however I was not able to find it. So, we are left with the last option - hack it.

First of all you need to transfer data from Garmin device to computer. I own Forerunner 610 with relays on [ANT][ant] network and I found Python [script][script] with takes care of data transfer. Once data is transfered there is another obstacle - Garmin uses a proprietary format [FIT][fit]. In order to tackle this problem I use another [Python script][pscript] which I have adapted to have [csv format][csv].

Once data is in CSV format R can be used to plot data.


![](http://dl.dropbox.com/u/6360678/blog/garmin_1.png)


![](http://dl.dropbox.com/u/6360678/blog/garmin_2.png)


I had a lot of fun by trying to understand Garmin longitude and latitude coordinates. Here is a short explantion by Hal Mueller:


> The mapping Garmin uses (180 degrees to 2^31 semicircles) allows them to use a standard 32 bit unsigned integer to represent the full 360 degrees of longitude. Thus you get the maximum precision that 32 bits allows you (about double what you get from a floating point value), and they still get to use integer arithmetic instead of floating point.


![](http://dl.dropbox.com/u/6360678/blog/garmin_map.png)



[clean]:http://www.edri.org/cleanIT
[ant]:http://en.wikipedia.org/wiki/ANT_(network)
[script]:https://github.com/kafka399/Garmin-Forerunner-610-Extractor
[fit]:http://www.thisisant.com/pages/developer-zone/fit-sdk
[pscript]:https://github.com/dtcooper/python-fitparse
[csv]:https://github.com/kafka399/fitparse/blob/master/run.py

