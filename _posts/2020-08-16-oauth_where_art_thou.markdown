---
layout: post
title:      "O'Auth Where Art Thou?"
date:       2020-08-16 21:59:41 +0000
permalink:  oauth_where_art_thou
---


I clicked the link. `ERR_SSL_PROTOCOL_ERROR`. Ok... Clear Browsing data then click again... annnnd... `ERR_SSL_PROTOCOL_ERROR`. Ok.. "Breath in and out slowly" I think to myself, "Google... yes... Google..." As my hair began to grey I asked.... "OAuth... Where Art Thou?" 

So this tale begins with my realization that, at this particular moment,a Facebook account would be rather useful. I have a sordid relationship with Facebook so I decided to unshackle myself from the platform and deleted my account. but for this particular lesson, [OmniAuth](https://learn.co/tracks/full-stack-web-development-v8/module-13-rails/section-12-authentication/omniauth) there was some utility. Alas I proceeded to reverse engineer the lesson using Github. 

All things equal, I would have benefitted from skipping ahead because I would have watched a walkthrough and had a lesson that addresses this very topic (OmniAuth using Github as a `:provider`), however, the completionist in me doesn't like to give up, so I forged ahead.  

I had, as one does

1. Gone to Github and logged in.

2. Navigated to my dropdown and selected "Settings" then "Developer settings".

3. Then clicked "New Github App".... We were all good! 

4. I then filled in the required information... App name, Homepage URL as `https://localhost:3000/`, and my callback using the `app/:provider/callback` convention.

5. Ok... Add `gem 'dotenv'` to my gemfile so I can secure the login information 

6. Then insert `PROVIDER_KEY` and `PROVIDER_SECRET` into the `.env` file then reference that in .`gitignore` to ensure we are not oversharing... I'm thinking I got this......Too easy

7. Adjust the routes to reflect the changes we made `match '/auth/:provider/callback' => 'sessions#create', via: [:get, :post]`... Check! 

8. Now create the file `config/initializers/omniauth.rb` and configure the middleware.

```
Rails.application.config.middleware.use OmniAuth::Builder do
     provider :github, ENV['GITHUB_KEY'], ENV['GITHUB_SECRET']
end
```

Ok, boxes checked. Let's taker 'er out for a test drive...

`ERR_SSL_PROTOCOL_ERROR`

This, my friends, is where my story begins. 

So I did read ahead that the line of code, `config.force_ssl = true`  commented out of `config/application.rb`. So... I tried there first. Commented out or not... no change... still  `ERR_SSL_PROTOCOL_ERROR`.

So I Googled. 

The Secure Sockets Layer (SSL) is a standard technology for keeping an internet connection secure. Along the same vein is Transport Security Layer or (TSL), which is effectively an updated version of SSL. HTTPS or HyperText Transfer Protocol Secure appears in the URL when a website uses a secure certificate. 

Ok, Were getting somewhere, defining terms. Google On!

It seems this is a common error that can have quite a few causes. Honestly I thought I might be at this for a while. I found a pretty comprehensive article on [TheSSLStore.com](http://TheSSLStore.com) by Jay Thakkar that very neatly and conveniently walked you through many common causes of this error (Thakkar, 2020). 

I started at the beginning and updated my date and time settings.Then I went ahead and dumped my browsing data. then I read the next option, "Fix ERR_SSL_PROTOCOL_ERROR by clearing your SSL State" (Thakkar, 2020). and I thought on this for a while. 

I found this great Quora Thread (I know, not super scientific) where John Mocan from SSL Dragon says, "An SSL/TLS Certificate State-Cache contains the credentials stored in your browser’s cache after it finished the “SSL handshake” and opened a secure connection with a certain website" (Mocan, 2018). If the SSL is looking for a certificate AFTER the "SSL handshake," as he noted, and that's EXACTLY what we're trying to create and failing I must be looking for an error in the handshake. OK, now we're getting somewhere. 

So I reopened my settings on Github and navigated back through the "Settings" tab and selected "OAuth Apps" and went to my New App and took a close look at what I had done. I had made an interesting and crucial mistake. Both my local host and my call back were written using `https://` not the `http://` provided in the lesson above. This mismatch with the lab, presumably because I was using a `localhost`/ redirect path, seems to have thrown a wrench in the gears of my OAuth, which subsequently worked after the change. I do realize a more secure connection would be preferable and am working to iron out the kinks as I progress, but for now I'll take the small victory against the error codes. 


Thakkar, J. (2020, August 07). How to Fix 'ERR_SSL_PROTOCOL_ERROR' on Google Chrome. Retrieved August 16, 2020, from https://www.thesslstore.com/blog/fix-err-ssl-protocol-error/

What is an SSL State? (n.d.). Retrieved August 16, 2020, from https://www.quora.com/What-is-an-SSL-State

What is an SSL Certificate? (n.d.). Retrieved August 16, 2020, from https://www.websecurity.digicert.com/security-topics/what-is-ssl-tls-https


 


