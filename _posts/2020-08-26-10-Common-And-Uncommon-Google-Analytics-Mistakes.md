---
layout: post
author: Saloni
image:
  path: /assets/link_preview.PNG
  height: 100
  width: 100
---

*A list of 10 mistakes to avoid while using Google Analytics and Google Tag Manager. Most of these are from my own experience while working with the tools*

Google Analytics (GA) is used by 55% of all websites on the Internet. That is a staggering number. Beyond adding the standard code to your website and answering simple questions like the number of daily visitors to your website, source of traffic, top pages visited, etc., there’s a lot you can track using the powerful tag management tool Google Tag Manager (GTM) and defining custom dimensions and custom metrics within GA. There is a common learning curve when it comes to working with GA and GTM and I’ve noticed that most people make the same kind of mistakes while using these tools to track more information about your users.

I’m going to do a clickbaity essay focusing on 10 common mistakes that are made in reporting while using GA. This is the first part of the series and will focus on 5 of them. However, if you are a beginner, please make sure you have the below bases covered. I’m including links to guides for these beginner errors:

[Not setting up the code correctly](https://chrome.google.com/webstore/detail/tag-assistant-by-google/kejbdjndbnbjgmefkgdddjlbokphdefk?hl=en), 
[cross-domain tracking](https://support.google.com/analytics/answer/1034342?hl=en), [e-commerce tracking](https://support.google.com/analytics/answer/1009612?hl=en),
[not setting up goals](https://searchengineland.com/a-beginner%E2%80%99s-guide-to-setting-goals-in-google-analytics-101826),
[adding GA code to staging set up](https://www.napkyn.com/2017/07/12/ga-gtm-environments/),
[incorrect time zones](https://support.google.com/analytics/answer/1010249?hl=en), [not linking GA with other Google products in use](https://support.google.com/google-ads/answer/1704341?hl=en),
and [enabling demographic and interest report](https://support.google.com/analytics/answer/2819948?hl=en).


 - - -
 
Alright, so once you have these out of the way, let’s start from the top -

**1. Setting up a utm_source for internal articles**

This is an easy mistake and one I made without considering the effects it could have on reporting. I appended utm_source = internal for in-page links to understand the performance of a few blog articles within the website. Do not append utm_source to track movements between articles on the website. The source parameter is for understanding channels of acquisition (external traffic) for a customer and not for tracking their behavior within the website. As soon as a visitor clicks on the internal link with UTM parameters, a new session is started with the source information you supplied. This increases the session count artificially; conversions cannot be traced to the original source and the bounce rate from external sources can increase too. What are your options in case you want to track internal articles/clicks?

i. If you want to look at all the pages that sent traffic to the internal page in question, you can create a [custom report](https://support.google.com/analytics/answer/1151300?hl=en). Set Page and Previous Page Path as dimensions and pageviews as the metric


ii. You can create a custom dimension like itm_source and use that for tracking internal links. [Here](https://www.smashingmagazine.com/2017/08/tracking-internal-marketing-campaigns-google-analytics/)’s a guide on how to create those and also on how to view them in custom reports
This is the most widely misunderstood GA metric. Google defines a bounce as a single-page session and consequently bounce rate as the % of single-page sessions. What this means is, if you have a website with only one page and users who come to your website can only look at that page (for however long they’d like), your bounce rate will be 100%.

iii. You can always track internal movements with [custom events](https://support.google.com/tagmanager/answer/6106716?hl=en) (You might already be using custom events to track CTAs on your website — like a sign-up form, video views, etc.)

**2. (Mis)understanding bounce rate**

This is the most widely misunderstood GA metric. Google defines a bounce as a single-page session and consequently bounce rate as the % of single-page sessions. What this means is, if you have a website with only one page and users who come to your website can only look at that page (for however long they’d like), your bounce rate will be 100%.

However, if your website has more than 1 page (which I am hoping it does), Google will calculate the bounce rate based on the % of single interaction sessions, which are sessions in which the visitor left your site from the landing page without interacting any further. However, one of the most important things while benchmarking your bounce rate against others or even in trying to make sense of it is — IT DEPENDS. It depends on your site, your business model, and your goals. You need to decide which website interactions count as interactions and accordingly define bounce rate by the % of people who do not engage in those interactions.

Thankfully, there is a way for you to make Google Analytics understand your definition of bounce rate. For example, if there is a video on your landing page and watching 10 seconds of it qualifies as an engaged visitor according to your business definition, you can do that by tracking the video view event (Check [here](https://support.google.com/tagmanager/answer/6106716?hl=en) for details on how to define events). More specifically, the flag ‘non-interaction Hit’ = False tells Google that this was an interaction hit (what’s up with the double negatives?!) and hence GA will exclude it from the bounced visitor flag.



**3. Scope of metrics**


Google allows us to analyze web traffic through two categories of data: dimensions and metrics. Simply put, dimensions answer the ‘what’ and metrics answer ‘how’ or ‘how many’. Google allows gives us access to standard reports where we can analyze these dimension-metric combinations. But I’m sure there are a couple of things you’ve wondered when looking at these reports:


i. Why do the Standard Reports not have ALL the metrics that I’m looking for in one single place?

ii. When I try to create Custom Reports with all dimensions and metrics, I’m not sure if the data is accurate

Google deliberately leaves out some metrics and dimensions from its standard reports and understanding why is key to building your custom reports too. Each dimension and metric have a defined ‘scope’ or in simple words, a way in which it is collected. The 4 types of scopes are:

A. Hit level

B. Session level

C. User-level

D. Product level

What this essentially means is, lumping together dimensions and metrics with different scope hierarchy is not allowed in standard reporting and is disastrous if you try to create a custom report. The reason is that a hit is the lowest in the hierarchy of interactions captured by GA. A hit is essentially any single action on the website such as an event trigger or a pageview. The next level is a session, which is essentially a collection of all hits that take place within a certain time frame (based on continuous activity or hits, or 30-minute duration of inactivity). A user is the highest level of data and as the name suggests, attempts to track multiple sessions from the same user (An important point to note here is that GA is tracking a browser and not a real user. It is doing that with a cookie dropped on the browser that the user first visits GA from. Hence, if a new browser is used or cookies are cleared, GA will assume it is a new user).

This hierarchy runs in one direction only, and hence, sessions have hits; however, we cannot say a hit has sessions. For example, a custom report with Page, Sessions, and Users is a wrong report to look at. A user could visit multiple pages in a session and hence, this level of reporting will inflate the overall user and session number. Similarly, you cannot look at pages and goals in one view either since goals are a session-level metric and page are a hit-level metric.

However, if your website has more than 1 page (which I am hoping it does), Google will calculate the bounce rate based on the % of single interaction sessions, which are sessions in which the visitor left your site from the landing page without interacting any further. However, one of the most important things while benchmarking your bounce rate against others or even in trying to make sense of it is — IT DEPENDS. It depends on your site, your business model, and your goals. You need to decide which website interactions count as interactions and accordingly define bounce rate by the % of people who do not engage in those interactions.

Thankfully, there is a way for you to make Google Analytics understand your definition of bounce rate. For example, if there is a video on your landing page and watching 10 seconds of it qualifies as an engaged visitor according to your business definition, you can do that by tracking the video view event (Check here for details on how to define events). More specifically, the flag ‘non-interaction Hit’ = False tells Google that this was an interaction hit (what’s up with the double negatives?!) and hence GA will exclude it from the bounced visitor flag.

**4. Averages**

Statistics 101 has taught us to be mindful of averages and to understand the underlying distribution instead. This lesson is also applicable when analyzing your website traffic with web tools. Web tools, including GA, report metrics such as Avg. Session Duration, Pages per Session, and Sessions per User. These metrics are computed with a simple average and hence, tend to lose a lot of information and insight that we would like to tease out from the data.


Most websites have a skewed distribution and follow an 80–20, if not, 90–10 rule; which means that when you look at an average session duration of say, 2 minutes, you might think that 50% of your users spend more than 2 minutes and the other, less. However, you are more likely to find that 80% of users spend way less than 2 minutes, probably somewhere between 0–20 seconds and the other 20% of users spend a long time, maybe more than 5–7 minutes and this smaller segment of users tends to skew the average.


Another error that I have seen being made is in computing an average of averages in custom reports where these metrics are featured. For example, if you are looking at bounce rate and avg session duration by source and medium, and you download this data and try to recalculate these metrics at a source level, be careful to not compute an average of avg session duration and bounce rate

**5. Filtering out internal sessions**

Depending on the size of your business, excluding employees and other internal traffic can be an important issue to tackle. Internal traffic is not likely to resemble your users and will skew important metrics like sessions, page views, and session duration. Although there is no foolproof method of filtering out all these sessions, we can still eliminate them to a great extent and make sure that they don’t bother your main metrics.

i. [Use IP address filtering](https://www.bounteous.com/insights/2020/02/13/filter-and-exclude-internal-traffic-google-analytics/?lang=en-ca) to block employees — This is applicable if your company has a static IP address range. Make sure you don’t mess with the ‘All Website Data’ view and implement this first on a second view (There is no way for you to get back unfiltered data if you alter the all website data view)


ii. All other ways are messy and tricky to implement. So go back to step 1. But here’s an excellent guide on other creative ways to filter out internal traffic
