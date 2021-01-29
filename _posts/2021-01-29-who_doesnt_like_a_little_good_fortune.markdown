---
layout: post
title:      "Who Doesn't Like a Little Good Fortune?"
date:       2021-01-29 18:59:25 +0000
permalink:  who_doesnt_like_a_little_good_fortune
---

I was searching for a good ideas for this project, brainstorming if you will, and my wonderful wife says, "lets get some Chinese for dinner." I had thought about some sort of tax calculating app... or maybe some social networking app, but in the end it all seemed so derivative. Sitting after dinner laughing with my kids about their funny fortunes and looking at some bunk piece of pseudo-intellectual prediction i was delivered through my own piece of dry folded waffer i thought to myself, "wouldn't it be nice if every fortune was some form of positive affirmation or message that made you laugh?" So, That's what I built. 

This was a very cathartic build for me. The API came together rather quickly, and I enjoyed the practice manipulating the DOM using Javascript. It reminded me of doing trim work as a carpenter, where building the backend might be more foundational, this was what made it all look pretty. I also enjoyed working with the CSS. 

One area where I ran into an interesting but of struggle was using a single login function I originally had a bit of code that looked like the following:

  `def create
     user = User.find_or_create_by(user_params)
     user.authenticate(params[:user][:password])
     fortunes = Fortune.where(user_id: user.id)
     render json: {user: UserSerializer.new(user).to_serialized_json, fortunes: fortunes} 
  end`
	
 I figured the function would be able to locate the user or create one if none was located. What I did not anticipate was that since I was using strong params (see below) the SQL was searching for an exact match using all parameters fed into the function.  
 
`def user_password
   params.require(:user).permit(:name, :email, :password)
end`

Oddly, in the context of the create method, when I `pry`ed in,  the password parameter is not showing as allowed. Baffled I  added in an if statement to render the full error messages to see what was going on. 
	
	  `def create
       user = User.find_or_create_by(user_params)
			 if user.valid?
            fortunes = Fortune.where(user_id: user.id)
            render json: {user: UserSerializer.new(user).to_serialized_json, fortunes: fortunes} 
       else
            render json: {errors: user.errors.full_messages}
       end
	end`
	
What I found was that the api was trying to find a column called `users.password` which, incidentally, didnt exist since I had used `password_digest` so I could use the method `has_secure_password` that comes with Ruby and the `bcrypt` gem which together will automatically salt the password, encrypt it and add the suffix `_digest` to `password` to store it. 
	
Once I figured this out I split my strong params into two methods. One `user_params` that included the password, the other `user_password` that included the password.  

`def user_params
   params.require(:user).permit(:name, :email)
end`

`def user_password
   params.require(:user).permit(:name, :email, :password)
end`

I could then feed these into my create method using an or statement so that if a user isn't found using the name and email, it is created using name, email, and password. I also added password authentication and a simple error message. 
	
	`def create
    user = User.find_by(user_params) || User.create(user_password)
    if user.valid? && user.authenticate(params[:user][:password])
      fortunes = Fortune.where(user_id: user.id)
      render json: {user: UserSerializer.new(user).to_serialized_json, fortunes: fortunes} 
    else
      render json: {errors: "Login Failed"}
    end
	end`
	
In the end this was an interesting error to run into and debug. I have to admit it felt kind of lazy using a single controller function to build this functionality, but I was trying to provide a MVP.

If you care to take a look at the project its located here:: [https://github.com/JoeDeGr/HappyCookieApp.git](http://)

Thanks for reading! 
