---
layout: post
title:      "What seems disorienting objects...."
date:       2020-03-13 18:15:00 +0000
permalink:  what_seems_disorienting_objects
---


In this lab we want to create a virtual classroom withI feel like every time I approach a new topic it can seem SOOO hard to understand at first, however over time and with a little diligence the fog can lift. I felt this way with object orientation. The very first lecture I paused maybe 5 minute in to take a breath, and when it came to inheritance and modules I had my paper ready and had to watch the lectures twice, but once I started to dig in I really could see how these things made programing EASIER not harder.  I walked through the Intro to Inheritance Lab and really felt like I dug in to try to get how this all works by playing with the logic and adding to what was requested to try and get a handle on how these relationships work. 

In this lab we want to create a virtual classroom with a teacher and many students. Each of these classes will have some basic functionality. To contain this we can create a ```User``` class that can develop this code and can be extended to the ```Teacher``` and ```Student```, and if at some point we decide to have, say a ```GuestSpeaker``` come in to teach we can extend these functions to them as well. 
The ```User``` class could create our new users and give them a name might look something like this:

````class User
  attr_accessor :first_name, :last_name
  def initialize
    @first_name = first_name
    @last_name = last_name
  end
end```

This initializes out user and gives them a first and last name. SWEET!
 
Now, we need a teacher. Our class ```Teacher``` is a type of ```User``` and inherits its functionality from that. 
```class Teacher < User```

It will have some KNOWLEDGE it can impart our students

  ```KNOWLEDGE = ["a String is a type of data in Ruby", "programming is hard, but it's worth it", "javascript     async web request", "Ruby method call definition", "object oriented dog cat class instance", "class method class variable instance method instance variable", "programming computers hacking learning terminal", "bash Ruby rvm update certs"]```

As good teachers do, out ```Teacher``` will impart some of that knowledge to either a single ```Student``` or all the ```Student```s that attend the class by calling the ```Student``` class. The ```Student``` gets taught by the ```Teacher```. The ```Teacher``` requires a ```Student``` to teach. 

  ````def teach
     KNOWLEDGE.sample
  end
	
  def teaches_class
    some_knowledge = self.teach
    Student.all.each do |student|
       student.learn(some_knowledge)
       puts "Thank you #{@first_name}, #{student.first_name} just learned: #{student.knowledge.sample}"
     end
  end
end```

Our ```Students``` will inherit the access through the ```User``` class, but we need a way to track all of our ```Student```s, so we create and ```@@all``` array that will collect each student on initialization that, and each ```Student``` will get pushed into and each ```Student``` will create an array of ```@knowledge``` that will store what they individually learn. In addition, the ```Teacher``` will ```.teach``` our ```Student```s how to ```.learn```. Our ```Student``` class would look something like this:


```class Student < User
  attr_accessor :knowledge
  @@all = []
  def initialize
    @@all << self
    @knowledge = []
  end
  def self.all
    @@all
  end
  def learn(knowledge)
    @knowledge << knowledge
  end
  def knowledge
    @knowledge
  end
end ```

If we create a ```Teacher.new(“Avi”)```, and a ```Student.new(Steve)```, and “Avi” teaches “Steve”, we get :

“Thank you Avi, Steve just learned: a String is a type of data in Ruby”

If we then add “Jim”, “Kim”, and “Bob” and “Avi” holds a webinar with all our students we get output of:

“Thank you Avi, Steve just learned: javascript async web request”
“Thank you Avi, Jim just learned: javascript async web request”
“Thank you Avi, Kim just learned: javascript async web request”
“Thank you Avi, Bob just learned: javascript async web request”
“Thank you Avi, Joey just learned: javascript async web request”

We can extend this by adding a class and the teachers could have many students through the class, and the students could learn from many teachers from various classes but those are discussions for another post, but warrant note as we can see how these concepts could build on each other. 
