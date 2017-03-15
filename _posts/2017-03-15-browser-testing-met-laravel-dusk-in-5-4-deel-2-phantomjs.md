---
layout: post
title: 'Browser Testing met Laravel Dusk: Deel 2 — PhantomJS'
categories: laravel
author: jorijn
cover: /images/covers/posts/browser-testing-met-laravel-dusk-in-5-4-deel-2-phantomjs.jpg # Header cover [optional]
image: /images/covers/posts/browser-testing-met-laravel-dusk-in-5-4-deel-2-phantomjs.jpg # Used by Twitter Cards and Open Graph [optional]
---

In het vorige deel [schreef ik](/browser-testing-met-laravel-dusk-in-54/) hoe je Browser Testing kan doen met Laravel Dusk (5.4+). Hiervoor gebruikte ik de Chrome Driver maar het nadeel hierbij is dat op de computer waarop je deze tests uitvoert, Chrome geïnstalleerd moet staan. Nu is dit in ontwikkeling voldoende, maar in omgevingen als acceptatie en productie wil je dat dit *headless* kan gebeuren. Dit betekend testen op de achtergrond zonder dat er schermen openen. Uitstekend voor servers zonder aanwezige GUI.

## PhantomJS
> PhantomJS is a headless WebKit scriptable with a JavaScript API. It has fast and native support for various web standards: DOM handling, CSS selector, JSON, Canvas, and SVG.

PhantomJS is een programma wat (eventueel) op de achtergrond draait en het [Webdriver protocol](http://www.seleniumhq.org/docs/03_webdriver.jsp) spreekt. Laravel kan hiermee communiceren.

Installeren van PhantomJS: [phantomjs.org/download.html](http://phantomjs.org/download.html)

### Installatieinstructies voor Mac OS X
Voor andere platforme, zie bovenstaande link.

Voor Mac OS X: Download de release naar een nieuwe map en pak het bestand uit:

```bash
$ wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-macosx.zip
$ unzip phantomjs-2.1.1-macosx.zip
$ cd phantomjs-2.1.1-macosx
```

### Uitvoeren

Je kan nu PhantomJS starten in webdriver-mode met het volgende commando:

```bash
$ ./bin/phantomjs --webdriver=4444
```

Vervolgens open je het bestand: `tests/DuskTestCase.php` en verander je de gewenste driver naar:

```php?start_inline=true
/**
 * Create the RemoteWebDriver instance.
 *
 * @return \Facebook\WebDriver\Remote\RemoteWebDriver
 */
protected function driver()
{
    return RemoteWebDriver::create(
        'http://localhost:4444', DesiredCapabilities::phantomjs()
    );
}
```

Draai nu opnieuw in een andere tab de test:

```bash
$ php artisan dusk
```

Het resultaat is — *als het goed is* — geslaagde tests zonder een nieuw Chrome venster.
 
![Laravel Dusk op PhantomJS in de Terminal](/uploads/2017/03/browser-testing-laravel-dusk-terminal-phantomjs.png "Laravel Dusk op PhantomJS in de Terminal")

## Conclusie

Deze opzet is bij zeer geschikt om in productie continue te blijven testen of functionaliteit blijft werken zoals het hoort. Ook kun je het inprikken op een process als CI om een (VCS) build af te keuren als alle tests niet slagen. 