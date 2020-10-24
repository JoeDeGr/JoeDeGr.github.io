---
layout: post
title:      "Rails Portfolio Project"
date:       2020-10-24 20:57:13 +0000
permalink:  rails_portfolio_project
---


Contractors Note Pad

This has definitely been an adventure. From conceptualization to writing the code I have really enjoyed putting the pieces together.  I wont say there haven't been a few hurdles along the way, but we'll get to that shortly. Let's start with a brief overview of the concept. 

Here's my repo if you would like to check it out:

[https://github.com/JoeDeGr/Contractor-Note-Pad](http://)

This is a utility app designed to help streamline a contractors management of projects and costs. The contractor (User) can create a Project. Each Project can have multiple [Punch Lists](https://www.merriam-webster.com/dictionary/punch%20list), a common payment benchmark. Punch Lists can each have multiple Tasks to complete. The Tasks can have materials and workers assigned to them which aggregate up the list. So all the workers and materials assigned to a Task are shown in bothe the Punch List and Project they belong to. The goal is that a User can know who's doing what, how much it has cost, and what is left to be done. As a former carpenter I can attest that this is something I could have used help with. 

Framing out the project was pretty simple. I built the Users, Project, PunchList, and Task models. Went through the proper associations and began building out the views. I then Proceeded to think out the Materials association and decided the most logical solution is that Materials `belongs_to` a Task. I then realized I also needed to aggregate the materials into totals, so I built a method that looks something like this:

```
def materials_total 
     total = 0self.materials.each do |m|
         total += m.price.to_i
       end`
       "$#{total.to_s[0..-3]}.#{total.to_s.last(2)}" 
   end```
		
Each subsequent layer up then got a similar method to help aggregate the data. 

Next I focused on Workers. This one puzzled me. I wanted the User to create the Worker, and for the User to be able to drill down into the Worker to see where they are assigned and to assign, and destroy a worker easily, but I also wanted this to be possible directly from a Task. I decided a join table would work to allow access if I made the Worker also `belong_to` a User. The Worker model ended up looking like this:

```
class Worker < ApplicationRecord
    belongs_to :user
    validates :name, presence: true
    has_many :worker_tasks
    has_many :tasks, through: :worker_tasks```
		
So I now also have a WorkerTasks table that `belongs_to :worker` and `belongs_to :task` tables respectively.

This got me this far. Now I wanted to be able to assign my tasks to workers so I built a method under my worker that I can call that shows all the available tasks associated with the User that the Worker `belongs_to` aaaand BAM! We have `available_tasks` that can be called on my worker:

```def available_tasks
        tasks = []
        self.user.tasks.each do |t|
            if !self.tasks.include?(t)
                tasks << t
            end
        end
        tasks
    end```
		
This self filters through the conditional `if` statement and allows for a dropdown that shows all tasks not associated with this worker allowing the assignment. 

So far so good, right?

I then worked out my views and knocked out a bunch of functionality. 

I had a hiccup with OAuth for facebook because i used `redirect_to` instead of `render` in my controller method, but It was a lesson learned. 

I also had an interesting time with the nested resources. I learned that when using, for example, `user_worker` methods I need to feed in both the `user_id` and the `worker_id`. So instead of my link looking something like this:

```<%= link_to "Edit #{@worker.name}", user_worker_path(@worker) %>```

It needed to be:

```<%= link_to "Edit #{@worker.name}", user_worker_path(@worker.user, @worker) %>```

So the program can catch the two seperate `id`'s. for the route.

All in all this is a great learning experience and I am excited to keep working on this one. If you have any input or are as excited about this as I am please feel free to reach out. Thanks for reading and enjoy! 

