---
layout: post
title: "First Blog Post"
date: March 11, 2017
---

## Well, here goes nothing

This is my first blog post.  I will be expanding this post as I continue building out the site, adding new features, and testing it.  While it might not be best practice to draft and iterate on the public facing site, I am doing it anyway :)  Break stuff and fix it, right?

I'm using Github's free Github Pages service to host this site, and I've installed Jekyll to create a local web server so I can edit my blog on a separate branch, view it via a localhost address, and edit it offline before I merge it into master and push to the live site.  Setting this up was relatively straightforward given a relatively decent level of technical ability.  

After some trial and error, I came across a great, simple, step-by-step how-to blog for [setting up your Github Pages website.](http://jmcglone.com/guides/github-pages/)

Github Pages lets you use HTML of course, but because the service relies on Jekyll, you can also write your blog posts in Markdown and the service will essentially convert it to HTML.

I'm not so into writing HTML, so being able to write everything in Markdown is appealing.  However, I wanted to make sure I could still embed rich content in my posts from other sites.  For example, Tableau dashboards.  

After a deep trip down the Google rabbit hole, I found the simple answer that was staring me in the face:  Just copy the iframe code (which websites will generate for you when you click the "embed" button next to a video, etc.) and copy it straight into your Markdown file.  No special syntax needed (facepalm).

Here's a very simple Tableau dashboard I made using some data on US SAT scores:


<iframe src="https://public.tableau.com/views/testhistogram/Sheet1?:embed=y&:display_count=yes"
 width="645" height="955"></iframe>


To accomplish this, I simply pasted the following code in my Markdown file:

    `<iframe src="https://public.tableau.com/views/testhistogram/Sheet1?:embed=y&:display_count=yes"
 width="645" height="955"></iframe>`

Why not try the same with a YouTube video? (Couldn't help myself, given that I'm working on my blog...)

<iframe width="560" height="315" src="https://www.youtube.com/embed/ZXsQAXx_ao0" frameborder="0" allowfullscreen></iframe>

Here's the embed code:

    `<iframe width="560" height="315" src="https://www.youtube.com/embed/ZXsQAXx_ao0" frameborder="0" allowfullscreen></iframe>`

More to come!
