---
title: Anime
author: Steve Hansen
layout: page
permalink: /anime/
nav: true
comments: true
---
{% for anime in site.data.anime %}<p>
 <a href="http://anidb.net/perl-bin/animedb.pl?show=anime&aid={{anime.aid}}" target="_blank" {% if anime.finished %}class="finished" title="Finished"{% else %}title="Watching"{% endif %}><img src="/images/{{anime.image}}" width="50">&nbsp;&nbsp;{{anime.name}}{% if anime.japanese %} aka {{anime.japanese}}{% endif %}</a>
</p>
{% endfor %}