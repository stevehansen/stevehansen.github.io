---
title: WPF Image Buttons
author: Steve Hansen
layout: post
permalink: /2010/07/16/wpf-image-buttons/
categories:
  - Uncategorized
tags:
  - Resizer
  - WPF
---
For my [Resizer][1] application I wanted a toolbar with image buttons, everything was perfect until I tried to disable the buttons. The first idea was to add a greyscale effect to the button if it was disabled. For a complete black/white icon this didn&#8217;t help either but changing the opacity does.

<img class="alignnone size-full wp-image-124" title="Toolbar-WithDisabled" src="http://i0.wp.com/hansen.azurewebsites.net/wp-content/uploads/2010/07/Toolbar-WithDisabled.png?resize=106%2C35" alt="" data-recalc-dims="1" />  
*Save/Clear disabled because there are no images *

<img class="alignnone size-full wp-image-122" title="Toolbar-AllEnabled" src="http://i2.wp.com/hansen.azurewebsites.net/wp-content/uploads/2010/07/Toolbar-AllEnabled.png?resize=102%2C36" alt="" data-recalc-dims="1" />  
*All buttons enabled*

<img class="alignnone size-full wp-image-123" title="Toolbar-MouseOver" src="http://i1.wp.com/hansen.azurewebsites.net/wp-content/uploads/2010/07/Toolbar-MouseOver.png?resize=103%2C33" alt="" data-recalc-dims="1" />  
*MouseOver Save button*

<pre class="brush: xml">&lt;Style TargetType="Button"&gt;
        &lt;Setter Property="Template"&gt;
            &lt;Setter.Value&gt;
                &lt;ControlTemplate TargetType="Button"&gt;
                    &lt;Grid Margin="1"&gt;
                        &lt;Rectangle x:Name="OuterBorder" RadiusY="2" RadiusX="2" Visibility="Collapsed"/&gt;
                        &lt;Rectangle x:Name="Bg" Fill="{TemplateBinding Background}" Margin="1" RadiusY="1" RadiusX="1" Stroke="{TemplateBinding BorderBrush}" StrokeThickness="1" Visibility="Collapsed"/&gt;
                        &lt;Rectangle x:Name="InnerBorder" Margin="2" Visibility="Collapsed"/&gt;
                        &lt;ContentPresenter Margin="5" VerticalAlignment="Center" /&gt;
                    &lt;/Grid&gt;
                    &lt;ControlTemplate.Triggers&gt;
                        &lt;Trigger Property="IsMouseOver" Value="True"&gt;
                            &lt;Setter Property="Visibility" TargetName="OuterBorder" Value="Visible"/&gt;
                            &lt;Setter Property="Visibility" TargetName="Bg" Value="Visible"/&gt;
                            &lt;Setter Property="Visibility" TargetName="InnerBorder" Value="Visible"/&gt;
                        &lt;/Trigger&gt;
                        &lt;Trigger Property="IsEnabled" Value="False"&gt;
                            &lt;Setter Property="Effect"&gt;
                                &lt;Setter.Value&gt;
                                    &lt;effects:GreyscaleEffect /&gt;
                                &lt;/Setter.Value&gt;
                            &lt;/Setter&gt;
                            &lt;Setter Property="Opacity" Value=".5" /&gt;
                        &lt;/Trigger&gt;
                    &lt;/ControlTemplate.Triggers&gt;
                &lt;/ControlTemplate&gt;
            &lt;/Setter.Value&gt;
        &lt;/Setter&gt;
    &lt;/Style&gt;</pre>

And the following .fx code is used for the greyscale effect.

<pre>sampler2D  ImageSampler : register(S0);  //take ImageSampler from S0 register. 

// 'uv' vector from TEXCOORD0 semantics is our texture coordinate, two floating point numbers in the range 0-1.
float4 PS( float2 uv : TEXCOORD) : COLOR
{
    float4 color = tex2D( ImageSampler, uv); // get the color of texture at the current point
    color.rgb = dot(color.rgb, float3(0.3, 0.59, 0.11)); //compose correct luminance value
    return color;
}</pre>

[Browse the latest source][2]

<div class="sharedaddy sd-sharing-enabled">
  <div class="robots-nocontent sd-block sd-social sd-social-official sd-sharing">
    <h3 class="sd-title">
      Share this:
    </h3>
    
    <div class="sd-content">
      <ul>
        <li class="share-email">
          <a rel="nofollow" class="share-email sd-button" href="http://xiu.shoeke.com/2010/07/16/wpf-image-buttons/?share=email" target="_blank" title="Click to email this to a friend"><span>Email</span></a>
        </li>
        <li class="share-twitter">
          <div class="twitter_button">
          </div>
        </li>
        
        <li class="share-google-plus-1">
          <div class="googleplus1_button">
            <div class="g-plus" data-action="share" data-annotation="bubble" data-href="http://xiu.shoeke.com/2010/07/16/wpf-image-buttons/">
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

 [1]: http://resizer.codeplex.com/
 [2]: http://resizer.codeplex.com/SourceControl/BrowseLatest "Browse Latest"