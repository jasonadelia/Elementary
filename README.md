# Elementary
 
The goal of this script is to provide a way of achieving element queries for use in responsive web design. 98% or more of the credit for this code goes to [Respond JS](https://github.com/scottjehl/Respond). Just as Respond JS was meant to add support for CSS3 Media Queries in browsers that don't support them, Elementary adds support for element queries in browsers that don't support them, aka all browsers. Respond JS provided all of the heavy lifting of pulling the CSS via AJAX and parsing the stylesheets. With Elementary we are searching for a different pattern to identify elements and altered the logic slightly to determine when to apply the styles to the page.

[Demo page](http://scottjehl.github.com/Respond/test/test.html) (the colors change to show media queries working)

How does it work?
======
Basically, the script loops through the CSS referenced in the page and runs a regular expression or two on their contents to find element queries and their associated blocks of CSS.

From there, each element query block is appended to the head in order via style elements, and those style elements are enabled and disabled (read: appended and removed from the DOM) depending on how their min/max width compares with the width of the element that has been defined.

What is an element query?
======
An element query is a figment of my imagination. While [Respond JS](https://github.com/scottjehl/Respond) is a polyfill to add support for a new feature to older browsers, Elementary is trying to add a feature that doesn't exist. In order for the script to work I needed to come up with a CSS syntax that the script could look for to find all element queries as well as a way to identify which element on the page should be used to test it's size. I setted on "@element[selector]". "@element" is essentially the same as "@media". It will never change and is used simply to identify the block of code. Inside the square brackets is the selector to identify the element to be tested. This can be any valid CSS selector. 


Usage Instructions
======

1. Craft your CSS with min/max-width element queries to adapt your layout from mobile (first) all the way up to desktop


<pre>
    @element[.testimonial] screen and (min-width: 480px){
        ...styles for 480px and up go here
    }
</pre>

2. Reference the elementary.min.js script after all of your CSS (the earlier it runs, the greater chance users will not see a flash of un-media'd content)


CDN/X-Domain Setup
======

[Respond JS](https://github.com/scottjehl/Respond) supports cross-domain scripts so this should be feasible but I have not tested it yet.


Support & Caveats
======

Some notes to keep in mind:

- As this is a copy of [Respond JS](https://github.com/scottjehl/Respond), all the same caveats listed on that project apply here.

- This is javascript. It's not going to work at all for a user without javascript being enabled.

- This is far from a finished product. I'm putting this out there to get feedback and hopefully some help from the community to improve on this if it is worthwhile.