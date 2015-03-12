---
layout: post
title: "Kaggle Challenge - Event Recommendation Engine"
date: 2013-02-21 15:24
comments: true
categories: [ml,data mining,kaggle] 
---

[Event Recommendation Engine Challenge][event] was my second challenge at Kaggle and I finished 15th out of 225 on final (private) leaderboard. I was able to finish 1st on public leaderboard. Believe or not but the difference doesn't come from over fitting but rather from an external data source (Google Maps) which was forbidden. I did read the rules, but such important restriction was buried under additional layer of rules which I didn't bother to read. So moral of the story - if you are doing well then read the rules for second time. Nevertheless it is strange, why the host of the challenge didn't preprocess the data and didn't convert location of the users into latitude/longitude format? It would definitely lead to better models, as in my case such conversion gave + 4% in precision.


For this competition I used random forest almost exclusively and devoted all my time for the feature derivation. For the final prediction I built three models and then combined them together:


	set.seed(333)
	final_model3=randomForest(factor((interested-not_interested)/2+.5) ~ .,data=final_model,importance=TRUE,nodesize=4)

	set.seed(33)
	final_model1=randomForest(factor((interested-not_interested)/2+.5) ~ .,data=final_model,importance=TRUE,nodesize=4)

	set.seed(3)
	final_model2=randomForest(factor((interested-not_interested)/2+.5) ~ .,data=final_model,importance=TRUE,nodesize=4)

	final_model=combine(final_model3,final_model1,final_model2)


Below you can find a chart with most important features of my final model:


![](http://dl.dropbox.com/u/6360678/blog/features.png)


* ***time_diff*** - From early beginning I found that the difference between when the event is scheduled to begin and when the user saw the event ad is important feature which is easy to derive.

* ***popularity*** - How many users said they are interested in the event.

* ***start_hour*** - Turns out, that it is important to know at what hour an event is going to begin.

* ***friends*** - The name of this feature might be misleading, nevertheless it keeps how many user friends are invited to the event.

* ***joinedAt*** The difference between year when the user joined the service and 2000-01-01. I was surprised to find, that such feature has weight at all.

* ***timezone*** Had few NA values which I replaced by 0. Then I converted timezone numerical value into factor of two hours: 14-12, 12-10 and etc.

* ***birthyear*** Numeric value.

* ***weekdays*** On which weekday did the event happen? (Monday, Tuesday and etc).

* ***friend_yes, friend_no, friend_maybe*** Number of friends which are interested, not interested or maybe in the event.

* ***c_XXX All c_xxxx*** features were used without preprocessing.

* ***locale*** I used the first two letter of locale variable.

* ***location_mat*** Once I found, that external sources such as Google maps are forbidden then I tried to determine if user location shares the same words with event country, state and city descriptions. If it does I would add +1 (max 3) for location_mat variable.

* ***distance*** (forbidden) the feature scored high, but I had to remove it. The first step was to obtain latitude and longitude for users with known location. If you are interested here is the [source code][source] which shows how easily it can be done in R. Need to say, that I did manual and automated data cleaning - converted states names and some frequent errors like "City name 19". Once I had the coordinates of the users I was able to calculate the distance to event. Then I used k-means to predict user location for those who did not specified it, based on friends location. For example if 5 out of 8 friends of the user are based in Indonesia then user is given Indonesia location and distance to the event is calculated. Here's the [source code][hub] for prediction of user location.

[Click here][click] if you are interested in the source code of my solution.

[event]:https://www.kaggle.com/c/event-recommendation-engine-challenge/leaderboard
[rf]:http://www.stat.berkeley.edu/~breiman/RandomForests/cc_home.htm
[hub]:https://github.com/kafka399/kaggle-event/blob/master/user_friends_coord.r
[click]:https://github.com/kafka399/kaggle-event/blob/master/review.r
[source]:https://github.com/kafka399/kaggle-event/blob/master/address.r
