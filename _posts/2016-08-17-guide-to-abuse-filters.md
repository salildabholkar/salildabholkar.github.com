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

## What are AbuseFilters?
The AbuseFilter is a tool that allows trusted editors on the wiki (usually sysops) to set controls mainly to address common patterns of harmful editing. It automatically compares every edit made against sets of conditions that are defined in user-created filters. If an edit matches the conditions of a filter, that filter will respond by logging the edit. It may also tag the edit summary, warn the editor, revoke his/her autoconfirmed status, and/or disallow the edit entirely. <sup>[[wikipedia](https://en.wikipedia.org/wiki/Wikipedia:Edit_filter)]</sup>

## Important pages
It is important to familiarize yourself with all the weapons that AbuseFilter provides you with:

+ **Special:AbuseFilter:** This is your main command center for creating and modifying filters for your wiki.
+ **Special:AbuseLog:** This is the log of all actions performed by the filters on your wiki.
+ **Special:AbuseFilter/test:** This page allows you to check a filter code entered in the box against the last 100 changes. You can also load an existing filter by its ID.
+ **Special:AbuseFilter/tools:** This page provides you with some tools which may be useful in formulating and debugging abuse filters.
+ **Special:AbuseFilter/import:** You can use this page to import public filters from other wikis.
+ **Special:AbuseFilter/new:** Allows you to create a new filter.


## AbuseFilter basics

### The AbuseFilter dashboard
When you navigate to **Special:AbuseFilter** on your wiki, you will see all the filters added on your wiki in a tabular format.  
This includes the Filter ID, decription, actions it will perform, its current status, last modification date, visibility and total hits.
Here is a screenshot for better understanding:
![Special:AbuseFilter page on Narutopedia](/assets/images/AF.PNG "Special:AbuseFilter page on Narutopedia")

### Inside each filter
You can click on a filter's ID or description to enter the filter. Every filter consists of two sections:

+ **Filter parameters:** Consists largely of the same Information you get from the dashboard as well as the code for the filter and any notes made by the author.
+ **Actions taken when matched:** Consists of various flags which control what actions should the filter take if an edit matches the rules set for the filter.

### The Log page
xyz


## Coding AbuseFilters

### Private vs Public Filters


## Commonly used filters
Over the years, I have come across and created several AbuseFilters for many wikis. Here are some of my favorites.
Added comments for ease of understanding:

### Large content removal (> 900 characters)
Perhaps the most commons usage of an AbuseFilter is to detect large removal of content from pages.
We need to specify a threshold to determine what we consider as *"large"*. For this example we consider it as 900 characters.

```c
/* Not autoconfirmed */
!("autoconfirmed" in user_groups) &

/* 0 means articles (mainspace) */
(article_namespace == 0) &

/* 900+ removed */
(edit_delta < -900) &

/* allow to turn it into a redirect or delete it */
!("#redirect" in lcase(added_lines)) & !(action == "delete")
```

**Notes:** You can detect complete blanking by using `new_size == 0` in the third line instead.

### Shouting (CAPS)
Shouting is when a user types in all caps (SOMETHING LIKE THIS IS SHOUTING). Some users have the impression that shouting will help them get their comments across faster.
But it can be very annoying for other users and might hide some legitimate comments in their noise.

```c
/* Not autoconfirmed */
! ("autoconfirmed" in user_groups)

/* User added something */
& length(added_lines) > 1

/* Redirect in caps is alright */
&  !"#REDIRECT" in added_lines

/* Detect caps from A to Z repeated 10 times */
& added_lines rlike "[A-Z\s']{10}"
```
**Notes:** You might want to restrict this filter only to "talk namespaces" like user and article talkpages or threads.

### Creation of other user's userpages
Userpages are common places for vandalism or "revenge" against specific users.
Sometimes user mistakenly use another user's userpage instead of talkpage.

```c
/* Editing */
action == "edit" &

/* Creation of the page */
article_articleid == 0 &

/* Not sysop */
!("sysop" in user_groups) &

/* Userpage */
article_namespace == 2 &

/* Subpages are fine */
!("/" in article_text) &

/* Allow user to create his own userpage */
user_name != article_text
```

### Common profanity
One of the most common problems faced by wikis is the use of profanity. AbuseFilters can be used to automatically detect and prevent most of the profanity. The below filter is used privately across a wide range of wikis and hence I am posting a highly edited version with most "bad words" removed.

```c
/* variable filter1 contains words that should not appear, within a word or otherwise */
filter1:="(beastiality|bio?tch|bastard|faget|tits|[wp][e3]n[li\!][5s]|v[a@]gina|fuck|ass(goblin|bandit|hat|c[lr]own|(w?hole|lick(er)?|wipe)\s)";

/* variable filter2 contains words that should not appear standalone */
filter2:="(?<!\w)(n(e|i)g(g|)(a|er|ro)\s|fuk\s|fart(ing|\s|)|va(j|g)\s|rap(e|ist)(ing|s|d|r|)|bunghole\s|twat\s|blue( |)waffle\s|puss(a|)(y|ies)|perv(ing|)|shat|pimp|chode(stroker)\s|sperm|semen|hooker\s|prostitute\s|pubic( |)hair|boner\s|chode\s)(?!\w)";

/* Not for autoconfirmed */
(!("autoconfirmed" in user_groups))

/* prevent filtered words from being added to text */
&(((lcase(added_lines) rlike filter1) | (lcase(added_lines) rlike filter2)
& !((lcase(removed_lines) rlike filter1) | (lcase(removed_lines) rlike filter2)))

/* prevent articles from being created which contain filtered words */
| (article_recent_contributors==""  & ((lcase(article_text) rlike filter1) | (lcase(article_text) rlike filter2))

/* prevent summaries containing such words */
| lcase(summary) rlike filter1 | lcase(summary) rlike filter2)

/* prevent page moves to titles containing filtered words */
| (action=="move" & ((lcase(moved_to_text) rlike filter1) | (lcase(moved_to_text) rlike filter2)))

/* prevent user accounts from being created which contain filtered words */
| (action=="createaccount" & ((lcase(user_name) rlike filter1) | (lcase(user_name) rlike filter2))))

/* allow action if the word was there before for some reason */
& !((lcase(removed_lines) rlike filter1) | (lcase(removed_lines) rlike filter2))

```
