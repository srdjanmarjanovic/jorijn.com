---
layout: post
title:  "Laravel 5.4: Specified key was too long error"
date:   2017-03-02
categories: laravel
author: jorijn
cover: /images/covers/posts/laravel54-specified-key-was-too-long-error.jpg # Header cover [optional]
image: /images/covers/posts/laravel54-specified-key-was-too-long-error.jpg # Used by Twitter Cards and Open Graph [optional]
---

Tijdens het in gebruik nemen van Laravel 5.4 liep ik er tegenaan dat per deze versie standaard gebruik maken van de database karakter set `utf8mb4` (en dus standaard emojis ondersteunen! 😀)

Als je MySQL draait vanaf versie v5.7.7 zul je hier niets van merken, echter indien je gebruik maakt van MariaDB of een wat oudere versie van MySQL loop je mogelijkerwijs tegen deze fouten aan:

> [Illuminate\Database\QueryException]
> SQLSTATE[42000]: Syntax error or access violation: 1071 Specified key was too long; max key length is 767 bytes (SQL: alter table users add unique users_email_unique(email))
>
> [PDOException]
> SQLSTATE[42000]: Syntax error or access violation: 1071 Specified key was too long; max key length is 767 bytes

Logisch ook, een multibyte karakter neemt meer ruimte in dan zijn standaard tegenhanger: `utf8`.

In de [upgrade guide](https://laravel.com/docs/master/migrations#creating-indexes) van Laravel hebben ze hier al iets over geschreven: Pas in de `boot` methode van je `AppServiceProvider.php` bestand de standaard sleutel lengte aan:

```php?start_inline=true
use Illuminate\Support\Facades\Schema;

public function boot()
{
    Schema::defaultStringLength(191);
}
```
