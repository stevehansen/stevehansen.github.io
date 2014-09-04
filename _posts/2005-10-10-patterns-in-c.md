---
title: 'Patterns in C#'
author: Steve Hansen
layout: post
permalink: /2005/10/10/patterns-in-c/
---
Just finished the first 4 chapters for school, converted all the code to C# and well I have to admit that I used more patterns before then I realized.

One of the patterns that I don&#8217;t really like is the Singleton, well I have nothing against it, but if you start a new class with the singleton in mind you can use a static class instead, it&#8217;s easier to access Class.Method() instead of something like Class.Default.Method(), but if you have to convert an existing class it can be easier to make a singleton:

*   Make constructor private so no other class can call it
*   Keep a static field from the same type
*   Use a static public property to access the field (and create it if it&#8217;s still null)

But I just love the Strategy in combination with a Factory. Use the strategy to build the class hierachy and then use the Factory to get an instance to them.