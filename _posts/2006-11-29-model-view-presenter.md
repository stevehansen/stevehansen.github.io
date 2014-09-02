---
title: Model-View-Presenter
author: Steve Hansen
layout: post
permalink: /2006/11/29/model-view-presenter/
categories:
  - Uncategorized
tags:
  - Software
---
Somebody mailed me that I should look into the MVP pattern (did I mention I love patterns! <img src="http://i2.wp.com/xiu.shoeke.com/wp-includes/images/smilies/icon_smile.gif?w=625" alt=":)" class="wp-smiley" data-recalc-dims="1" /> )

So after some browsing on the web it sure looks like the right pattern to use for my last problem.

MVP exists of a Model (the data), a View (the user interface) and a Presenter which links everything together. There are a few good articles about it on codeproject so you should look there if you want to.

Since MVP completly seperates model from view it should be possible to use an ORM and when you don&#8217;t want to use it anymore you just need to create a new model.

I couldn&#8217;t really find a sample of a MVP application with 2 models so I&#8217;ll create a sample myself. I might post it online to.

<div class="sharedaddy sd-sharing-enabled">
  <div class="robots-nocontent sd-block sd-social sd-social-official sd-sharing">
    <h3 class="sd-title">
      Share this:
    </h3>
    
    <div class="sd-content">
      <ul>
        <li class="share-email">
          <a rel="nofollow" class="share-email sd-button" href="http://xiu.shoeke.com/2006/11/29/model-view-presenter/?share=email" target="_blank" title="Click to email this to a friend"><span>Email</span></a>
        </li>
        <li class="share-twitter">
          <div class="twitter_button">
          </div>
        </li>
        
        <li class="share-google-plus-1">
          <div class="googleplus1_button">
            <div class="g-plus" data-action="share" data-annotation="bubble" data-href="http://xiu.shoeke.com/2006/11/29/model-view-presenter/">
            </div>
          </div>
        </li>
        
        <li class="share-facebook">
          <div class="like_button">
          </div>
        </li>
        
        <li class="share-linkedin">
          <div class="linkedin_button">
          </div>
        </li>
        
        <li class="share-reddit">
          <div class="reddit_button">
          </div>
        </li>
        
        <li class="share-end">
        </li>
      </ul>
    </div>
  </div>
</div>