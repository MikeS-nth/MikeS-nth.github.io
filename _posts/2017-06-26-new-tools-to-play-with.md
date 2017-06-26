---
layout: post
title: "New Tools to Play With!"
feature-img: '../img/sample_feature_img_3.png'
---
Over the weekend, I attended the D.C.-area [Data Intelligence](http://www.data-intelligence.ai) conference, which was organized by [NumFocus](https://www.numfocus.org).  It was great to see some of the really interesting machine learning work that people are doing--certainly far too much to capture in a blog post.  But check out the list of talks on the site linked above.

One of the fun parts for me was discovering new tools that can improve my data science workflow. Below are two that I'm excited to start playing with.  I will be doing some actual testing of these (and others!) in the coming week or two, and I'll publish future posts about what I've learned.  

### Yellowbrick

[Yellowbrick](https://github.com/DistrictDataLabs/yellowbrick), created by [District Data Labs](http://www.districtdatalabs.com), is another visualization-related tool that essentially ties  Scikit-Learn with Matplotlib to make it easier to visualize your data at each step in your sklearn modeling process.  

[Benjamin Bengfort](https://github.com/bbengfort) of District Data Labs did a talk at the conference about using Yellowbrick to create a "visual pipeline" for textual analysis in sklearn.

The authors characterize it as a "suite of visual diagnostic tools called "Visualizers" that extend the Scikit-Learn API to allow human steering of the model selection process."  Essentially, they've created a set of what they call "visualizers" that help you examine and tune your models.  With a visualizer, you use very familiar sklearn-style methods (e.g. `.fit()`, `.score()`) and finally Yellowrick's `.poof()` method to both execute the transformations and also generate the appropriate visualization.  

Why is this cool?  For one, it makes it a lot easier and more seamless to embed visualization at each step of the process when using skearn--and that's important because visualization is one of the best ways for a human to understanding the data and spot insights or issues.

It's also got some helpful things out of the box:  For example, classification reports and confusion matrices incorporate heat map-style color coding to enhance interpretability.  Also, because the visualizations are built with Matplotlib, you can get under the hood and customize them as you wish.

### mpld3

[mpld3](https://mpld3.github.io) is a Python library that adds some of the awesomeness of javascript D3 ([D3js](http://d3js.org/)) to matplotlib so that you can generate HTML visualizations without needing to work directly in D3.  

I saw this in use during [Francois Dion's](https://github.com/fdion) discussion of identifying and understanding outliers.

Why is this cool?  The easiest example is adding basic interactivity to your plots (including within a Jupyter notebook) with one or two extra lines of code.  Let's say I've generated a scatterplot and there are a couple of extreme outliers.  With matplotlib alone, it would be tedious to identify the index of that outlier.  However, with mpld3, it is trivial to add a tooltip to the plot, allowing you to see the index (or whatever else you define in the tooltip) by hovering the mouse over that point.  This is a huge timesaver for exploring outliers.
