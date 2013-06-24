# Elementary
 
The goal of this script is to provide a way of achieving element queries for use in responsive web design. 98% or more of the credit for this code goes to [Respond JS](https://github.com/scottjehl/Respond). Just as Respond JS was meant to add support for CSS3 Media Queries in browsers that don't support them, Elementary adds support for element queries in browsers that don't support them, aka all browsers. Respond JS provided all of the heavy lifting of pulling the CSS via AJAX and parsing the stylesheets. With Elementary we are searching for a different pattern to identify elements query blocks instead of media query blocks and altered the logic slightly to determine when to apply those blocks to the page.

How does it work?
======
Basically, the script loops through the CSS referenced in the page and runs a regular expression or two on their contents to find element queries and their associated blocks of CSS.

From there, each element query block is appended to the head in order via style elements, and those style elements are enabled and disabled (read: appended and removed from the DOM) depending on how their min/max width compares with the width of the element that has been defined.

What is an element query?
======
An element query is a figment of my imagination. While [Respond JS](https://github.com/scottjehl/Respond) is a polyfill to add support for a new feature to older browsers, Elementary is trying to add a feature that doesn't exist. In order for the script to work I needed to come up with a CSS syntax that the script could look for to find all element queries as well as a way to identify which element on the page should be used to test it's size. I settled on "@element[selector]" for my syntax. "@element" is essentially the same as "@media". It will never change and is used simply to identify the block of code. Inside the square brackets is the selector to identify the element to be tested. This can be any valid CSS selector. 


Usage Instructions
======

1. Craft your CSS with min/max-width element queries to adapt your layout from mobile (first) all the way up to desktop


<pre>
    @element[.testimonial] screen and (min-width: 480px){
        ...styles for 480px and up go here
    }
</pre>

2. Reference the elementary.min.js script after all of your CSS (the earlier it runs, the greater chance users will not see a flash of un-media'd content)

Demos
======
- I first began thinking about this problem after a blog post by [Ian Storm](http://ianstormtaylor.com/media-queries-are-a-hack/). In there he describes a problem he was having with testimonials. I have created a [demo](http:) of how that issue could be solved with Elementary

- A classic example of how to use media queries is Chris Coyier's [Email Links Sidebar](http://css-tricks.com/css-media-queries/). In Chris' example the media queries were all based on the size of the sidebar within the parent container. If the size of the container were to change or you wanted to put those same links into a different context, say the footer, you'd have to redo all of that work. Here is a [demo](http:) where by using Elementary, the context doesn't matter since we are using the size of the element, not the viewport, to determine breakpoints.

- I exposed a run() function for Elementary. Calling this will trigger the logic to reapply the element query logic to the page. I created a [demo](http:) for where this could be useful. In this example we have a filter section that is collapsed and can be toggled open by the user. When the user clicks to open the section, in addition to the logic for opening / closing the filter section, we call elementary.run(). In the demo, if the table is no longer wide enough (now that the filters are shown) the last two columns are hidden from view.

CDN/X-Domain Setup
======

[Respond JS](https://github.com/scottjehl/Respond) supports cross-domain scripts so this should be feasible but I have not tested it yet.


Support & Caveats
======

Some notes to keep in mind:

- As this is a copy of [Respond JS](https://github.com/scottjehl/Respond), all the same caveats listed on that project apply here.

- This is javascript. It's not going to work at all for a user without javascript being enabled.

- This is far from a finished product. I'm putting this out there to get feedback and hopefully some help from the community to improve on this if it is worthwhile.