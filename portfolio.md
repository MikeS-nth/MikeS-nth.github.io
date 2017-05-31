---
layout: page
title: Portfolio
permalink: /portfolio/
feature-img: "img/sample_feature_img_2.png"
---

## [Predicting D.C. Traffic](https://github.com/MikeS-nth/portfolio/blob/master/DC_Traffic_Prediction/Predicting_DC_Traffic_Mike_Sanders.ipynb)

Traffic in the District of Columbia is bad; that much is a given. But what if you could know ahead of time just how bad it was going to be?

I set out to try to answer that question based on an intuition that's evolved in 15+ years of living here: Perhaps the volume and intensity of political/governmental activity and events on a given day impacts that day's traffic.  

After all, politics and government remain the District's primary industry, with many adjacent and/or support industries (e.g., catering, private security, lobbying, etc.).  If the political calendar drives these other industries, perhaps its influence on the total number of people coming into the city can be correlated to traffic.

This was a proof-of-concept project, and I'm happy to report that the results suggest that it may indeed be possible to build a traffic forecast based on event data.

I've written up a more detailed description [in this blog post](https://michaeljsanders.com/2017/05/26/predicting-dc-traffic.html).  You can also find the data, code, and complete writeup in a [jupyter notebook on Github](https://github.com/MikeS-nth/portfolio/blob/master/DC_Traffic_Prediction/Predicting_DC_Traffic_Mike_Sanders.ipynb).


## [Identifying Target Counties for a New Liquor Store in Iowa](http://nbviewer.jupyter.org/github/MikeS-nth/portfolio/blob/master/Iowa_Liquor_Store_Siting/Liquor_store_siting_analysis.ipynb)

This project was from an assignment for the General Assembly Data Science Immersive course that I completed.  We were given a dataset from the Iowa Alcoholic Beverages Division containing detailed information on wholesale transactions and Iowa liquor stores covering about 5 quarters.  

In the scenario, there were investors interested in opening a new liquor store in Iowa and wanted to know what locations they should target for in-depth market research.  The task was to use the dataset to develop recommendations for the investors on which specific geographic areas made sense for spending limited research resources.

Coming from a technology sales and business strategy background, I found this project particularly interesting.  One of the key challenges with the data was that it provided wholesale transactions from the state to the store, but no information on store-level sales to consumers or other costs.  This meant I was working with the equivalent of COGS for each store, but no way to confidently know revenue (let alone profit).  

I focused my geographic attention to the county level, since zip codes are terrible for anything other than sending letters and city-level is too granular and limiting for a largely rural state.  To home in on target counties, I created what I called an "opportunity score", which compares a county's population, per-capita income, per-capita liquor stores, and liquor store COGS (as a rough leading for the businesses' performance).  This allowed me to rank and sort each county by their opportunity score (higher is better), which is a deliverable for an investment team seeking to home in on target counties.

For best results, I recommend [reading the notebook via nbviewer](http://nbviewer.jupyter.org/github/MikeS-nth/portfolio/blob/master/Iowa_Liquor_Store_Siting/Liquor_store_siting_analysis.ipynb).

*Note:* because the source data file is >377MB, I am not hosting it on Github.  If you are interested in recreating the analysis, you can find you can access the same data from the [Iowa Alcoholic Beverages Division](https://abd.iowa.gov/).  I may consider hosting this specific file if enough people express interest.


## [Bayesian A/B Testing](https://github.com/MikeS-nth/portfolio/blob/master/Bayesian_AB_testing/Bayesian_AB_testing.ipynb)
A/B testing is an extremely common and useful method for optimizing content, such as websites or marketing emails.  

Typically, A/B test results are evaluated using traditional, Frequentist hypothesis testing (or, perhaps without any statistical method other than comparing total results).  Arguably, Bayesian hypothesis testing is more appropriate for A/B tests, since the evaluation is *based on the actual data*.  Arguably, Bayes is more appropriate for everything.

This mini project is an implementation of a Bayesian A/B test using the PyMC library for Python.  The beauty of PyMC is it allows you to conduct the Markov Chain Monte Carlo simulation needed to evaluate your data with just a few lines of code.

The code and results can be viewed in a [jupyter notebook on my Github profile](https://github.com/MikeS-nth/portfolio/blob/master/Bayesian_AB_testing/Bayesian_AB_testing.ipynb).
