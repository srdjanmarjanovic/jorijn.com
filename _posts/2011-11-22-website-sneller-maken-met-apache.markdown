---
layout: post
title:  "Scripts en styling samenvoegen met Apache"
date:   2011-11-22
categories:
author: jorijn
cover: /images/covers/posts/website-sneller-maken-met-apache.jpg # Header cover [optional]
image: /images/covers/posts/website-sneller-maken-met-apache.jpg # Used by Twitter Cards and Open Graph [optional]
excerpt: Moderne browsers staan er om bekend om slechts vier gelijktijdige requests naar een domein uit te voeren. In theorie is dit voldoende, maar in de praktijk blijkt dit er vaak voor te zorgen dat een website trager wordt dan nodig.
---

_Dit is een oud bericht, wat er in staat kan mogelijk niet functioneren._

Moderne browsers staan er om bekend om slechts vier gelijktijdige requests naar een domein uit te voeren. In theorie is dit voldoende, maar in de praktijk blijkt dit er vaak voor te zorgen dat een website trager wordt dan nodig.

## Een voorbeeld

{% highlight html %}
<!-- javascripts -->
<script src="jquery.js"></script>
<script src="website.js"></script>
<script src="jquery.fancybox-1.3.4.pack.js"></script>
<script src="jquery.mousewheel-3.0.4.pack.js"></script>
{% endhighlight %}

{% highlight html %}
<!-- styles -->
<link rel="stylesheet" href="reset.css">
<link rel="stylesheet" href="website.css">
<link rel="stylesheet" href="jquery.fancybox-1.3.4.css">

{% endhighlight %}

De browser zal de eerste vier scripts ophalen en wachten tot deze zijn gedownload voordat de browser verder gaat met de styling en andere scripts. Alle bestanden op dit domein tellen mee voor dit limiet.

## Hoe verbeteren we dit?

Buiten kijken welke afhankelijkheden en assets noodzakelijk zijn, is er een quick-fix mogelijk. Open `.htaccess` en voeg het onderstaande toe:

{% highlight apache %}
<FilesMatch "\.combined\.(js|css)$">
        Options +Includes
        SetOutputFilter INCLUDES
</FilesMatch>
{% endhighlight %}

Nu, maak een bestand met de naam `scripts.combined.js` met de volgende inhoud:

{% highlight apache %}
<!--#include file="libraries/jquery-1.7.min.js" -->
<!--#include file="custom/script1.js" -->
<!--#include file="custom/script2.js" -->
<!--#include file="custom/script3.js" -->
<!--#include file="custom/script4.js" -->
{% endhighlight %}

Apache zal nu al deze bestanden onder elkaar plakken en voor de bezoeker is er enkel nog één bestand.
