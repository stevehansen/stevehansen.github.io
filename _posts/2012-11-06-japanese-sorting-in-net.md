---
title: Japanese sorting in .NET
author: Steve Hansen
layout: post
permalink: /2012/11/06/japanese-sorting-in-net/
tags:
  - Japanese
---
As you know I have my little test site on Appharbor  <http://vidyano.apphb.com/#!/KanjiOverview>

The Kanji data came from a SQL server database with an order by on the Kanji character. But once I cached the query (automatically refreshed every 30 minutes) the order was completely different. It seems that ordering and unicode don&#8217;t really match, apparently Japanese doesn&#8217;t really have a fixed (or at least a single) way of ordering their characters. And now because the order by was happening in .NET it gave me different results.

The only thing I could find was using special comparers, all linked to the ja-JP culture. But then it hit me, my current thread&#8217;s culture was already set to **ja-JP** because I was playing with the Japanese date format. Changing the thread back to **en-US** gave my back the same results as before.

The order is now uses is by radical and then stroke count which makes it easy to see the related/same kanji.

Does anyone know what order the Japanese culture info uses?