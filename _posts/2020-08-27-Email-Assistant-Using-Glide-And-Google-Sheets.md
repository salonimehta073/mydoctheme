---
layout: post
author: Saloni
title: Email Assistant Using Glide and Google Sheets
image:
  path: /assets/link_preview.PNG
  height: 100
  width: 100
---

P.S. If you just want to check the high-fidelity wireframe, check it [here](https://email-assistant.glideapp.io/)

Writing, thinking, and reading in English does not come naturally to a lot of non-native English speakers. But they have had to adopt it to unlock access to better work opportunities and if you live in urban India, to fit in. When you are in a professional work environment, it becomes ever more necessary to ensure clarity and sophistication in written and verbal communication. If you work for foreign clients, written communication through email is one of the first ways you establish contact and later, trust. However, in my (very short) career, I’ve seen a lot of my colleagues, peers and even superiors struggle with professional email writing. The hardest step is always the first step – figuring out what components the email should contain and in what order. I asked a few friends of mine about their email writing process and if they too feel the need to Google a template before writing their email. A lot of them admitted that they do spend some time looking online for available email examples that can serve as a base for their eventual email.

With this need identified, I had an idea for a simple service that would work as an email writing assistant. It would aggregate all available templates online by different email use cases (for example, a job application email to a recruiter, requesting a client for a meeting etc.), break down each email into its components (subject line, greeting, body, action statement, closing) and help a user construct an email by selecting the best option for each of these components for his/her specific use case. 

I have recently started dabbling a bit with scraping through Python and I figured this will be an interesting project to try building. My ex-colleague, Dharmik, also joined with me and we started working on creating a basic MVP so we could test this idea. 

The first step was to think about email use cases and data collection. We narrowed it down to two basic categories: jobs and business emails. Jobs includes all use cases related to applying to a job, asking for a referral, thanking, and following up with a recruiter and networking with your peers/friends. Business email includes general use cases like asking for a leave, requesting for a meeting and even sending in a formal resignation email. I realized that the true value of this service would be its superior content and ease of crafting an email. Hence, just scraping and collecting a hundred bad templates will probably not be very useful. Our initial thought process was that with enough number of templates, we’d somehow score them based on which templates were most similar and occurred frequently (using some cool ML techniques on the way that we wouldn’t understand). However, to understand the process better, we started collecting data manually for a few cases to check how available email samples looked like. We collected about 50-60 samples across a few use cases and easily split them up into 5 components: subject, greeting, body, CTA and closing. We could therefore expand our set of available templates with basic permutation; for example, you could select a subject line from Email Example 1 and the main body from Email Example 5. 

Once we had this data collected, we turned to figuring out a user flow for crafting an email. Roughly, it looked like the below:


Selecting category of email (Job/Business Email) - > Selecting a use case within the category (Job application/Meeting Request etc.) - > Choosing a subject line from available options corresponding to the category and use case selection - > Choosing a greeting -> Choosing the main body element -> Choosing an action statement (optional) -> Choosing a closing phrase -> Edit some part of the email if needed - > Copy the email

Along with access to a variety of email components according to a user’s need, there was also a need to see a few perfectly written emails with all the details filled in. We decided to also have a repository of the best 5 email samples for each of the use cases. Since we already have a large collection of emails created with the permutation described above, we were able to score each of these emails and choose the best 5 out of the lot.

Once all this data was collected and a user flow in mind, next step was to figure out how and where to build this so we could show this idea to our friends and peers and get feedback from them. I’ve been reading a bit about the No-Code revolution and all kinds of new products that are beginning to offer no-code easy building of apps and websites. Glide Apps particularly stood out (because of Tech Twitter marketing? Maybe) with their 5-minute promise of building an app from Google Sheets (not unlike the fabled 2 min Maggi noodles). Although I am embarrassed to admit that it took way longer than that, it was still much easier to have a high-fidelity wireframe of what a service like this will eventually look like. 

Next, we realize that no email is complete without your personal details and additions. Although it is certain that a user will need to add details or remove parts not relevant to the use case, we wanted to try and reduce the load on doing that by standardizing a few details and dynamically replacing these values with user details. A simple example of that is adding your name at the end of the email. Most emails end with a simple closing greeting, like ‘Thanks’ or ‘Regards’ or ‘Best’ and ends with the name of the person sending the email. We decided to fill in this name automatically by using the name of the user from his filled-in profile details on the app. 

Another important addition to a personalized email experience was also saving emails or templates that users created and liked. Glide has a wonderful integration with Zapier that allows us to offer a functionality of sending the saved email/template to the user's email ID. 

This is it for now. It's still a work in progress. Will keep updating. 
