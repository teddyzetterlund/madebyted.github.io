---
layout: post
title: "Using Images as Labels Inside Forms in Internet Explorer 11"
date: 2013-11-22
---

If you’ve been around the web development community for a while it’s likely that the title of this post will remind you of an eight year old article written by [Jonathan Snook](http://snook.ca/about/), of [SMACSS](http://smacss.com/) fame, called [Using Images as Labels in Internet Explorer](http://snook.ca/archives/javascript/using_images_as).

## Image labels aren't clickable

Jonathan's article explains a bug in Internet Explorer where if you use an image inside a label the label won't be clickable. Guess what, the bug is back in Internet Explorer 11 with the only difference that now the whole thing has to be wrapped inside a form to fail. It works fine outside of a form.

Here's the markup for [a JSBin that demonstrations the problem](http://jsbin.com/UbiHOfE/1/edit):

``` html
<form>

  <!-- input inside label -->

  <label>
    <input type="radio">
    <img src="http://placekitten.com/50/50">
  </label>

  <!-- input outside of label referenced by for/id -->

  <input id="test-1" type="radio">

  <label for="test-1">
    <img src="http://placekitten.com/50/50">
  </label>

</form>
```

## Simply solved with CSS magic

In Jonathan's original article two JavaScript solutions are provided, one with jQuery and one without, use this if you don't want to clutter your <abbr>HTML</abbr> and <abbr>CSS</abbr> but I recommend not to depend on JavaScript and instead use the following solution.

We'll add two new elements to the markup. One that wraps the image and one that is positioned above the image through CSS usage and therefore renders the label clickable again. Another benefit (except no dependency) over the JavaScript solutions is that we don't *need* a `for` attribute on the `label`.

Here's the code revisited with a solution ([editable JSBin](http://jsbin.com/UbiHOfE/5/edit)).

``` html
<form>

  <!-- input inside label -->

  <label>
    <input type="radio">
    <span class="image-container"><!-- NEW -->
      <img src="http://placekitten.com/50/50">
      <span class="image-clickable"></span><!-- NEW -->
    </span>
  </label>

  <!-- input outside of label referenced by for/id -->

  <input id="test-1" type="radio">

  <label for="test-1">
    <span class="image-container"><!-- NEW -->
      <img src="http://placekitten.com/50/50">
      <span class="image-clickable"></span><!-- NEW -->
    </span>
  </label>

</form>

<style>

.image-container {
  /* the container needs display to
     be either inline-block or block */
  display: inline-block;
  position: relative;
}

.image-clickable {
  position: absolute;
  top: 0; bottom: 0;
  left: 0; right: 0;
}

</style>
```

**Note:** The `label` could just as well act as the wrapper element. IE doesn't care if the `input` is inside or outside of the `label`.

## What's next?

I've filled [a bug report](https://connect.microsoft.com/IE/feedback/details/809378/using-images-as-labels-inside-forms-in-internet-explorer-11) to Microsoft by following Rey Bango's excellent instructions for [submitting a bug report to Microsoft](http://blog.reybango.com/2013/02/28/submitting-an-internet-explorer-bug-to-microsoft) so I guess now we'll wait and see. Maybe it gets noticed faster if you comment on the bug report or know the right people on Twitter to nudge about it but other than that I suppose we'll have to live with the workaround for now.
