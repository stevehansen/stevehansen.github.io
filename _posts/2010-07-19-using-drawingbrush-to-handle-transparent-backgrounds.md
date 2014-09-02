---
title: Using DrawingBrush to handle transparent backgrounds
author: Steve Hansen
layout: post
permalink: /2010/07/19/using-drawingbrush-to-handle-transparent-backgrounds/
dsq_thread_id:
  - 2982209807
categories:
  - Uncategorized
tags:
  - WPF
---
With images it is sometimes difficult to see the difference between a white and transparent background. Using a DrawingBush in Tile mode can create the known checker background used in applications as Photoshop.

<pre class="brush: xml">&lt;DrawingBrush&gt;
    &lt;DrawingBrush.Drawing&gt;
        &lt;DrawingGroup&gt;
            &lt;GeometryDrawing Brush="White"&gt;
                &lt;GeometryDrawing.Geometry&gt;
                    &lt;RectangleGeometry Rect="0,0,10,10" /&gt;
                &lt;/GeometryDrawing.Geometry&gt;
            &lt;/GeometryDrawing&gt;
            &lt;GeometryDrawing Brush="LightGray"&gt;
                &lt;GeometryDrawing.Geometry&gt;
                    &lt;GeometryGroup&gt;
                        &lt;RectangleGeometry Rect="0,0,5,5" /&gt;
                        &lt;RectangleGeometry Rect="5,5,5,5" /&gt;
                    &lt;/GeometryGroup&gt;
                &lt;/GeometryDrawing.Geometry&gt;
            &lt;/GeometryDrawing&gt;
        &lt;/DrawingGroup&gt;
    &lt;/DrawingBrush.Drawing&gt;
&lt;/DrawingBrush&gt;</pre>

Which will give the following effect if used as the background property.

<img class="alignnone size-full wp-image-129" title="TransparentBackground" src="http://i1.wp.com/hansen.azurewebsites.net/wp-content/uploads/2010/07/TransparentBackground.png?resize=143%2C134" alt="" data-recalc-dims="1" />

<div class="sharedaddy sd-sharing-enabled">
  <div class="robots-nocontent sd-block sd-social sd-social-official sd-sharing">
    <h3 class="sd-title">
      Share this:
    </h3>
    
    <div class="sd-content">
      <ul>
        <li class="share-email">
          <a rel="nofollow" class="share-email sd-button" href="http://xiu.shoeke.com/2010/07/19/using-drawingbrush-to-handle-transparent-backgrounds/?share=email" target="_blank" title="Click to email this to a friend"><span>Email</span></a>
        </li>
        <li class="share-twitter">
          <div class="twitter_button">
          </div>
        </li>
        
        <li class="share-google-plus-1">
          <div class="googleplus1_button">
            <div class="g-plus" data-action="share" data-annotation="bubble" data-href="http://xiu.shoeke.com/2010/07/19/using-drawingbrush-to-handle-transparent-backgrounds/">
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