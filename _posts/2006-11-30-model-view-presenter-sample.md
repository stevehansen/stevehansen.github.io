---
title: Model-View-Presenter Sample
author: Steve Hansen
layout: post
permalink: /2006/11/30/model-view-presenter-sample/
tags:
  - Design Patterns
---
Here is a small part of my Demo that I&#8217;m creating. It is actually a second Presenter with Model and View that are used when you want to import something (the demo will follow so don&#8217;t worry :smile: ).It gives a good view of how I&#8217;m implementing the MVP pattern.

<p style="text-align: center">
  <img alt="Import MVP Class Diagram" title="Import MVP Class Diagram" src="https://i0.wp.com/xiu.shoeke.com/images/ImportClassDiagram.png?w=625" data-recalc-dims="1" />
</p>

As you can see my Model exists only of methods to get data. My view exists of only events. The presenter has 1 public constructor which takes an IImportModel and IImportView instance. The constructor calls the *SetUpView* method which will bind all the View&#8217;s events to the private methods (*ViewAdd*, *ViewClosing*, *ViewLoadFeed*). The Closing event is an easy feature (WinForms already have this event anyway) which allows me to clean up everything. That&#8217;s why the Model also implements the IDisposable interface. So when the view is closed the presenter will call the *Dispose* method on the Model which can then close the database connection, file or &#8230;