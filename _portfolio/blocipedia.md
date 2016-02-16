---
layout: post
title: Blocipedia
thumbnail-path: "img/blocipedia.png"
short-description: Build a production quality SaaS app that allows users to create their own wikis.

---

{:.center}
![]({{ site.baseurl }}/img/blocipedia.png)

## Explanation

Blocipedia is a wiki based app that allows users to create, edit, and add collaborators to their own wikis. 

## Problem

In any community, I like to see a Wiki page. I never see, however, wikis that only certain users can edit, or that can be hidden from the general public. 

## Solution

Enter Blocipedia. The challenge for me was to work on developing code for user authorization and permissions in order to get the features I wanted. 

## Results

All said and done, I was able to work with Pundit and Devise for user authorization. In order to add and delete authorized users from one's Wiki, I added a JQuery autocomplete form. Using Stripe, I was able to develop multiple tiers of usership with different abilities.

> Working with Stripe turned out to be a much easier challenge than I thought it would. It just involved adding some inline Javascript. 

In the future, I plan to further build out this code in order to add it to any application or community I might build. 

## Conclusion

Overall, I found Blocipedia to be a great learning experience. While the backend works quite well, I still need to further develop the frontend. In the future, I will be developing an api and a decoupled front end.