---
layout: post
title:      "Adventures in CSS"
date:       2020-05-06 19:02:38 +0000
permalink:  adventures_in_css
---


After chugging through the Ruby portion of the class HTML and CSS have been a happy reprieve from what I will call more traditional coding to what might be called visual impact coding, where you get to (under the correct circumstances) immediately see the results of your efforts.

In my previous blogs I mentioned some initial struggle with setting up my local environment. It was nothing major, just some start/stop glitches that happened to coincide with both my CLI project and the onset of COVID 19 (SARS-COV-2). The whole transition to quarantine and having my young children home fulltime made things, well, lets say... interesting. But that's not the purpose of the blog, to wax philosophically about the modern education system or the benefits and deficiencies of modern culture on parenting (which I will reserve for more casual company and maybe a few glasses or a fine wine). What I will talk about is the interesting situation I found myself in when I was trying to use ```httpserver``` as I was instructed in the lectures. 

It didn't work. Yup... it wasn't installed. I'm not sure if it was me or what, but it wasn't there. I made it through anything that had us running tests while I struggled to figure out where I went wrong. I got through all of the HTML portion of the course work just fine without it but once I hit CSS there was no way I was moving on. 

I got to these lines of the first lab and I was dead in the water:

"Introduction
In this lab, we will be adding style to our index.html page by linking an external CSS file. If you open index.html in the browser (by either opening the file with Google Chrome or running httpserver on the Learn IDE), you will see basic HTML that has been provided. The website emulates a basic Real Estate website (the links on it have been disabled, we will be working with only the basic index.html landing page)." 

OH NO! WHAT TO DO!?!

I did some poking and realized I never installed nodejs or npm on this computer. After a bit of struggle with versioning and some back and forth installing we go it figured out and I had stumbled on this awesome NPM function called ```live-server``` that, with a command of the same name, auto reloads your page as it detects your make changes.

Now I've read that you may not want to use this on public wifi, so be forewarned, and you can see the concerns with a Google.com search, but for this CSS work it has been invaluable. I've just finished the module and for even the first lab, My Little Rainbows, it made changing the colors and tracking my progress WAY easier. It afforded me the ability to test and play with various aspects of the CSS code and HTML without having to constantly reload the page from the command line. 

Now you might suggest that you could use the developer tools for this. That is a valid argument. You CAN use the developer tools window for this, and I did. However, when you're writing the code directly in the file this may not be an option, or at least not a great one.

Either way, having the ability to work directly in the CSS file while in labs like the HTML Grid lab, or CSS Kitten Wheelbarrow Lab made hacking through the learning curve much easier. In the CSS Kitten Wheelbarrow Lab and later in the Animal Save Lab being able to play with setting pixel values, alignment, or position a breeze. In the same vein the Flexbox code along and  and, really any of the responsive design portion of the module I had the ability to see the impact of my code in real time. In the grid lab I could put a visual on what changing values in the ```grid-area:``` had or ```justify-self``` and ```align-self```. It honestly made the experience way more immersive. I didn’t have to keep re-loading the pages in order to move on. It gave some needed freedom.  

I can honestly say I enjoyed this module and can't wait to start putting some of my newfound CSS skills to work.

