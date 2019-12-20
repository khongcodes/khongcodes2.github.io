---
layout: post
title:      "Hero's Journey Spread - Rails-as-API/Javascript project"
date:       2019-12-20 04:39:49 -0500
permalink:  heros_journey_spread_-_rails-as-api_javascript_project
---


A pre-post-mortem perhaps - because I feel dead and I've finally finished what can be conceivably called a 1.0 version of this. [Here](https://github.com/khongcodes2/Hero-s-Journey-Spread)'s the repo. Boy am I tired.

So what is this project? As I said in the repo README; lately I'd been feeling inspired by [Sasha Reneau's Spindlewheel deck and games.](https://www.teacabbage.com/spindlewheel) They've been creating an interesting deck of cards, meant to be interpreted tarot-like, to be used with in a set of tabletop games. I find them fascinating and awesome - a real rigorous attempt to take the format of interpretive oracle cards and craft them alongside a game system, in such a way that they are both chicken and egg - built neither is prime; they are built for each other.

I wanted to work with their cards really, but I didn't feel like I had the time or space to reach out and talk about usages, rights, etc. - so I decided to work with Waite-Smith tarot cards instead, seeing as they're a bit more... open source. So the first thing I did was conceive of and execute a design of the card side of the API, and then fill out all 78 cards, with their upright and inverted meanings. Once I had built an API that could return a dynamic amount of random cards, I turned towards building the basic shell of what I wanted the page to look like, and drafting out the eventListeners and DOM manipulation work that would make the website actually function - I was newer at that, so I wanted to make sure what I was envisioning was feasibly build-able (and actually I didn't even get to all of it - turns out features take a long time). Following that, loading had to work, and then saving.

Perhaps because reading and writing to API were my last centers of focus, I ended up implementing a system quite similar to Rails web apps' *session*. I created an object in global scope, and then read and wrote to it in performing what I considered micro-operations in the application, then used its state to inform my models what to change in the database. I feel that this design decision may also have been influenced by object-relation model thinking - just as models are intermediaries between clients and the database; my pointState object storing user changes to a saved resource served as a buffer between the user and my database.
