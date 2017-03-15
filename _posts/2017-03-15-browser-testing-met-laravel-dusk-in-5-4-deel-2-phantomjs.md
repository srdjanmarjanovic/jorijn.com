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