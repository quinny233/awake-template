---
title: An Insight into Shopify Liquid Inspector
subtitle: >-
  The new Chrome Extension tool released by Shopify, to help improve
  performance.
category:
  - Shopify Plus
  - Technical Performance
author: Liam Quinn
date: 2020-03-01T18:22:42.377Z
featureImage: /uploads/about-hero.jpg
---
## The Nutshell

Shopify, like pretty much every other hosted platform, has always had question marks around exactly how good a performance it is actually possible to achieve for a new site. Thankfully Shopify seem to have identified this issue as a key area for improvement - and are doing so on an ongoing basis from a server side perspective. 

But in a bid to help us help ourselves, Shopify have released a new tool - for inspecting and debugging Liquid code within the frontend template files. This means it is now easier to analyse the quality of how the frontend has been built, rather than just whether it looks good.

## The Deepdive

To begin using this tool and exploring which aspects of the Liquid code could be improved, there are a few initial steps to setup:

*Prereqs. You must be using Chrome as your web browser, and have access to the Store Owner account of the Shopify Store you are looking to inspect.*

1. Start by installing the Chrome Extension called "Shopify Theme Inspector for Chrome" - here's a link <https://chrome.google.com/webstore/detail/shopify-theme-inspector-f/fndnankcflemoafdeboboehphmiijkgp>
2. Navigate to your Shopify Store within the Chrome browser. 
3. Click the new Shopify icon which should sit within your extensions, in the top right corner of the browser window. You'll be prompted to login to the Store in order to use this.
4. Open up Chrome Developer Tools (Right-click -> Inspect), and switch to the Shopify Tab which should now have been added. 
5. Refresh the page, or click through to a page that you think may have performance issues.

You should now see a beautiful 'Flame Graph' just like this...

![Shopify Liquid Inspector flame graph](/uploads/screenshot-2020-03-17-at-11.53.35.png "Shopify Liquid Inspector flame graph")

As you can see from the image, this graph displays all the nodes of Liquid that are being loaded into that specific page; from the theme layout all the way down into the granular snippets - which you can then click into to poke your head further down whichever rabbit hole looks interesting. You can start to dig into which aspects of the page are causing big 'flames', and consider from a high level whether any aspects are out of proportion with their importance to the page. For example if a small feature is the cause of a big percentage of the graph - it's a good place to start in considering whether it can be refactored, or in some cases if it is worth removing completely. 

So to try and demonstrate a use case for this, I've added a new snipped of Liquid code into the template that was visualised in that initial image (above). So from this following image you can see the new snippet named "liquid-test" now getting loaded in, early in the page load.

![Shopify Flame Graph - Test Snippet](/uploads/screenshot-2020-03-19-at-14.24.40.png "Shopify Flame Graph - Test Snippet")

We can see from the above, that this new snippet accounts for ~5-10% of the graph now. Within this snippet, I've decided I wanted to output a flag for each product that is Tagged as 'featured'. So it's a basic loop through all products, checking each for a matching Tag, as follows:

```
{% for product in collection.products %}
    {% if product.tags contains "featured" %}
        
    {% endif %}
{% endfor %}
```

I can now dig a bit further to see how efficient this code is, clicking into the relevant section of the graph. As it expands out, we can see exactly how many nodes are within the loop (signifying the amount of products we're looping through - 10 in this case), and how many nodes are pulled out to the next level down (signifying the amount of matches - 3 in this case).

![Shopify Flame Graph - Three Nodes](/uploads/screenshot-2020-03-19-at-14.26.27.png "Shopify Flame Graph - Three Nodes")

To highlight this a little more, I went into my Shopify Admin and removed the 'featured' Tag from one of the Products. As expected, we're still looping through all 10 - but now there are only two nodes pulled out to the next level down:

![Shopify Flame Graph - Two Nodes](/uploads/screenshot-2020-03-19-at-14.27.50.png "Shopify Flame Graph - Two Nodes")

Next, I accidentally got my loops wrong - and have ended up nesting them so that the page loops through all products, then for each it loops through all products again looking for that 'featured' tag. It looks like this:


```
{% for product in collection.products %}
    {% if product.tags contains "featured" %}
      {% for product in collection.products %}
          {% if product.tags contains "featured" %}
            
          {% endif %}
      {% endfor %}
    {% endif %}
{% endfor %}
```

So referring back to the Flame Graph now, we can see that the length of that element of the graph has now extended because it's taking up a bigger proportion of the page load. As expected, when we dig back into it - we can see the loop now happening ten times, with the two matching nodes being pulled out each time. 

![Shopify Flame Graph - Double Loop](/uploads/screenshot-2020-03-19-at-14.28.57.png "Shopify Flame Graph - Double Loop")

And this is exactly the sort of inefficiency that this Shopify Liquid Inspector is perfect to debug. Without looking into the code line-by-line, something like this could easily go under the radar because it has no visual impact and still actually works. In terms of performance, it might not even be noticeable if you have a store with minimal products, and minimal Tags. But, the hit on performance would scale as the inventory increases. This poorly written code could be left lurking on the site, and only become noticeable when a new batch of 1000 products were added to the store - making the loops suddenly increase exponentially. 



## The End Result

conclusions here...