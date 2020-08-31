---
layout: post
author: Saloni
image:
  path: /assets/link_preview.PNG
  height: 100
  width: 100
---

This post details its implementation. Check the site [here](https://inspiron.webflow.io/). Code posted [here](https://github.com/salonimehta073/inspiron)


EDIT: After experimenting with Glide, I wanted to move this to Glide too. Implementation [here](https://inspired-reading.glideapp.io/) :) 


I love reading. I know this is true for a lot of us and I’m so glad that all book-loving champs have a special relationship with their books. Over the years, there has been a shift in my reading habits — I read about a lot many different subjects now than I used to, which is good. The flip side is that I do not have as much time to read as I used to back then (Back then = college. I’m not that old). With the paucity of time and an overwhelming external memory that we call the Internet, we need to then be smart about the books we choose to read. More importantly, how do we decide which books to read? Goodreads recommendations algorithm has never really been useful for me, nor has been just consulting my friends and peers. Visits to the bookstore are not cool anymore and with Bumble safely installed on my phone, there is no reason to waste all that time pretending to discover books. Book clubs and closed communities are much better, and I imagine they curate books based on what their role models are reading.


This approach is a good way to discover books worth reading — it might still not be exhaustive and might not lead you to those obscure titles that you can talk about at a dinner party, but you get a snapshot of content consumption habits of the people you admire. About 5 years back, I wanted to start a book subscription service in Bangalore and I wanted to send over one book per month to a subscriber, based on a questionnaire that I’d create. The idea was to discover a new book or a category for a user with the whole surprise element thrown in. I did not pursue the idea though — it just felt like… a lot of work. I wanted to do something interesting around book curation in this lockdown, which culminated in a side project of a book recommendation website. TLDR; It’s a website that allows you to discover book titles recommended by successful people. I’ve used Python to scrape book recommendation data from Google and get book title details (images, description, author) using the Open Library API. I’ve used Webflow to build the website and also used the WebFlow API to populate the CMS with the data. The rest of the article will focus on the methodology and what I can do better to solve this problem.


I started with the broad problem of ‘I want to discover the next best book to read’ into several sub-problem statements:

1. I want to read books recommended by my favorite person X
2. I want to read books recommended in the field of X
3. I want to read books recommended by important people who are experts in X field
4. I want to read books recommended by the greatest number of important people
5. I want to read books written by the author whose books were most recommended by important people

Although I managed to scrape data in a way that allows me to do all 5 things above, I’ve worked on the first 3 problems from a frontend perspective (Totally not used to WebFlow and its many secrets). So, for all the 5 statements I needed to build a database of book recommendations with the following specific data points:

1. A distinct list of ‘categories’ or ‘fields of work’ that I would select Important people from
2. Important people belonging to each category from #1
3. Book titles recommended by the list in #2
4. Metadata of books — the category it belongs to, a description, author details, book cover image and maybe an Amazon link

So, the first two data points, important people across different categories, is my ‘curation’. The focus was on having a well rounded of fields and if possible, a uniform distribution of important people across these categories. I did not automate this bit specifically but if I wanted to, I guess I could scrape lists like Forbes 40 under 40 and its counterparts in various fields apart from business. For this POV, I just created a super biased list of people across categories that seemed cool.

Once I had the list of people with me, I wrote a Python script to:

**1. Look up ‘PersonName book recommendations’ on Google**

*The easiest way to get access to articles or blogs that have this information. Web publications either interview people or aggregate this information from somewhere else*

**2. Visit the first 10 links from the result page**

*I did this to ensure I can get access to as many recommendations across different publications, for exhaustiveness, and because the first three Google search results aren’t always reliable. I did clean up the data later to remove duplicates*

**3. Within each link, get all hyperlinks and the associated hyperlink text from the page that matches either ‘Amazon’ or ‘Goodreads’**

*In each of these publications, the article would be something like ‘X has recommended these 5 books to read in 2018’ and would go on to list them along with an affiliate link for Amazon or in rare cases, a Goodreads book page
This was the easiest way I could remove other non-important hyperlinks (like the publication’s social sharing URLs, link outs to other pages within the website, or even other websites). This step ensured a lot of clean data*

**4. Download all this data in an excel with the below format:**
PersonName | Search Result Link No. | Title | Hyperlink

----Break for cleaning up the data----


After downloading the excel, I had to clean it up before getting details about each title through OpenLibrary API. Each publication would have a different way of presenting the title information. For example, one hyperlink could be a link to the Amazon page for ‘A brief history of time, by Stephen Hawking’ with the same hyperlink text; another website’s link could have a link to the same book but only ‘A brief history of time’ as the text. Some links were broken and would just go to Amazon.com; some links did not have text etc. This was a bit of a task. I did create a few rules to clean the data — however, largely this was a manual effort. Once I deduped and cleaned this list, there was another Python script to:

**1. Use ‘Title’ as an input parameter for OpenLibrary Search API**

**2. Parse the response format and get the below details:**

        a. ISBN/key
    
        b. Subject/Title Category
    
        c. Title Description
    
        d. Author name and author key
    
**3. Use ISBN/key to get book cover image using OpenLibrary Covers API**

**4. Use Author key to get author images using OpenLibrary Covers API**

**5. Do this in a loop and keeping in mind the API rate limitations**

**6. Write an exception for no responses**

**7. Download all this data in an excel**

Finally, with a lot of terrible code, I had all this data in place. Now, all I needed to was make a beautiful website with the right CMS structure that would allow me to interlink these disparate data points

  Book — Book Category
  
  People — People Category/Field
  
  People — Books
  

WebFlow is a no-code SaaS company for website building and website hosting. It has a Photoshop-like UI that allows one to visually create websites. Perfect for a noob like me. From the frontend perspective, it is a great, great tool. The CMS structure is super intuitive as well and I had no trouble creating these various tables and uploading my data through Excel. The primary issue was that I could not do ‘multi-referencing’ across tables with an excel upload. What that meant was, if I have a table that has a list of these important people, another table that has a list of all the books that I downloaded and if I need to match the recommended books to each person in the table, I can’t do it with an excel upload. I could do it manually or through an API. So I wrote my last Python script with the following steps:
 
**1. Upload an excel for each list:**

        a. Book Categories
      
        b. People Categories
      
        c. People
      
        d. Books
      
**2. This will assign a key to each item in each table. Download the file with individual item keys**

**3. Do a lookup with the original excel file so you have a mega file with all keys together (example, Person 1 key mapped to {Recommended Book 1 Key, Recommended Book 2 key, Recommended Book 3 key})**

**4. Use WebFlow API to update the multireference field items**

CMS was updated with all references and all I needed to do was build the frontend. I have kept it fairly simple as of now and I’ll allow you to explore it in more detail. There are definitely a couple of things I would love to change and improve:

1. Redesign and make the UI better

2. Get better quality images — I am relying on the OpenAPI cover images and they aren’t consistent in their quality

3. Make the data cleaning process a proper process and maybe automate it

4. Get a list of new people every month through scraping and update all this information automatically

5. Have a web form on the page and allow users to submit their recommendations for people to include


Overall, I had a lot of fun with this project because it allowed me to dabble a little bit with Python and also get a sense of how websites are built. Hit me up if you have feedback, good or bad 😊
