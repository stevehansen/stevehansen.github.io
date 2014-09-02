---
title: Resizing images with WPF 4.0
author: Steve Hansen
layout: post
permalink: /2010/07/15/resizing-images-with-wpf-4-0/
dsq_thread_id:
  - 2981565351
tags:
  - .NET 4.0
  - Resizer
  - WPF
---
Microsoft changed the default behaviour for scaling images with WPF 4.0/.NET 4.0.  
They opted for a faster but less accurate scaling algorithm named Linear instead of the default Fant that was used in WPF 3.0.

You can change this behaviour using the [RenderOptions.BitmapScalingMode][1] attached property.

{% highlight xml %}<Image Source="Image.png"
    RenderOptions.BitmapScalingMode="HighQuality" />{% endhighlight %}

Microsoft recommends to only use HighQuality if the image&#8217;s scaled size will be less that 30-50% of the original size.

The [Resizer ][2]application will always use HighQuality so that it gives the best image quality for any image.

Using the attached property on images scaled in code using DrawingVisual/[RenderTargetBitmap][3] requires a bit of special code.

{% highlight csharp %}private static BitmapFrame CreateResizedImage(ImageSource source, int width, int height, int margin)
{
    var rect = new Rect(margin, margin, width - margin * 2, height - margin * 2);

    var group = new DrawingGroup();
    RenderOptions.SetBitmapScalingMode(group, BitmapScalingMode.HighQuality);
    group.Children.Add(new ImageDrawing(source, rect));

    var drawingVisual = new DrawingVisual();
    using (var drawingContext = drawingVisual.RenderOpen())
        drawingContext.DrawDrawing(group);

    var resizedImage = new RenderTargetBitmap(
        width, height,         // Resized dimensions
        96, 96,                // Default DPI values
        PixelFormats.Default); // Default pixel format
    resizedImage.Render(drawingVisual);

    return BitmapFrame.Create(resizedImage);
}{% endhighlight %}

Width and height contains the margin already, so if the image is scaled to 300px with a margin of 10px then the method will be called with width = 320px and margin = 10px. We can use the DrawingGroup to set the BitmapScalingMode and then add the ImageDrawing to it.

 [1]: http://msdn.microsoft.com/en-us/library/system.windows.media.renderoptions.bitmapscalingmode.aspx
 [2]: http://resizer.codeplex.com/ "resizer.codeplex.com"
 [3]: http://msdn.microsoft.com/en-us/library/system.windows.media.imaging.rendertargetbitmap.aspx "RenderTargetBitmap Class"