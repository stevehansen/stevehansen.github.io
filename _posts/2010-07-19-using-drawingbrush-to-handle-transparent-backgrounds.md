---
title: Using DrawingBrush to handle transparent backgrounds
author: Steve Hansen
layout: post
permalink: /2010/07/19/using-drawingbrush-to-handle-transparent-backgrounds/
dsq_thread_id:
  - 2982209807
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

<img class="alignnone size-full wp-image-129" title="TransparentBackground" src="http://i1.wp.com/xiu.shoeke.com/wp-content/uploads/2010/07/TransparentBackground.png?resize=143%2C134" alt="" data-recalc-dims="1" />