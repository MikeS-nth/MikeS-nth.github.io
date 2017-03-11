---
layout: post
title: "First Blog Post"
date: March 11, 2017
---

## The First Post...a work in progress

This is my first blog post.  I will be expanding this post as I continue building out the site, adding new features, and testing it.  While it might not be best practice to draft and iterate on the public facing site, I am doing it anyway :)  Break stuff and fix it, right?  

I'm using Github's free [Github Pages](https://pages.github.com) service to host this site, and I've installed [Jekyll](http://jekyllrb.com), which, among other things, lets me create a local web server so I can review my new posts and edits locally (from a branch of the master) before committing it to the live master branch.  Setting all this up took some research, but it's relatively straightforward if you have at lest some knowledge of Git, Github, CLI, and HTML.  

After some trial and error, I came across a great, simple, step-by-step how-to blog for [setting up your Github Pages website.](http://jmcglone.com/guides/github-pages/)

Github Pages lets you use HTML of course, but because the service relies on Jekyll, you can also write your blog posts in Markdown and the service will essentially convert it to HTML.  Markdown is great for making relatively presentable/formatted text content quickly and easily.  I like Markdown.

I'm not so into learning enough HTML for the purposes of blogging, so being able to write everything in Markdown is appealing.  However, I wanted to make sure I could still embed rich content in my posts from other sites.  For example, Tableau dashboards.  

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
