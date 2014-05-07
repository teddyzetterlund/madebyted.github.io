---
layout: post
title: "Semantic placeholder links"
date: 2012-06-21
---

Another overlooked specification detail.

An unrelated discussion at work yesterday ended up with my colleague [Stefan Lindbohm](http://twitter.com/kolizz) having a read-through of the [specification for the anchor element](http://developers.whatwg.org/text-level-semantics.html#the-a-element) in which he found an interesting section that I’m not sure if I was aware of before.

> If the `a` element has no `href` attribute, then the element represents a placeholder for where a link might otherwise have been placed, if it had been relevant.

I know I’ve seen and reacted to the browser behavior when an `href` attribute isn’t present but I’m pretty sure I hadn’t looked it up in the specification before.

When Stefan read this aloud I immediately saw the opportunity for ditching the `span` element for links targeting the current page and replace them with an anchor element without an `href` attribute.

The specification confirms my thoughts with an example.

> If a site uses a consistent navigation toolbar on every page, then the link that would normally link to the page itself could be marked up using an a element:

``` html
<nav>
  <ul>
    <li><a href="/">Home</a></li>
    <li><a href="/news">News</a></li>
    <li><a>Examples</a></li>
    <li><a href="/legal">Legal</a></li>
  </ul>
</nav>
```

Having this change done in your markup shouldn’t be much more than modifying your `a` element styles a bit. I know I’ll try out this approach from now on.
