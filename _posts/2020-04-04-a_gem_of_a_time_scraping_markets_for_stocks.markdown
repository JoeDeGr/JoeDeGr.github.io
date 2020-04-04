---
layout: post
title:      "A Gem of a time Scraping Markets for stocks."
date:       2020-04-04 13:13:47 -0400
permalink:  a_gem_of_a_time_scraping_markets_for_stocks
---


So I ventured to build a scraper that would look at a webpage, I had originally decided on Yahoo Finance, for data on Stocks and would return the current stock price. I considered the Coronavirus datasets, but I thought that wouldn't be all that original. So... I developed a flow chart and set out to build my gem in the Learn IDE. 

I had never done this before, but a little optimism and diligence went a long way. I ended up scrapping my first attempt at the build for a couple of reasons. Not the least of which was that after about ten minutes of hacking away at it I decided to build my local environment prior to building the gem. I figured this would give me a little less stress in the re-coding department as the connection can become unstable during high web traffic times around me. In the end I think this was the correct move, but it did add a bit of frustration in figuring out how to get the system functional. This resulted in a couple of errors and re-start to the project. In the end I think the re-start was actually good for me because I had a better idea of what I wanted and was able to tear through a good chunk of the coding. 

I did work on the LEARN IDE for about 3 hours to test the functionality of my gem on a different system at the end and, of course, did a little editing. When I returned from a quick break... the screen was frozen and I couldn't access the files! It wasn't all gone, but the system had re-loaded. Luckily I had the Stock class of my gem, the part I was editing still up... although unfunctional. So I got to work copying what I had done. Lesson learned. Save and commit often. 

On the bright side, this isn't the biggest hurdle I had. I began my final set of code by following the advice of AVI and beginning at the CLI. I worked through each bit of functionality one piece at a time. I built the CLI class to ask the Portfolio Class for the information and when needed the Portfolio class calls on the Stock class to provide information about a specific stock. Once I got in a rhythm it all came together for me... until I began trying to scrape Yahoo Finance. 

Yahoo Finance uses Javascript and, after a bit of trying I reached out for some advice. The watir gem was recommended and I tried to get it running, but I ended up getting hung up in installation process. For the sake of time, as I was getting hung up installing software rather than writing code, I then considered using an API. I thought this might be a good option, but there would also be a learning curve.  At the recommendation of a teacher I took a look at EODdata.com and that made it all come together for me. Parsing out the data took a moment, but in the end everything I was looking for was there and I was able to pull it all together using tools I had in my current toolbox. 

using Nokogiri and open-uri I was able to open a webpage to a document that contained the data for an individual stock by calling the individual stocks symbol and the exchange it is traded on within the url. I can then parse the data I need from table data within that document. I could even expand to including some historical data.

I do eventually plan to come back to watir or the API for the sake of knowledge, I also hope to expand the functionality of the gem at some point. I feel this would do well if the portfolio data could be called and stored for comparison.

In the end I am happy how this came together. 

If you would like to see what I came up with, please feel free. You can find my projects repository  here: 

https://github.com/JoeDeGr/MarketScraper.git

As always, any input and constructive advice is happily accepted.  


