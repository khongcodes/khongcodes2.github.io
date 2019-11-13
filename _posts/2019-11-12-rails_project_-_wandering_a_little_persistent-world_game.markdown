---
layout: post
title:      "Rails Project - Wandering: a little persistent-world game"
date:       2019-11-12 04:44:17 -0500
permalink:  rails_project_-_wandering_a_little_persistent-world_game
---

![](https://i.imgur.com/r2XANrb.png)

*Above: an entity relationship diagram for the project, which can be found [here.](https://github.com/khongcodes2/Wandering)*

We're supposed to think in metaphors, right?
User has blog post. Blog post has comments. Blog post and users also have likes. And once you close out the page and come back, user still has their post and comments.

I like games. So how about User has objects? Scavenged from debris. What can we do with the objects? For one, we can pick them up and drop them in new spaces, thereby giving them new associations. Having an object itself is an association - what if just the object-possession association existing caused a change in the user's attributes?

I'm sure this is nothing ground-breaking, but it was still way more work than I thought to implement
1. A mechanic for creating and ending a journey, through spaces (if your user can have many journeys, it's like your user has users)
2. I like rogue-like games - I particularly like discovering and navigating new spaces. So I want there to be an element of randomness in the paths available to a user at any given space. However, it would do no good to generate a new set of connected spaces each time a user enters a space. How do the spaces have any meaningful relationship to each other if they change everytime they are accessed? But I also don't want to persist them to the database - there's only one copy of each record in there, and I like the idea of potentially multiple users accessing the records at the same time, so we can't allow the space to have a saved attribute describing the spaces it's linked to. I want the space relationship to reset each time a new journey is started or ended - as journey start and finish are mechanized through the cookie, it makes sense to have space relations stored with the cookie too, as they are tied more to the one journey than the set of spaces which will persist across journeys. I created a sort of serializing method to encode information about what spaces are connected to what spaces as new connections are randomly generated - I was careful to not allow generation of too many spaces that are also connected to old ones.
3. Simple mechanics for picking up items and dropping them.
4. A seed generator that creates spaces and items by randomly combining sets of nouns and adjectives and description parts.

Ultimately this project was very challenging, but it was a challenge of my own making. If I had the time to continue working on this project, I would; as there's room for many more potential features, as far as I can see
* Logging events (this traveler passed through this space, this traveler left behind this item)
* Random events (specific to region)
* End journey and resume them right where you left off
* Profanity filter to protect the database
