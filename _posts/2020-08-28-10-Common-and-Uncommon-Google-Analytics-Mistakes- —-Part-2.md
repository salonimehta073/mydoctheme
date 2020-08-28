---
layout: post
author: Saloni
title: 10 Common and Uncommon Google Analytics Mistakes — Part 2
image:
  path: /assets/link_preview.PNG
  height: 100
  width: 100
---

*A list of 10 mistakes to avoid while using Google Analytics and Google Tag Manager. Most of these are from my own experience while working with the tools*

You can find the first part of the series [here]({% post_url /_posts/2020-08-26-10-Common-And-Uncommon-Google-Analytics-Mistakes %})

The next 5 in this post are not errors per se but things to keep in mind when setting up your account in Google Analytics.

**6. Have an unfiltered view**

We talked about filtering internal traffic through employee IP. GA gives you the ability to subset the traffic data and exclude unwanted information. You can create filters at the account level or view level. The view level filter will only subset data that you can see on that view. Hence, a better way would be to [create a filter](https://support.google.com/analytics/answer/1034823?hl=en) at the account level and assign them to different views.

A lot of marketers create filters properly but then proceed to apply them to all views. This can be risky since your data cannot be recovered if you apply a wrong filter. Hence, it is always advisable to create at least three views: All Website Data (unfiltered view), a Test view where you can test the effect of your filter, and finally a Final View where you can apply the filters you have already tested. Keeping an unfiltered view is a simple step but not doing this can mean loss of data that you cannot recover later

**7. Custom channel grouping**

Channels represent the path taken by users before landing on your website. For example, users could come from organic search, a paid ad, a referral from another website, or just by directly typing in your URL. The channels report in acquisition gives us a good view of traffic coming from different sources and how it is essentially engaging. These channels come pre-defined from GA’s end and are called Default Channel Grouping. The issue with the default grouping is that it is overly simplified and does not work for a lot of cases.

A better way to look at this data is by creating your own custom channel grouping. This will take a bit of work but is incredibly useful and allows you to look at your data from the lens of your acquisition sources. You can get a detailed tutorial on how to enable it for your site [here](https://www.datadrivenu.com/channel-grouping-google-analytics/). One thing to keep in mind is the order of the channel groupings. Google treats this in a waterfall method and therefore, these grouping rules are executed in the order in which they are defined. Therefore, it is very important to define the logic of each grouping correctly and ensure that the order is maintained in the way you want it to be. For example, if you have ‘Direct’ as the first grouping and ‘Organic Search — Google’ as the next one, Google will bucket all traffic for which there is no source into the ‘Direct’ channel and then it will go on to find all traffic with google organic as the source and bucket that into ‘Organic Search — Google’.

**8. Enabling Site Search**

If you have a search box on your site, then enabling site search is crucial to your understanding of your users’ needs. Site search can give you valuable insights about how your users are performing a search on the website; if they can find what they are looking for (% search exits, % search refinement) and if there is any additional content that they look for which you do not have currently (time after search, avg search depth). This option is not enabled by default and you can enable it from your admin settings. You simply need to turn the setting on and define the query parameter that GA will strip to identify the query. For example, if your search result page looks like www.yoursite.com/s=iphone11 then you need to enter ‘s’ as your search parameter.

**9. Debug with GTM — preview mode**

When (and if) you define custom events or implement any other tags really, there is a high possibility that it might not work because of a few silly errors. Testing the tags in a preview mode is the best way to debug errors and also understand how different values (custom dimensions and metrics, if any) are being passed to GA as you interact with the site. For example, if there is an event defined for a video play after 10 seconds and certain values are passed if this event occurs, you can preview the specific tag on GTM and check if it fired or not. If it did not fire, GTM allows you to see which logical condition was not satisfied and you can make the required changes. You can find a complete guide on how to preview and debug errors [here](https://www.optimizesmart.com/guide-to-google-tag-manager-debug-console/).

**10. Custom campaigns not being tracked**

You cannot always rely on GA’s understanding of traffic sources and campaign tracking. You might be also running quite a few custom campaigns and might want to track them appropriately. Tagging each campaign is extremely important if you want to enjoy the fruits of attribution. It is extremely easy and Google’s dev tools [here](https://ga-dev-tools.appspot.com/campaign-url-builder/) can help you do that in no time.

I hope you (to the 2 people reading this) find some value in this and avoid the same mistakes I made while setting up GA and GTM
