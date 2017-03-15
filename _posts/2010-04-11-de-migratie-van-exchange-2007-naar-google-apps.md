---
layout: post
title:  "De migratie van Exchange 2007 naar Google Apps"
date:   2010-04-11 10:18:00
categories: legacy google-apps
author: jorijn
cover: /images/covers/posts/de-migratie-van-exchange-2007-naar-google-apps.jpg # Header cover [optional]
image: /images/covers/posts/de-migratie-van-exchange-2007-naar-google-apps.jpg # Used by Twitter Cards and Open Graph [optional]
---

Op het moment van schrijven werk(te) ik bij Rhinofly. Dit is een bedrijf van bijna 50 werknemers groot en met zijn allen hebben wij bijna een half miljoen e-mail berichten opgeslagen op onze Exchange 2007 server. Dit komt neer een gemiddeld aantal van 10.000 e-mail berichten per persoon.

E-mail wordt veelal gebruikt als een grote bak met communicatie. Gestructureerd bijhouden kost een hoop tijd en schiet er bij in. Dit vertaald zichzelf bij Rhinofly door tot een wekelijkse systeem back-up ten grootte van 231 GB aan data. Exchange kwam vanaf versie 2003 met een back-up tool genaamd ntbackup.exe. Je kan er back-ups mee maken maar daar is eigenlijk alles mee gezegd. Ik denk dat een enkele mailbox herstellen een nachtmerrie zou zijn voor iedere systeembeheerder.

De beslissing om te migreren van Exchange naar Google Apps ligt in een aantal factoren, waarin voornamelijk kosten (licentiekosten v.s. 40 euro per gebruiker per jaar), gebruiks- en beheergemak. Taken zoals urenregistratie en projectmanagement sluiten ook goed aan op de API’s van Google Apps.

Dit project is onderdeel van een groter project om EBS (Essential Business Server) uit te faseren en daar in plaats open source oplossingen te implementeren. Samba 4 is op dit moment goed op weg om een allround oplossing te bieden voor een Active Directory inclusief DHCP, achterliggend LDAP en DDNS updates. Stap 1 was onze Exchange 2007 server uit het plaatje zien te krijgen en daarvoor in ruil Google Apps aan te nemen. Het project is erg leerzaam geweest en met dit bericht wil ik enkele punten toelichten die ik onderweg ben tegen gekomen.

# Communicatie vooraf
Veranderingen zijn eng, zeker als het één van de balangrijkste elementen in je productiviteit is. Uitgebreid communiceren vooraf neemt een deel van de angst weg doordat men weet wat er komen gaat. Leg uit wat de voordelen en veranderingen zijn en voornamelijk op welke termijn het allemaal gaat gebeuren.

# Afhankelijkheden?
Voordat alle e-mail geüpload kan worden naar Google komen er nog een heleboel dingen kijken. De Outlook extensie vereist namelijk ook een aantal dingen van je computer, bijvoorbeeld minimaal SP3 van Office 2003 en SP2 van Office 2007.

Je bent vrij om Google Apps Premier edition te proberen voor een proefperiode van 30 dagen. Wees wel bewust van het feit dat Google het bedrag voor het aantal gebruikers alvast reserveert op de creditcard. Deze 30 dagen betekenen dat er vooraf duidelijke afspraken moeten zijn over een testfase en voldoende evaluatiemomenten in het geval dat er wordt afgezien van het plan.

# De bestaande userbase
De meeste bedrijven hebben hun userbase staan in de vorm van een Active Directory. Het is belangrijk om tijdig te testen met synchronisatie hiervan. Google’s oplossing hiervoor met de naam Google Apps Directory Sync neemt dingen zoals gebruikers, distributiegroepen en gedeelde contacten mee. Over het algemeen wil je zoeken op (objectClass=user) met als filter de OU met de testpersonen hierin.

# Bestaande e-mail
Het correct meenemen van de bestaande e-mail is misschien nog wel het meest belangrijke in dit project. Wij maakte gebruikt van Google Apps Migration for Microsoft Exchange. Dit programma upload e-mail van geselecteerde gebruikers uit een IMAP server, een map met PST bestanden of (hosted) Exchange 2003 en 2007. Het probleem wat wij maakte is er vanuit gaan dat dit programma een soort synchronisatie zou bieden. Helaas bleek dit niet waar en moet de term migratie erg serieus genomen worden. De veronderstelling dat vooraf alvast wat e-mail te uploaden op maandag en de laatste batch in het weekend doen bleek er voor te zorgen dat alle e-mail status wijzigingen sinds maandag niet meegenomen waren. Denk hierbij dus aan status Inbox naar Verwijderde items.

In ons bedrijf hebben mensen mailboxen met de meest complexe map structuren. Hoewel de migratietool voor Exchange map niveau’s tot 250 karakters diep toe laat, mag een label in Google Mail slechts 40 karakters lang zijn. Bij lange/map/structuren/met/meer/dan/40-karakters/ gaat dit dus aanvankelijk goed, maar deze naam kan later door de controle in de webmail interface niet aangepast worden. Attendeer de gebruikers er dus op dat herconstructie nodig is. In combinatie met de labs plugin “Nested labels” zijn mappen nog wel mogelijk.

# Telefoons
Google biedt met caldav, carddav, imap, pop3, syncml, etc. voldoende mogelijkheden aan om e-mail, contactpersonen en agenda afspraken op de telefoon te laten verschijnen. Blackberry is daarentegen altijd al een ander verhaal geweest. De migratie van Exchange naar Google Apps heeft bij Rhinofly veel vertraging opgelopen omdat we moesten wachten op de release van Google Apps Connector for Blackberry Express Server. Dit is een tool die het mogelijk maakt voor Blackberry Server om met Google Apps te praten.

De conclusie uiteindelijk is dat Google Apps hedendaags een volledige oplossing is ter vervanging van Exchange. Sommige tools staan helaas nog in kinderschoenen en soms kwamen er nog wat bugs tevoorschijn. Rhinofly draait nu drie weken op Google Apps en het is goed om te zien dat er verschillende mensen die Outlook vaarwel hebben gezegd en hun werk in de online suite van Google doen.
