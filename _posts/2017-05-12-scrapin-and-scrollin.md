---
layout: post
title: "Tricks for Scraping Scrolling Pages"
feature-img: '../img/sample_feature_img_3.png'
---
For a recent project, I was scraping data from a few different websites and needed to solve for how to handle infinite scrolling.  Here are two useful methods I found that worked for me.  (They won't work in every situation, but I think they are good to know.)

Before I get into the details, let me define what I mean by infinite scrolling.  This is a feature found on many modern websites where additional content is only loaded when the user scrolls to the bottom of the active window.

This creates a problem for basic web scraping, since simply requesting the page does not load all the data we want to grab.  This means we need to find a way to make the page scroll in order to collect the data (or access the data we want in other ways).

## When the Entire Page Has Infinite Scroll
Generally, Selenium is a great library any time you want to programmatically interact with a website.  It provides a headless web driver, which you can program to interact with a website as if it were a human.

For a site where the entire page has infinite scroll, you can use the following code to scroll to the "true" bottom and then grab the content:

```python
import time
from selenium import webdriver
from bs4 import BeautifulSoup as bs

# I used Firefox; you can use whichever browser you like.
browser = webdriver.Firefox()

# Tell Selenium to get the URL you're interested in.
browser.get("http://URLHERE.com")

# Selenium script to scroll to the bottom, wait 3 seconds for the next batch of data to load, then continue scrolling.  It will continue to do this until the page stops loading new data.
lenOfPage = browser.execute_script("window.scrollTo(0, document.body.scrollHeight);var lenOfPage=document.body.scrollHeight;return lenOfPage;")
    match=False
        while(match==False):
                lastCount = lenOfPage
                time.sleep(3)
                lenOfPage = browser.execute_script("window.scrollTo(0, document.body.scrollHeight);var lenOfPage=document.body.scrollHeight;return lenOfPage;")
                if lastCount==lenOfPage:
                    match=True

# Now that the page is fully scrolled, grab the source code.
source_data = browser.page_source

# Throw your source into BeautifulSoup and start parsing!
bs_data = bs(source_data)
```
## When a Sub-Section of a Page Has Infinite Scroll
This one is trickier, and to be honest, I don't yet have a programmatic way to solve for it.  The situation I encountered on a particular site was there was a `<DIV>` which had its own infinite scroll nested within it.

The code snippet above only worked to scroll the overall `<BODY>`, but this did not scroll the content of the `<DIV>` and therefore did not trigger the site to call all of the data I wanted.

I found many suggestions on stackoverflow on how to handle this, but was (so far) unsuccessful in implementing it.  

Then I learned something interesting: if the site is built with javascript (as so many are), then the infinite scroll is probably returning data from a JSON file.

If I could find the JSON, maybe I can access the data directly.  And in fact I did find it.  On the Network tab of Chrome's site inspection tool (be sure to reload the page), I found this:

![jsons](https://michaeljsanders.com/img/site_inspect.jpg)

See all of those items under Name labeled [year].json?  Each of those turned out to be a full year's worth of data in one file, no scrolling required.  

At that point, it was as simple as grabbing the URL of the JSON and grabbing the data with `pandas.read_json('url_address')`
