---
title: Japanese sorting in .NET
author: Steve Hansen
layout: post
permalink: /2012/11/06/japanese-sorting-in-net/
categories:
  - Uncategorized
tags:
  - Japanese
---
As you know I have my little test site on Appharbor  <http://vidyano.apphb.com/#!/KanjiOverview>

The Kanji data came from a SQL server database with an order by on the Kanji character. But once I cached the query (automatically refreshed every 30 minutes) the order was completely different. It seems that ordering and unicode don&#8217;t really match, apparently Japanese doesn&#8217;t really have a fixed (or at least a single) way of ordering their characters. And now because the order by was happening in .NET it gave me different results.

The only thing I could find was using special comparers, all linked to the ja-JP culture. But then it hit me, my current thread&#8217;s culture was already set to **ja-JP** because I was playing with the Japanese date format. Changing the thread back to **en-US** gave my back the same results as before.

The order is now uses is by radical and then stroke count which makes it easy to see the related/same kanji.

Does anyone know what order the Japanese culture info uses?

<div class="sharedaddy sd-sharing-enabled">
  <div class="robots-nocontent sd-block sd-social sd-social-official sd-sharing">
    <h3 class="sd-title">
      Share this:
    </h3>
    
    <div class="sd-content">
      <ul>
        <li class="share-email">
          <a rel="nofollow" class="share-email sd-button" href="http://xiu.shoeke.com/2012/11/06/japanese-sorting-in-net/?share=email" target="_blank" title="Click to email this to a friend"><span>Email</span></a>
        </li>
        <li class="share-twitter">
          <div class="twitter_button">
          </div>
        </li>
        
        <li class="share-google-plus-1">
          <div class="googleplus1_button">
            <div class="g-plus" data-action="share" data-annotation="bubble" data-href="http://xiu.shoeke.com/2012/11/06/japanese-sorting-in-net/">
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