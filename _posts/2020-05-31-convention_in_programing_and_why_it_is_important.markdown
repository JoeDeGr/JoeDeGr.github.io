---
layout: post
title:      "Convention in Programing and Why it is Important."
date:       2020-05-31 17:02:21 +0000
permalink:  convention_in_programing_and_why_it_is_important
---

Convention in programing and why it's important.

Coming into my Sinatra project and completing module 12 one thing has become very evident to me. In programming conventions matter. Especially when dealing in test driven design. Without having a baseline pattern by which we can develop a framework for our programing project having someone step in to further develop, edit, or create content on our platform. We might be left with a pretty incredible task of understanding what the previous developer did and decide to simply rebuild the whole project from scratch.

In steps Representation State Transfer, or RESTful routs.  This is a design specific architectural style that helps us map an HTTP request to our CRUD (create, read, update, delete) functionality. This gives any designer a base framework with which to understand and build upon. As I mentioned earlier, it also allows for the establishment of expectations when developing tests and a way to chase down errors and repair broken code. 

The RESTful route structure is pretty simple. Given a specific HTTP verb you have an associated route convention and that convention gives us a specified action. Using an example of a blog page the routes would look something like the following:
1.	GET	
	ROUTE: /blogs'	
	Action: The index action. 
i.	This links to the index page to display all the blogs
2.	GET
	ROUTE: /blogs/new'      	
	Action: New/Create action. 
i.	This displays a create a blog form
3.	POST
	ROUTE: /blogs'  
	Action: create action. 
i.	This encapsulates the creates functionality that creates a new blog in our associated database and would typically redirect us to the show action.
4.	GET
	ROUTE: /blogs/:id
	Action: Show action. 
i.	This displays the blog page associated with the ID in the URL.
5.	GET
	ROUTE: /blogs/:id/edit'	
	Action: edit action. 
i.	This displays an edit form for the blog associated with the ID in the URL.
6.	PATCH
	ROUTE: /blogs/:id'
	Action: Update action. 
i.	This changes or updates an existing blog associated with the ID in the URL.
7.	PUT
	ROUTE: /blogs/:id'
	Action: update action. 
i.	This replaces an existing blog associated with the ID given in the URL.
8.	DELETE
	ROUTE: /blogs/:id'
	Action: delete action.
i.	This action deletes the blog associated with the ID in the URL.
As you can see this framework provides us with a very clear repeatable pattern that we could apply over and over and have a clear understanding of what each action is supposed to be doing. If we were to have associated posts within our blog we could change ‘/blogs’ to ‘/posts’ throughout this framework and have a baseline for all of our CRUD actions even within the same web application. Further, if a new designer steps in to add content or functionality or make a repair they could also clearly understand what we intended. This topic of convention extends elsewhere withing the topics of design and engineering as well, but I will save those of subsequent posts.  

 

