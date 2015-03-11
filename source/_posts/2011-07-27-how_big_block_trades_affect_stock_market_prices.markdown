---
layout: post
title: "How Big Block Trades Affect Stock Market Prices?"
date: 2011-07-27 16:01
comments: true
categories: [EN, R-language, TCA, data analysis, quant] 
---

I will be giving a presentation on "Optimal transaction cost" in [Vilnius][map] on 16th of August. While preparing the presentation and looking for an optimal execution solution, a natural question arises: does the size of the trade affect stock market price? I'm sure, you would say 100 % yes. Well, you would be right, but what is the scale of such effect? Is it possible to profit from execution of the big block trades?


Such test is not trivial and to conduct it, you need high frequency data, which is messy in most of the cases. For testing purpose I chose [BNP Paribas][bnp] stock from February 2011 to May 2011. Initially, I had more than 460 k. trades and more than 320k. quotes. However, the data was filtered by buyers initiated trades. To find buyers initiated trades, I used Lee-Ready Rule - short description can be found [here][here] on page 2. I found about Lee - Ready rule while reading [Maxdama][maxdama] last post and a damn good [summary][summary] (check page 42).


The first chart below shows the average return  one trade later (within seconds in most of the cases), when big or small trade was done. X axis represents difference between the trade and following trade, Y axis represents the trade size and the dot size represents number of trades within that cluster of volume. As you can see, small trades add 0.0004% to the price, while big ones (more than 980 of shares) increase the price on average 0.0007%


[![](http://i176.photobucket.com/albums/w180/investuotojas/bnpNextTrade.png)][1]


The next figure shows average return one minute later. This time the different between small trades and big one are almost3 times!


[![](http://i176.photobucket.com/albums/w180/investuotojas/bnpMinuteLater.png)][2]


While we can see, that stock market prices are affected by big blocks, there's no easy way to profit from it. You have to take into account bid/ask spread, plus you are becoming liquidity demander when liquidity is dry. On other end, this test shows the cost for each volume cluster and this cost can be used when choosing an optimal strategy for portfolio/stock liquidation.

[1]:http://s176.photobucket.com/albums/w180/investuotojas/?action=view&current=bnpNextTrade.png
[2]:http://s176.photobucket.com/albums/w180/investuotojas/?action=view&current=bnpMinuteLater.png
[map]:http://maps.google.com/maps?q=vilnius,Maironio+g.+11&hl=en&sll=54.689386,25.280024&sspn=0.599292,1.226349&z=16
[bnp]:http://finance.yahoo.com/q?s=BNP.PA&ql=0
[here]:http://goo.gl/RWSqa
[maxdama]:http://www.maxdama.com/?p=477
[summary]:http://dl.dropbox.com/u/39904/maxdama.pdf
