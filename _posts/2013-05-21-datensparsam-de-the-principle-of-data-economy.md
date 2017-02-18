---
layout: post
title: Datensparsam.de & the Principle of Data Economy
permalink: principle-data-economy/
description: The 1st Principle of Data Economy - With Datensparsam.de I established Germany's first civic app focussing on the first principle of data economy.
image: http://lorempixel.com/600/300/people
---

The [Datensparsam.de](https://www.datensparsam.de) form generator helps people to easily opt out at their registration offices. Here I'd like to write some words about the hows and whys that led to the final web app...

## Data Economy at Registration Offices

Internationally, Germany is often referred to as a country full of strong privacy groups and citizens having some kind of a generic bias against all kinds of _post privacy_ and private data liberality. Nevertheless, there is a huge lack of privacy thinking in one of Germany's official laws: The _compulsory registration_ and the communal system of registration!

The problem I see is that registration offices in Germany often sell the private datasets of their citizens to address traders and political parties, companies or further interested parties. In my eyes that's in fact a scandal!

## Opt-Out at Registration Offices

However, the Federal Republic of Germany wouldn't be a democratic republic without any chance of raising an objection. In fact, German citizens are legally allowed to opt out at their local, communal registration offices, but of course this (for some people) is quite an obstacle.

To simplify the process and the flatten possible obstacles, I created [Datensparsam.de](https://www.datensparsam.de). Inspired by Chaos Computer Club Mainz/ Wiesbaden and their post on the [principle of data economy](http://www.cccmz.de/datensparsamkeit/), I started working on this project during the international __Open Data Hackday 2013__ in Berlin.

## Python, Django, Tastypie

After discussing several possible ways of implementing such an form generator, I came up with a somehow classic technology stack using the [Django web-framework](https://www.djangoproject.com/) for Python, [Tastypie](https://github.com/toastdriven/django-tastypie) for a clean and simple API and [Bootstrap](http://twitter.github.io/bootstrap/index.html) for the frontend.

In the end, the entire technology thing was not the central problem. Much harder was to find, scrape, combine and clean the required data about zip-codes and registration office addresses. The reason for that is, that there (still) are no central/ offical platforms in Germany providing all official addresses or datasets about the n2m relations between zip-codes and municipalities.

Working on [Datensparsam.de](https://www.datensparsam.de) showed me that there's a strong need of open governmental data in Germany. So hands on and free data!
