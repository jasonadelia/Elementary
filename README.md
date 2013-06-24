# Elementary
 
The goal of this script is to provide a way of achieving element queries for use in responsive web design. 98% or more of the credit for this code goes to [Respond JS](https://github.com/scottjehl/Respond). Just as Respond JS was meant to add support for CSS3 Media Queries in browsers that don't support them, Elementary adds support for element queries in browsers that don't support them, aka all browsers. Respond JS provided all of the heavy lifting of pulling the CSS via AJAX and parsing the stylesheets. With Elementary we are searching for a different pattern to identify element query blocks instead of media query blocks and altered the logic slightly to determine when to apply those blocks to the page.

How does it work?
======
Basically, the script loops through the CSS referenced in the page and runs a regular expression or two on their contents to find element queries and their associated blocks of CSS.

From there, each element query block is appended to the head in order via style elements, and those style elements are enabled and disabled (read: appended and removed from the DOM) depending on how their min/max width compares with the width of the element that has been defined.

What is an element query?
======
An element query is a figment of my imagination. While [Respond JS](https://github.com/scottjehl/Respond) is a polyfill to add support for a new feature to older browsers, Elementary is trying to add a feature that doesn't exist. In order for the script to work I needed to come up with a CSS syntax that the script could look for to find all element queries as well as a way to identify which element on the page should be used to test it's size. I settled on "@element[selector]" for my syntax. "@element" is essentially the same as "@media". It will never change and is used simply to identify the block of code. Inside the square brackets is the selector to identify the element to be tested. This can be any valid CSS selector. 


Usage Instructions
======

- Craft your CSS with min/max-width element queries to adapt your layout from mobile (first) all the way up to desktop


<pre>
    @element[.testimonial] screen and (min-width: 480px){
        ...styles for 480px and up go here
    }
</pre>

- Reference the elementary.min.js script after all of your CSS (the earlier it runs, the greater chance users will not see a flash of un-media'd content)

The selector
======
The script uses the selector specified to find all matching elements in the DOM and then tests each element to see if it meets the query that is specified. In the example above, the script will find all elements with a class of "testimonial" and test to see if each element is at least 480px wide. If it is, the script will dump the CSS block onto the page. 

It is very possible that there are multiple elements on the page that match the selector and that each of those elements could have a different size. Just because testimonial A is greater than 480px, doesn't mean that testimonial B is. We need to be able to assign styles only to the element that meet the criteria. To do this, the script will replace every instance of the selector inside of the element query block with a unique element query class and also apply that class to the element in the DOM. For example:

<pre>
    ... html file ...
    &lt;div class="testimonial"&gt;...&lt;/div&gt;

    ... css file ...
    @element[.testimonial] screen and (min-width: 8em ){
        .testimonial{
            font-size:1em;
        }
        .testimonial .avatar {
            width: 3.5em;
        }
    }
</pre>

If the testimonial is wider than 8em, the class "__eq1" would be added to the div and the following CSS would be appended to the page

<pre>
    .__eq1{
        font-size:1em;
    }
    .__eq1 .avatar {
        width: 3.5em;
    }
</pre>


Demos
======
- I first began thinking about this problem after a blog post by [Ian Storm](http://ianstormtaylor.com/media-queries-are-a-hack/). In there he describes a problem he was having with testimonials. I have created a [demo](http://jasondelia.com/Elementary/demo/signup.html) of how that issue could be solved with Elementary

- A classic example of how to use media queries is Chris Coyier's [Email Links Sidebar](http://css-tricks.com/css-media-queries/). In Chris' example the media queries were all based on the size of the sidebar within the parent container. If the size of the container were to change or you wanted to put those same links into a different context, say the footer, you'd have to redo all of that work. Here is a [demo](http://jasondelia.com/Elementary/demo/email-sidebar.html) where by using Elementary, the context doesn't matter since we are using the size of the element, not the viewport, to determine breakpoints.

- I exposed a run() function for Elementary. Calling this will trigger the logic to reapply the element query logic to the page. I created a [demo](http://jasondelia.com/Elementary/demo/table.html) for where this could be useful. In this example we have a filter section that is collapsed and can be toggled open by the user. When the user clicks to open the section, in addition to the logic for opening / closing the filter section, we call elementary.run(). In the demo, if the table is no longer wide enough (now that the filters are shown) the last two columns are hidden from view.

CDN/X-Domain Setup
======

[Respond JS](https://github.com/scottjehl/Respond) supports cross-domain scripts so this should be feasible but I have not tested it yet.


Support & Caveats
======

Some notes to keep in mind:

- As this is a copy of [Respond JS](https://github.com/scottjehl/Respond), all the same caveats listed on that project apply here.

- This is javascript. It's not going to work at all for a user without javascript being enabled.

- This is far from a finished product. I'm putting this out there to get feedback and hopefully some help from the community to improve on this if it is worthwhile.
