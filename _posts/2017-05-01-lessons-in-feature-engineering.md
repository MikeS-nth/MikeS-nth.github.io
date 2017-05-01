---
layout: post
title: "Lessons in Feature Engineering"
feature-img: '../img/sample_feature_img_3.png'
---
I recently completed a brief, but intense, team effort on an old Kaggle competition as an exercise in testing and sharpening our data science skills.  We worked on the [West Nile Prediction](https://www.kaggle.com/c/predict-west-nile-virus) competition, which asks you to try and predict which mosquito traps in Chicago will contain a mosquito that tests positive for West Nile Virus.  

At a very high level, we were given data on individual mosquito traps, their locations, and, for given dates, how many mosquitos were found and whether or not West Nile Virus was present.  The latter point was a binary value (equivalent to a boolean True/False), so we did not know *how many* mosquitos tested positive.  We were also given weather data encompassing the same time period, as well as very limited data on insecticide spraying.  (You can read more about the competition and details via the link above.)

As we began to evaluate the task, we quickly became curious about the impact of a trap's proximity to any other trap(s) where West Nile Virus was detected.  In other words, if the virus was detected at a nearby trap, does that increase the likelihood that a given trap would have the virus at a future date?  And if so, what features of the data might allow us to make that prediction?

In a broader sense, we were interested in the hypothesis that presence of the virus at some location *in the past* has some relationship to if and where it will be detected at some other location *in the future*.  

To investigate these questions, we homed in on the weather dataset as being potentially quite relevant for two reasons:
1. It is commonly understood that weather conditions impact mosquito breeding and prevalence. We hoped this could allow us to correlate weather patterns with West Nile detection.
2. The dataset contained a continuous set of observations over time (i.e., every day), while the mosquito trap observations were spread out over time (e.g., once per week).  This meant that we could look at a given trap's weather conditions leading up to any given observation, which we thought would be more meaningful than single point-in-time measurements.

In order to test these ideas, we needed to extract and represent aspects of the data in a way that would allow statistical analysis and modeling.  In other words, we needed to engineer some features.

We decided to engineer two categories of features.  While two categories sounds like a manageable number, in practice it became quite cumbersome.  What we sought to derive from the data were features (a.k.a. columns, a.k.a. variables) that showed *for every single observation*:
- What was the weather on the day of the observation and for each of the 6 days prior.  In other words, one full week of weather observations for every mosquito trap observation.
- For every trap in every observation, what was the distance from that trap to all other traps, and what was the compass bearing (e.g., direction of travel) from that trap to all the others.

The intuition for the first category was simply that prior weather impacts mosquito breeding and activity.  The intuition for the second category was that perhaps the intensity (speed) and direction (bearing) of wind in the past week may have influenced the geographic movement of mosquitos, the birds that are the disease vector for West Nile Virus transmission to mosquitos, or both.

You may be seeing the issue we ran into...
- There were 44 weather variables we selected from the original weather data (this number reflects creating dummy variables on a single categorical column).  We wanted to show seven days' worth of weather for every observation, which adds up to 308 columns.  But wait, there's more...
- There were 138 trap locations, and we wanted to show the relative distance and compass bearing from each trap to every other trap.  That's 276 columns.
- Including all the other columns (like date, trap location, etc.), we had a dataset with **613 features**.

My teammate Brian created a gif to visualize this feature bloat:

![alt text](/../img/features.gif "too many features")

Now, feature selection is important, and generally more features often is not a good thing.  (It's decidedly a bad thing in terms of computational expense.)  We did run Principal Component Analysis on the data, which reduced the features all the way down to about 30.  But, the models with those features actually performed worse on average.

In the end, the models we built on this data did not end up performing especially well.  Our best ROC-AUC score from Kaggle was about 0.57 (although some of our training models did much better).

I am certain that we could further refine the feature selection and engineering.  For the purposes of this exercise, we were operating under a fixed timeframe and, well, ran out of time.

So, what are the lessons I promised in the title of this post? The first is a reinforcement of the importance of exploratory data analysis.  Not only is EDA critical in any data project, but it should be *iterative*, rather than a discrete task that is never revisited.  (Think Agile vs. waterfall.)  Had we done further rounds of EDA on our engineered data, we may have found clues about its usefulness before we went into modeling mode.

The second major lesson is the importance of sketching out the end-to-end workflow you are proposing to better understand and anticipate downstream issues.  For example, had we done this with the relative geographic features, we would have realized that our test dataset had some different traps (with different geographic locations) than in the training dataset.  This meant that our models were fit on X number of features, but when we transformed the test dataset, the number of columns didn't match.  This required a lot of last minute tweaking (and some compromises) to make it possible to run any models at all.

Finally, I learned to treat EDA a little more broadly in terms of methods and tools.  Excel can be an easy way to do a little EDA (as long as the data isn't too big).  Yes, I know, Excel.  I don't claim to be a purist, and I have no shame about using practical tools.  Same thing goes for Tableau, which can do quite a lot out of the box--including plotting regression lines.  It's no substitute for real data science, but it's a handy tool if you know how to interpret it.
