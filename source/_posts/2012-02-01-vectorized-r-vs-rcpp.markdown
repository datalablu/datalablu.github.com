---
layout: post
title: "Vectorized R vs Rcpp"
date: 2012-02-01 11:35
comments: true
categories: [EN, R-language, data analysis, quant] 
---

[In my previous post][post], I tried to show, that Rcpp is 1000 faster than pure R and that generated the fuss in the comments. Being lazy, I didn't vectorize R code and at the end I was comparing apples vs oranges.

To fix that problem, I built a new script, where I'm trying to compare apples against apples. First piece of code named "ifelse R" uses R "ifelse" function to vectorize code. Second piece of code is fully vectorized code written in R, third - pure C++ code and the last one is C++, where  Rcpp "ifelse" function is used.


[![](http://i176.photobucket.com/albums/w180/investuotojas/performance.png)][1]

| Name  | Seconds |
|-------|--------|
| ifelse R | 27.50
| vectorized R | 10.40
| pure C++ | 0.44
| vectorized C++ | 2.24


Here we go - vectorization truly helps, but pure C++ code still 23 times faster. Of course you pay the price when writing it in C++. I found a bit strange, that vectorized C++ code doesn't perform that well...

You can get the code from [github][github].

[post]:http://www.investuotojas.eu/2012/01/30/the-power-of-rcpp/
[1]:http://s176.photobucket.com/albums/w180/investuotojas/?action=view&current=performance.png
[github]:https://github.com/kafka399/Rproject/blob/master/performance/performance.R
