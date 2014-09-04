---
title: Azure Websites support .NET 4.5
author: Steve Hansen
layout: post
permalink: /2012/10/30/azure-websites-support-net-4-5/
tags:
  - .NET 4.5
  - Vidyano
  - Windows Azure
---
Unless you&#8217;ve been living under a rock you&#8217;ll have heard about the Azure Websites that&#8217;s available from Microsoft. You can start by using a shared environment and then scale as traffic grows.

Scott Hanselman has confirmed that they now support ASP.NET 4.5, giving better performance for all websites hosted on it, even those deployed and build for .NET 4.0.

Vidyano also benefits from this as we make use of Entity Framework which got some really great performance improvements in .NET 4.5 (all query parsing is cached now).

More info: <https://www.windowsazure.com/en-us/home/scenarios/web-sites/>