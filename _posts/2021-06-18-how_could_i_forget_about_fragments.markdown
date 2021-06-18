---
layout: post
title:      "How could I forget about Fragments! "
date:       2021-06-18 15:21:18 +0000
permalink:  how_could_i_forget_about_fragments
---


So here I am trying to style my final React project and I cant get my `navbar` ro render all nice and clean with evenlyspaced buttons, so I went to a study group... 

Wait. I know your waiting for the punchline akin to that old one liner, how'd that go? ... oh... right, "one time at band camp...," but before we get there lets start at the beginning. 

*(Begin wistful music and requisit scrolling screen...)*

## ... A long time ago, 

### ...in a land far, far...
 
#### ...no... keep going...

##### ...seriously... farther...

**...ok, just a little farther...**

#### Hey... wait... ok, ok... thats good... 

...just... stay there..., ok? *...sheesh...* I was just joking... yes, this *is* serious busines, but it *can* still be fun.

Now, where was I?

My project is a tool to help the user with game fish identification. I want to have 3 seperate navigational components, wach housed in a container that renders the nessicary links or components. 

First  a static component that houses the app home page and some public inormation.

![Imgur](https://i.imgur.com/fk7H4yF.png)

Second the login navigational container that houses the login, create a new user, and logout functionality and the required logic to switch between them when a user logs in. 

![Imgur](https://i.imgur.com/v7wTzr6.png)

Lastly a user navigational component thats housed in a private route that only renders once a user has logged in, and for the time being is pinned to the left hand side of the screen while I turn the nuts and bolts of the functionaluity of the app.

![Imgur](https://i.imgur.com/CZuW7NS.png)

As all well and good as this may sound, I'm in no way happy when it renders like this:

![Imgur](https://i.imgur.com/40KB9OJ.png)

Or, like this once a user os logged in:

![Imgur](https://i.imgur.com/xxNEtYF.png)

Now, we can debate the merrits of the shade of blue I selected, or the overall oppulence of Mr.Carpyface up there on the top left, but what *I'm* concerned with is that giant... cavernous... Grand Canyon sized fissure between my StaticNav on the left and my LoginNav on the right! 

I tried manipulating it with CSS to varying degrees of failure. I tried centering, flexbox manipulation, space-between and all sorts of layouts and they all gave me a big 'ol ze-ro on the efficacy scale. So whats an old carpenter trying to learn to code to do? 

I went to a study group. 

Now, I do pride myself on being autodidactic, but truth be told I kno no person is an island. We all get to where we are and to where we are headed through the grace and benevolence of others. So I made the big ask... 

"HAAAAALP! I'm stuck", I cried into my web cam.

... and they did.

To be honest I'm not sure who exactly said It, It may hve been the instructor Tyler, or one of the students but they sugested using *React fragments* instead of a `<div/>` in the return value of my containers!

"Brilliance! Lets give it a try." I exclaimed, and started making some changes. 

My initial code (as you can see above) rendered HTML that looked like this on initial render and after login:

![Imgur](https://i.imgur.com/h713S3M.png)

![Imgur](https://i.imgur.com/cz5yrnh.png)

As you can see, each container renders in its own pretty little `<div/>` container that seperates it from all the cool code floating around it. Now this definitly has its merrits, however, what we want is one grand masterpiece of a navBar that will encapsulate all therequired functionality. 

What was suggested was this, React has this cool bit of functionality that allows it to pass along information without createing a subsequent node. To explain this in a different way, my code is returning this to my `NavBarContainer` :

```
return (
  <div>
		 <NavLink to="/home">Home</NavLink>
      <NavLink to="/genus">Genus</NavLink>
      <NavLink to="/species">Species</NavLink>
      <NavLink to="/user">My Stuff</NavLink>
   </div>
  );
```
	
This is what resulted in a seperate node (the `<div/>` elements you see above) wrapping each component of my `NavBar`. Now we all know react just *LOVES* its `<div/>`s, however, so long as this will get added to another component or container that will ensure we have our `<div/>` to make React happy we can  replace all these `<div/>`s with one of two options React allows for.
	
First, we can use `<React.Fragment/>`. This would allow us to include a `key`, should we need one, say, for styling or some other functionality. So I could make my code look like this:
	
```
return (
	<React.Fragment key='navBar-static'>
		<NavLink to="/home">Home</NavLink>
		<NavLink to="/genus">Genus</NavLink>
		<NavLink to="/species">Species</NavLink>
		<NavLink to="/user">My Stuff</NavLink>
	</React.Fragment>
);
```
	
However, I want this to look and feel like one single component once its rendered and my styling plan does not, as of yet, include different styling for these seperate items. Knowing this, I'm not planning on using a `key`, so to avoid the warning I might receive i opted for this second option.
	
Instead of using the `<React.Fragment/>` syntax, o opted for the newer, shorter, version wich is simply `<>...</>`.

Heres what it looked like when we added it to my code:
	
![Imgur](https://i.imgur.com/x4edCp3.png)
	
![Imgur](https://i.imgur.com/mVcumhD.png)
	
So what was the effect? Well, take a look:

First heres what the HTML looked like:

[Imgur](https://i.imgur.com/bPUDmoi.png)

[Imgur](https://i.imgur.com/vY90PTH.png)

As you can see it all appears as one continus node within the file, whic his exactly what we were looking to do so my `.css` file can style it out. 

The result in view:
	
![Imgur](https://i.imgur.com/MSJpS6l.png)
	
And after login:
	
![Imgur](https://i.imgur.com/AfJ2rO6.png)

EVENLY SPACED LINKS AND BUTTONS IN ALL THEIR WONDERFUL GLORY! ... VICTORY IS MINE! 
	
... I mean.... Pretty sweet, right?
	
Thanks for stopping by, now on to the rest of my styling. I hope this helped you.  


