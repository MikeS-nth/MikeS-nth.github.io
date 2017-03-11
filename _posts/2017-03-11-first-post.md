---
layout: post
title: "First Blog Post"
date: March 11, 2017
---

## Well, here goes nothing

This is my first blog post.  I will be expanding this post as I continue building out the site, adding new features, and testing it.  While it might not be best practice to draft and iterate on the public facing site, I am doing it anyway :)  Break stuff and fix it, I say.

I'm using Github's free Github Pages service to host this site, as well as Jekyll.  Setting this up was relatively straightforward given a relatively decent level of technical ability.  

After a lot of trial and error (especially while trying to parse how this works with Jekyll), I came across a great, simple, step-by-step how-to blog for [setting up your Github Pages website:] (http://jmcglone.com/guides/github-pages/)

Github Pages uses Jekyll, which means that you can write posts and create pages using Markdown (or raw HTML if you are so inclined).  I'm not so into writing HTML, so Markdown is appealing.  However, I wanted to make sure I could still embed rich content in my posts from other sites.  In particular, Tableau dashboards.  

After a deep trip down the Google rabbit hole, I found the simple answer that was staring me in the face:  Just copy & paste an iframe straight into your Markdown file (facepalm.

Here's a very simple Tableau dashboard I made using the SAT data from our current GA DSI project:


<iframe src="https://public.tableau.com/views/testhistogram/Sheet1?:embed=y&:display_count=yes"
 width="645" height="955"></iframe>


To accomplish this, I simply included the following code in my Markdown file:

    `<iframe src="https://public.tableau.com/views/testhistogram/Sheet1?:embed=y&:display_count=yes"
 width="645" height="955"></iframe>`

Why not try the same with a YouTube video? (Couldn't help myself, given that I'm working on my blog...)

<iframe width="560" height="315" src="https://www.youtube.com/embed/ZXsQAXx_ao0" frameborder="0" allowfullscreen></iframe>

Here's the embed code:

    `<iframe width="560" height="315" src="https://www.youtube.com/embed/ZXsQAXx_ao0" frameborder="0" allowfullscreen></iframe>`

More to come!