---
layout: post
title:  "Werken met ITIL: Het opzetten van een CMDB"
date:   2012-02-29
categories:
author: jorijn
cover: /images/covers/posts/werken-met-itil-opzetten-cmdb.jpg # Header cover [optional]
image: /images/covers/posts/werken-met-itil-opzetten-cmdb.jpg # Used by Twitter Cards and Open Graph [optional]
---

In mijn dienstverband bij Rhinofly heb ik een aantal mooie dingen gedaan. Eén van de producten waar wij beide erg blij mee zijn is de CMDB.

De afkorting CMDB staat voor _Configuration Management Database_.

## CMDB?
Dit is een database waarin alles met betrekking tot configuratie wordt bijgehouden en beheert. Ieder bedrijf dat groeit en producten levert met betrekking tot het internet heeft IT infrastructuur. Dit kunnen simpele dingen zijn zoals domeinnamen en werkstations maar ook servers, applicaties en klanten komen hierin terug. In de startfases van een bedrijf zul je zien dat zaken zoals Access databases en Excell sheets voldoen aan de basis behoefte om te beheren. Bij Rhinofly kwam het besef dat dit uit zijn voegen aan het groeien was, er was iets beters nodig.

## Hoe het product tot stand kwam
Bij Rhinofly was ik aangenomen met de functie Systeembeheerder. Met mijn achtergrond als programmeur ontstond al snel het idee om een portaal tot bestaan te brengen waarin alle genoemde factoren aan elkaar gebonden waren. Zo moest het mogelijk zijn om DNS aanpassingen vanuit het zelfde systeem te doen en in één oog opslag te zien welke servers vol waren en welke er nog voldoende resources hadden.

## Beveiliging
Het is voor iedereen en vooral bedrijven een eng idee om gevoelige informatie centraal op te slaan en enkel achter een gebruikersnaam en een wachtwoord te bewaren. Hiervoor is er besloten om handen ineen te slaan met *YubiKey*. De YubiKey is een sleutel aan je sleutelbos die er uit ziet als een normale USB stick. Het verschil is echter: Je legt een vinger bovenop de knop en door middel van “Two Factor Authentification” word je ingelogd in een systeem. Dit houdt in het kort in dat met een iedere keer uniek gegenereerde sleutel verificatie wordt uitgevoerd op een centrale authentificatie server.

Indien de sleutel verloren is, word de machtiging op de sleutel ingetrokken en kan deze niet meer worden gebruikt om in te loggen. Deze methode elimineert het probleem om complexe wachtwoorden te onthouden en biedt centraal beheer over wie toegang heeft.

## Vindbaarheid
Zodra je grote hoeveelheden data gaat bewaren is het kunst om deze op een zo’n prettig mogelijke manier te presenteren en doorzoekbaar te maken. Ik heb afgekeken bij Google Mail een soort gelijke manier toegepast. Om alle .NL domeinnamen te zoeken kan de gebruiker bijvoorbeeld op `.nl in:domains` zoeken. Om alle servers in 10.0.0.0/24 te weergeven zoekt de gebruiker enkel op `10.0.0 in:servers`.

## Conclusie
Gestructureerd beheer van informatie is belangrijk om er voor te zorgen dat hier efficiënt gewerkt mee kan worden. Ik hoop dat ik met een greep uit de functionaliteit van dit systeem heb kunnen laten zien dat dit haalbaar is met relatief simpele technologieën.
