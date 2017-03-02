---
layout: post
title:  "Browser Testing met Laravel Dusk in 5.4"
date:   2017-03-02
categories: laravel
author: jorijn
cover: /images/covers/posts/browser-testing-met-laravel-dusk-in-54.jpg # Header cover [optional]
image: /images/covers/posts/browser-testing-met-laravel-dusk-in-54.jpg # Used by Twitter Cards and Open Graph [optional]
---

[Dusk](https://laravel.com/docs/5.4/dusk) is een component wat nieuw is in Laravel 5.4. Het versimpeld de manier waarop wij als ontwikkelaars Browser Tests kunnen uitvoeren.

## Waarom
Het lijkt me een goede stap om dit als extra vangnet te kunnen implementeren. In de ideale wereld zou je 100% test-coverage willen hebben met wat simpelere Unit Tests en Feature Tests maar steeds vaker worden applicaties opgebouwd met complexe JavaScript aan de voorkant zoals AngularJS, ReactJS of Vue.js.

## De valkuil met Unit Tests
Unit Tests zijn waarvoor ze bedoeld zijn erg goed - het puntsgewijs testen van functies. “Als ik er X in stop, moet er Y uitkomen”. Dit kan ik meten aan de PHP/back-end kant, maar wat als ik wil meten: “Ik vul een foutief e-mail adres in en er moet een rood kader omheen komen.”

Het lijkt simpel, maar hiervoor is daadwerkelijke rendering nodig aan de zeide van een client: Browser Tests.

## De technische “Hoe”
Zoals bijna alles met Laravel, de syntax is duidelijk en eenvoudig te onthouden. Ik zal hieronder de stappen omschrijven die benodigd zijn Dusk draaiende te krijgen.

### Installatie
_Dit is een summiere beschrijving van hetgeen te vinden op de [documentatiepagina](https://laravel.com/docs/5.4/dusk) van Laravel Dusk. Ik ga er vanuit dat er reeds een werkende Laravel applicatie staat._

Om te beginnen, dienen we het composer component `laravel/dusk` op te nemen in ons project.

{% highlight bash %}
$ composer require laravel/dusk
{% endhighlight %}

Zodra deze geïnstalleerd is, moeten we de ServiceProvider registreren in de applicatie. Een goede plek om deze te registreren is in de `AppServiceProvider` in de methode `register`.

{% highlight php %}
<?php
use Laravel\Dusk\DuskServiceProvider;

/**
 * Register any application services.
 *
 * @return void
 */
public function register()
{
    if ($this->app->environment('local', 'testing')) {
        $this->app->register(DuskServiceProvider::class);
    }
}
{% endhighlight %}

Om vervolgens de mappenstructuur correct aan te maken op de schijf voer je dit commando uit:

{% highlight bash %}
$ php artisan dusk:install
{% endhighlight %}

Zorg er voor dat in het configuratiebestand `.env` de `APP_URL` correct staat ingesteld naar de locatie van je applicatie. Dat is in mijn geval `https://browsertest-test.app/`.

### De testcase: Inloggen
Maak op de commandline een nieuwe test aan:

{% highlight bash %}
$ php artisan dusk:make LoginTest
{% endhighlight %}

Deze is nu geplaatst in de map `tests/Browser`. Wat ik wil gaan doen in deze test:

* Een gebruiker maken met e-mail adres test@jorijn.com
* Testen of ik kan inloggen met deze gebruiker via de browser
* De aangemaakte gebruiker verwijderen

Voeg deze functie toe aan de nieuw aangemaakte test:

{% highlight php %}
<?php

public function testLogin()
{
  $user = factory(\App\User::class)->create([
    'email' => 'test@jorijn.com',
  ]);

  $this->browse(function ($browser) use ($user) {
      $browser->visit('/login')
              ->type('email', $user->email)
              ->type('password', 'secret')
              ->press('Login')
              ->assertPathIs('/home');
  });

  $user->delete();
}
{% endhighlight %}

Draai nu vervolgens met Artisan het Dusk commando:

{% highlight bash %}
$ php artisan dusk
{% endhighlight %}

Als alles goed gegaan is zie je nu dat er een nieuw Chrome venster opent die geheel geautomatiseerd deze handelingen uitvoert.

![Laravel Dusk in de Terminal](/uploads/2017/03/browser-testing-laravel-dusk-terminal.png "Laravel Dusk in de Terminal")

## Conclusie
Laravel Dusk is een eenvoudige manier om op een snelle manier een toch relatief grote set aan functionaliteit te testen. Dit is een goede manier om op de machine van de developer functionaliteit te kunnen testen. In een volgend artikel wil ik het aspect van headless testen met bijvoorbeeld PhantomJS toelichten. 
