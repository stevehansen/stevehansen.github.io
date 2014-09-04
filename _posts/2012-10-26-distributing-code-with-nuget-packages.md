---
title: Distributing code with NuGet packages
author: Steve Hansen
layout: post
permalink: /2012/10/26/distributing-code-with-nuget-packages/
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