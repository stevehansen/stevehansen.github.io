---
title: Distributing code with NuGet packages
author: Steve Hansen
layout: post
permalink: /2012/10/26/distributing-code-with-nuget-packages/
categories:
  - Uncategorized
tags:
  - NuGet
  - Vidyano
---
NuGet packages are getting really popular for distributing libraries. But I found out that they can also be used to distribute C# code.

This can be very useful to share those &#8220;small&#8221; libraries with extension methods or other commong code, you can still include comments or extra information, and they can be updated like any other NuGet package without adding all those extra external libraries.

With the introduction of <a title="JavaScript" href="http://www.vidyano.com/#!/Documentation/javascript" target="_blank">JavaScript</a> in Vidyano we have the option to expose .NET classes to the JavaScript side (as globals). But it will only look for classes in your service project that has the ExposeToJavaScript attribute. So with the NuGet code packages we can provide common extensions for Vidyano JavaScript that are easily updated and installed.

The first released NuGet extension is for adding basic Reflection support to JavaScript, allowing you to load assemblies, create instances and get field/properties/methods.

<https://nuget.org/packages/Vidyano.Reflection>

The source code is also available on Bitbucket so you can play around with it and make your own code packages.

<https://bitbucket.org/Hansen/vidyano.reflection>

<div class="sharedaddy sd-sharing-enabled">
  <div class="robots-nocontent sd-block sd-social sd-social-official sd-sharing">
    <h3 class="sd-title">
      Share this:
    </h3>
    
    <div class="sd-content">
      <ul>
        <li class="share-email">
          <a rel="nofollow" class="share-email sd-button" href="http://xiu.shoeke.com/2012/10/26/distributing-code-with-nuget-packages/?share=email" target="_blank" title="Click to email this to a friend"><span>Email</span></a>
        </li>
        <li class="share-twitter">
          <div class="twitter_button">
          </div>
        </li>
        
        <li class="share-google-plus-1">
          <div class="googleplus1_button">
            <div class="g-plus" data-action="share" data-annotation="bubble" data-href="http://xiu.shoeke.com/2012/10/26/distributing-code-with-nuget-packages/">
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