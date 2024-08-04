# Scraping home listings: “Do you have €1M+ extra?”

Check out the piece I wrote based on the scraper data: [LINKKI]

## My aim:

Investigating and scraping a Finnish home listing page [Oikotie](https://asunnot.oikotie.fi/myytavat-asunnot?pagination=1&cardType=100) with 60,000 listed apartments. 

I tried to approach the data first by entering a undocumented API, but it was protected. I would have liked to get all information existing of each apartment. The page gets the listings from the API while scrolling, so also requests / BeautifulSoup was useless: only the page’s filter menu was returned as the result, not the listings.

Downgraded my project to get only apartments worth for €1,000,000 or more, so I would get a reasonable dataset. Finally, I scraped the page by using Playwright, and I gathered only information seen on each tab (price, size and address), not all the data available, when clicking a listing.


## What I found:

When investigating the page, I realized that there were also homes from other countries, e.g. from the Emirates, so I filtered the page before scraping it just to ease my job.

I got a dataset for more than 500 €1M+ apartments from all over Finland. The data revealed that great share of the valuable apartments is in Southern Finland. From +500 apartments around 400 were in Helsinki metropolitan area. I have never seen a dataset like this before.

The data needed a lot of cleaning, for example because not all €1M+ listings were one family homes, but one could find also entire row houses etc. In my story, I wanted to talk about homes, so I had to eliminate part of the results. After investigating the material, by using the apartment size I draw line to 800 m²: listings above that seemed to be something else than private apartments.


## Data collection process:

Here is the [filtered link]( https://asunnot.oikotie.fi/myytavat-asunnot?pagination=1&locations=%5B%5B1,9,%22Suomi%22%5D%5D&cardType=100&price%5Bmin%5D=1000000) that I used for scraping.

With asynchronous Playwright I entered to Oikotie and created several for loops to go through all listing cards and tabs. To identify the right html elements, I used Xpath.

When going through the page, I created a try/except command, so the code would loop through even when encountering missing information. On the listing card of each apartment, there was sometimes extra information, like monthly dues the owner must pay for house maintenance. I cleaned those kind of information away already when looping with .endswith().

Saved the scraped information into csv.


## Overview of the data analysis:

Before analyzing, I cleaned the data in a df by dividing the address information, e.g. I made a new column for city. Also, extra characters like ‘€’ and spaces needed to be cleaned away, and I calculated price per square meter for each listed home. The datatypes needed to be partly changed too. There were also misleading row with price like 1,234,567, and also building lots for sale, so I cleaned them away. Before analyzing, I saved the cleaned data into a new csv.

Before I found out, what kind of story do I want to write, I made some basic questions, like which are the biggest vs. smallest and most expensive vs. cheapest homes. I also checked average and median prices and which streets are most popping out from the data.

When analyzing the data, I understood that not all listings were private homes, but more like entire housing units, B&Bs etc. so I dropped part of data away.


## New skills:

My main goal was to scrape by using something else than requests, so I strengthened my knowledge of using Playwright. Looping through different tabs and collecting several elements was also something, I had not been doing many times earlier. 
When cleaning and organizing data, I tried to focus on using principles of tidy data and to chain pandas commands.


## What I would have liked to do better:

I wanted to get page’s whole content, but unfortunately had no skills for that.

When looping through the page, it would have been wise to collect also the link to each home listing. This would have helped when checking things manually afterwards or I could have add the links into Datawrapper’s tooltips when visualizing the data.
