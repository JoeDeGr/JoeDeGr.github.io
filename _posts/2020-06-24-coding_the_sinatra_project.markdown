---
layout: post
title:      "Coding the Sinatra Project."
date:       2020-06-25 02:20:30 +0000
permalink:  coding_the_sinatra_project
---


So, as I began in a previous post, I had originally intended on keeping some thematic continuity throughout my projects, but as I approached the start of this project my world had kind of changed. Covid-19 was in full effect and I had been spending increasing amounts of time with my children. So... I became inspired.

My daughter Stella is an avid reader and writes of fairy and tall tales and, at 7 years old, really enjoys creating and exploring new characters. She also enjoys creating both places for those characters and superpowers for them. So... sitting at the table asking my daughter about her latest project I began to realize this was a pretty complex relationship she was building. Let’s take a look at a Character she was developing.

Mia is a Mermaid. She Lives in Mertopolis. Ok, so we know She has a name, she has a Location, and she has an Archetype, or a set of characteristics. Stella has also informed me that she lives in a Seashell Castle and can talk to sea creatures. So, she also has a Building, and some special Powers. 

I began building the association like this:

![](https://drive.google.com/file/d/1Bf33HG9vyYmFCWynH7ANOBjNaH3ulQWT/view?usp=sharinghttp://)

From this I build out each of my character classes with their respective attributes as follows:

All things flow from the user, but the user doesn’t interact with them directly. My daughter has a character and the character has a Location, a Type, Powers etc... So, the `class User`  `has_many :characters` and my `class Character` will `belongs_to :user`.

Then I thought about out next link in the chain, the Character, and how they would interact with each class. What I came up with is that the Character has many Powers through an Archetype. A Mermaid won’t likely fly, unless they're of the flying variety and we can address that as a separate Archetype, but they will likely have the ability to swim under the water and talk to fish. So, my character Will have a many-to-many relationship with the type (many characters can, of course be Mermaids and we don’t want Mia to be lonely, and we may want to augment our Mermaids to fly at some point). Our character will also have a many-through relationship with Powers. 

Next, we discussed (yes, I did talk this out with my 7yo who was invaluably helpful) the Characters relationship to location. What I found worked best was also a many to many relationships. And we based this idea on the fact that the character may travel from place to place and we want to retain any of those travels. I thought this was sound advice so we went with it, the Character has many locations and, of course, the location must have many characters. 

I will digress for a moment to enumerate that I did in fact use Join Tables for these many-to-many relationships as I will illustrate below and, if you like you can poke around my repo here: [https://github.com/JoeDeGr/Character-Creator.git](http://). 

Next was the Buildings. Every good Mermaid lives in a castle, right? So, what’s our relationship to that? And like the Little Mermaid, does she have two? one on land and another in the ocean? And what about her treasure trove in the bottom of the sea with all her Human collectibles? This is where the many locations relationship quandary came from and we agreed that multiple characters should also have rights to a building, and that building should also have many characters, however, the building can only have one location. so... in the end we ended up with models for the rest of my primary classes that looked like the following:

`class Character < ActiveRecord::Base
    include Helpers::InstanceMethods
    belongs_to :user
    has_many :character_locations
    has_many :locations, through: :character_locations
    has_many :character_types
    has_many :archatypes, through: :character_types
    has_many :powers, through: :archatypes
    has_many :character_buildings
    has_many :buildings, through: :character_buildings
end'

class Location < ActiveRecord::Base
    include Helpers::InstanceMethods
    has_many :buildings
    has_many :character_locations
    has_many :characters, through: :character_locations
end

class Building < ActiveRecord::Base
    include Helpers::InstanceMethods
    belongs_to :location
    has_many :character_buildings
    has_many :characters, through: :character_buildings
end

class Archatype < ActiveRecord::Base
    include Helpers::InstanceMethods
    has_many :character_types
    has_many :characters, through: :character_types
    has_many :type_powers
    has_many :powers, through: :type_powers
end

class Power < ActiveRecord::Base
    include Helpers::InstanceMethods
    has_many :type_powers
    has_many :archatypes, through: :type_powers
    has_many :characters, through: :archatypes
end`

There were, of course, the appropriate classes for the joins and they `belongs_to` their respective counterparts, as required to establish proper id's to build the association. To give an example Mu `Character` class `has_many :character_buildings` so that it can `has_many :buildings, through: :character_buildings` and vice versa,  `Buildings` `has_many :character_buildings` so that it can `has_many :characters, through: :character_buildings`. This join table class allow us to associate many `character_ids` with a single building as well as many `building_ids` with a single character. Now, like Ariel, Mia can have a couple of castles and each of those castles have a few friends and maybe a handsome prince or kind king (or 3). However, the `Building` (our castle under the sea, let’s say) `belongs_to` the `Location` named "Under the Sea". But Mia also has what we will call her "Treasure Trove" of human trinkets in this location, "Under the Sea" and this is allowed because the location `has_many :buildings` because the `Building` class can store the location information in its hash under `location_id`, forgoing the need for a join table. The SQL would look like this if you were to query it in TUX for the location with an `id` of 2:

`SELECT  "buildings".* FROM "buildings" WHERE "buildings"."location_id" = ? LIMIT ?  [["location_id", 2], ["LIMIT", 11]] `

Or, Select all the "buildings" from "buildings" where the "location_id" is equal to "2".

This would pull up our "Seashell Castle" and "Treasure Trove."


So now Mia or Ariel can have 3 locations with 3 places of power, and can both swim and fly if she likes and gain all the appropriate powers from those Archetypes, and even learn magic if she makes up with Ursula... or meets Gandalf... or any of a myriad of other scenarios. Stella approves but has now set me to the task of figuring out how she can illustrate these beauties and maybe begin recording some tall tales... or maybe even some real ones.

