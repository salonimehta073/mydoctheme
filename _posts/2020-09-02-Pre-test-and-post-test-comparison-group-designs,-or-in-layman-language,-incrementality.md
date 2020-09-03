---
layout: post
author: Saloni
comments_id: 3
image:
  path: /assets/link_preview.PNG
  height: 100
  width: 100
---

Forget the jargon topic name and imagine this simple scenario: You want to measure the effectiveness of a discount coupon that you sent to a few of your customers. When I say effectiveness, you essentially want to answer two questions: Was my coupon effective in driving my [main metric]? If yes, by how much? You start off by creating two similar groups from your customer base: a test group that received this coupon and a control group that does not receive it. You’ve tried your best to ensure that the two groups are similar from a purchase behaviour and demographic standpoint and therefore, next step would be to compare the differences in the mean metric (your metric of focus could be # sales, basket value etc) for the two groups. Although this method is reasonable, what if you had a seasonal sale right around the time the discount coupon was sent? You might run into some trouble because it will be difficult to attribute and quantify the true effectiveness of the marketing campaign on your audience. The solution is in considering pre-discount and post-discount means for both the groups, test and control. Essentially, you want to ensure that you eliminate effects of the differences between pre control and post control from the overall pre-post differences in the test group. 

Although this problem sounds simple, there seems to be a lot of debate on which method to use for measuring overall incrementality with a statistical test. This problem is fairly common in clinical experiments, as you can imagine. I came across this problem when I was working in the marketing analytics division of a retailer. Seasonality played a big role in driving sales and it was always necessary to remove its effects from the overall campaign incrementality analysis. One of the reasons we did an incrementality test was to prove, with utmost confidence, that the marketing tactic really worked and it wasn’t engineered towards driving sales from people who would anyway buy our stuff. We’d found some evidence that a lot of high-value or engaged shoppers were being sent discount coupons. Our hypothesis was that these shoppers do not need to be incentivized to shop more and this budget could instead be used in driving sales from other groups of customers. A test environment like this, with pre and post for similar test and control groups eliminated these biases and allowed for true incrementality to shine through. 

The most important thing to keep in mind, however, is to ensure that the two groups are similar. Pre-existing differences in the groups can lead to a lot of pain and suffering as you try different tests and discover different answers. You need to ensure that the pre-experiment group differences are close to 0. That said, we used a ratio-based method to arrive at a predicted post-test mean and compared it with the observed value of the post-test group. 

The method estimates a ‘predicted post-test score’ by taking a ratio of post and pre control means and multiplying that with the pre-test mean. The formula looks like:

    Predicted post-test = Pre-test * (Post-control/Pre-control)

The real incrementality is then basically calculated as Observed post-test – Predicted post- test. If this difference is positive (& with statistical significance), we can say that the effect of the coupon was positive and even quantify it. If the difference is negative, we observe the coupon/discount and discard it if it doesn’t work anymore. 

I’m honestly not sure if this method is accurate and what other considerations we’ve missed out on. I found a few references (mentioned below) that state the assumptions/risks that each method comes with. Did you encounter an experiment like this at work? How did measure it?

Source: 

https://yorkspace.library.yorku.ca/xmlui/bitstream/handle/10315/33240/pre_post_change_jennings_cribbie_jds.pdf?sequence=1&isAllowed=y – Best resource to understand different methods that can be used

https://sg.inflibnet.ac.in/bitstream/10603/1548/14/14_chapter%204.pdf

https://www.theanalysisfactor.com/pre-post-data-repeated-measures/


