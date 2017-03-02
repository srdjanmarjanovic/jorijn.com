---
layout: post
title:  "Een WordPress “shortcode” gebruiken in een widget"
date:   2013-02-01
categories:
author: jorijn
cover: /images/covers/posts/wordpress-shortcode-gebruiken-in-een-widget.jpg # Header cover [optional]
image: /images/covers/posts/wordpress-shortcode-gebruiken-in-een-widget.jpg # Used by Twitter Cards and Open Graph [optional]
---

Voor één van de projecten waar ik nu mee bezig ben wilde ik in het kader van flexibiliteit het gebruik van shortcodes toestaan in een widget. Een shortcode ziet ongeveer zo uit:

{% highlight text %}
[naam_van_de_shortcode argument="waarde"]
{% endhighlight %}

Ik was verbaasd om er achter te komen dat dit standaard niet kon in WordPress. Gelukkig is het vrij makkelijk om hierop in te haken met een filter en action-hook.

{% highlight php %}
<?php add_filter('widget_text', 'do_shortcode'); ?>
{% endhighlight %}

Als dit ergens in het functions.php bestand geplaatst zal het werken zoals gewenst.
