---
layout: post
title: "Sass :watches CSS4"
date: 2012-08-14
---

Reading the [CSS selectors level 4 specification](http://www.w3.org/TR/selectors4/) can be exhilarating. CSS is growing rapidly and browser support, while sometimes not as fast as we'd want, is steadily increasing.

Two weeks ago [A List Apart](http://www.alistapart.com/) published [Learning to Love the Boring Bits of CSS](http://www.alistapart.com/articles/love-the-boring-bits-of-css/) by [Peter Gasston](http://www.broken-links.com/), an excellent summary of forthcoming CSS4 units, functions and selectors.

The `matches()` pseudo-class selector was mentioned, and even though I've seen it before in [Mozilla's Firefox 4: -moz-any() selector grouping](http://hacks.mozilla.org/2010/05/moz-any-selector-grouping/), I immediately saw that it could be used today, by using [Sass](http://sass-lang.com/) – but before I show how, here's what the specification has to say about it:

> The matches-any pseudo-class, `:matches(X)`, is a functional notation taking a selector list as its argument. It represents an element that is represented by its argument.

This is useful for when you have big blocks of CSS with repeating selectors with one piece being different. Here's an example of how it has to be written today in pure CSS and then in CSS4 (example taken from the ALA article):

``` css
.home header p,
.home footer p,
.home aside p {
  color: #F00;
}

/* … is the same as … */
.home :matches(header,footer,aside) p {
  color: #F00;
}
```

The way you'd do this in Sass is not the same but it's both easy to do and understand – albeit in a different order.

You start with the selector list, followed by a nested use of the referencing parent selector between the other selectors:

``` css
/* Scss variant of :matches() */
header, footer, aside {
  .home & p {
    color: #F00;
  }
}
```

``` css
/* CSS output: */
.home header p,
.home footer p,
.home aside p {
  color: #F00;
}
```

This solution makes use of Sass' & selector which is used for [referencing parent selectors](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#referencing_parent_selectors_).
