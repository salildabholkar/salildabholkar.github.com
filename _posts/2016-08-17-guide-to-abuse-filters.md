---
layout: post
title: "Guide to Abuse Filters"
description: "Salil teaches you the basics of AbuseFilters and shares his experience of working with them over the years."
tagline: "Gotta Catch 'Em All"
category: guides
tags: [wikia, mediawiki, guide]
keywords: AbuseFilter, abuse filter, wikia, mediawiki, guide
---
{% include JB/setup %}

[Abuse Filters](https://www.mediawiki.org/wiki/Extension:AbuseFilter) are used in a mediawiki environment to prevent certain pre-defined actions. The filter can then be configured to take specific actions against the user. This guide teaches you how to create new filters and configure them.
<!--more-->

This guide assumes you already have installed the AbuseFilter extension on your mediawiki instance. It is recommended you also install the [AntiSpoof extension](https://www.mediawiki.org/wiki/Extension:AntiSpoof) to use string normalization features.

## Important pages
It is important to familiarize yourself with all the weapons that AbuseFilter provides you with:

+ **Special:AbuseFilter:** This is your main command center for creating and modifying filters for your wiki.
+ **Special:AbuseLog:** This is the log of all actions performed by the filters on your wiki.
+ **Special:AbuseFilter/test:** This page allows you to check a filter code entered in the box against the last 100 changes. You can also load an existing filter by its ID.
