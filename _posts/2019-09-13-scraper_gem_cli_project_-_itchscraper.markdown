---
layout: post
title:      "Scraper Gem CLI Project - ItchScraper"
date:       2019-09-13 20:22:19 +0000
permalink:  scraper_gem_cli_project_-_itchscraper
---

##### This blog post refers to the project at this repository: [ItchScraper](https://github.com/khongcodes2/ItchScraper)

I'd say I'm pretty into the independent tabletop RPG and video game scenes. So when I thought about what information I'd like to scrape, I asked myself what website do I visit frequently, and [itch.io](http://itch.io) sprang immediately to mind. 

Since [Google took down Google+](https://www.zeshio.com/blog/2019/2/3/itchio-and-the-changing-landscape-of-tabletop-rpg-community), and in the wake of recent public scrutiny of the kind of cuts platforms like [Steam and Epic Games Store take from their creators' games sales](https://www.vice.com/en_us/article/nexeyx/why-are-gamers-mad-about-a-real-competitor-to-steam), [itch.io](https://itch.io/docs/creators/faq#how-much-does-itchio-cost) has become a place where independent creators of games, digital and analog alike, are flocking together.

As someone who believes that:
*  video games and role-playing games are a unique and powerful medium of artistic and creative expression and vision, and,

* democratization of games through increasing the accessibility of tools to make and share and sell and play games is good;

Itch is exciting and cool to me.

So! How I thought through this gem:
I normally access the front page of Itch, but Cernan pointed out in his lecture that websites that use React can be hard to scrape off of because they shift - and using the Chrome extension Wappalyzer, I found that the Itch front page uses React.

No problem! I can still make something that crawls menus of Itch to display in CLI what's available at the top of each category.

First, I found that Itch has 9 categories,
1. Games
1. Tools
1. Game assets
1. Comics
1. Books
1. Physical games
1. Soundtracks
1. Game mods
1. Everything else

and 5 sort methods,
1. Popular
1. New & Popular
1. Top sellers
1. Top rated
1. Most recent

through which it parses objects in each category. Rather than create some kind of array where each element is a category combined with a sort method (which would have 45 elements), I decided that the categories and sort methods should be displayed through two menus, and in each menu, when one of the items was picked, an add-on to the URL was selected from an array using the input indicating the item picked.

In the process of my programming, I referred to this as a nested menu structure. Upon retrospection, I'm not sure this is true, as it's not as if there is a separate Sort menu inside of each Category. I used the notion of inside/outside, though to program variables (like @nest_nav and @lvl3_nav) that keep track of the location of currently-viewed and previously-viewed menus.

They semantically are nesting - displaying popular objects within the category of games -  but that was just a matter of string interpolation. In reality it was just sending @lvl2_nav to lookup a specific index of one array, and sending @lvl3_nav to lookup a specific index in a different array.


