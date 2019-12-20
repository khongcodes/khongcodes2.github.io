---
layout: post
title:      "Changes to Wandering - Rails Project - models"
date:       2019-12-20 05:11:28 -0500
permalink:  changes_to_wandering_-_rails_project_-_models
---


Additional models added -

##### Memories
Actually probably what I've been looking for this whole time. Necessary, important - in an ideal-ish world where multiple people have used my application, they will be able to see traces of other users who had played the game before them. Marks left by precursors, items and spaces have memories. That was one of my visions for this whole project. So far I have implemented it as a kind of additional table connecting spaces and a journey, and items and a journey, (or all three in some cases) - but it's not 100% where I want it to be, because I believe I could get it to replace the join table space_memories - but it will take some refactoring in the future.

##### Moderator
I've added an admin column, marked as false for all but for the first user in the application (already generated thanks to my seeds. On all fields where users can input, I have methods scanning all input with regular expressions for common hate speech and offensive language. In cases where there is a match, the vowels in the offending section of text are replaced with \*\*asterisks\*\*. The admin is able to update and delete all flagged content (all tables have a 'flagged' column now, and all flagged content is gathered on one page for easy admin work.

I owe a lot on this project to Chris Fritz - his [Language Filter Ruby gem](https://github.com/chrisvfritz/language_filter) showed me a framework of logic on which I could build this section of my application.
