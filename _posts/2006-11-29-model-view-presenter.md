---
title: Model-View-Presenter
author: Steve Hansen
layout: post
permalink: /2006/11/29/model-view-presenter/
tags:
  - Software
---
Somebody mailed me that I should look into the MVP pattern (did I mention I love patterns! <img src="http://i2.wp.com/xiu.shoeke.com/wp-includes/images/smilies/icon_smile.gif?w=625" alt=":)" class="wp-smiley" data-recalc-dims="1" /> )

So after some browsing on the web it sure looks like the right pattern to use for my last problem.

MVP exists of a Model (the data), a View (the user interface) and a Presenter which links everything together. There are a few good articles about it on codeproject so you should look there if you want to.

Since MVP completly seperates model from view it should be possible to use an ORM and when you don&#8217;t want to use it anymore you just need to create a new model.

I couldn&#8217;t really find a sample of a MVP application with 2 models so I&#8217;ll create a sample myself. I might post it online to.