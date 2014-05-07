---
layout: post
title: "Fight whitespace with Git"
date: 2012-06-18
---

Last week I visited [Nordic Ruby](http://nordicruby.org/). [Yasuragi](http://www.yasuragi.se/) was an exceptional venue and there were many a speaker who did well and inspired the attendees. This post is the result of me taking notice of [Katrina Owen](http://twitter.com/kytrinyx) mentioning **whitespace removal** during her topic on **Therapeutic Refactoring**.

I've become somewhat allergic of trailing whitespace during my years of traversing code, so – naturally – I have a history of fighting whitespace and I thought I'd share one effective weapon, in this battle; [Git](http://git-scm.com/).

Git is fully aware of the troubles that developers encounter with whitespace when collaborating in projects and therefore gives you a bit of formatting and whitespace handling options out of the box. By default it catches trailing spaces and spaces before tabs at the beginning of the line. These are enough for the rest of this post so for futher information you'll need to read up on in the official [Git documentation](http://git-scm.com/book/en/Customizing-Git-Git-Configuration#Formatting-and-Whitespace).

Along with these configurable options Git also adds action hooks inside `<your-project>/.git/hooks` when initialized and they’re also nice enough to add a whitespace check inside the `pre-commit.sample` hook.

*Unfortunately* (yeah, not really) this file is not active by default and you either have to rename it (from `pre-commit.sample` to `pre-commit`) or create your own and add the following code in `<your-project>/.git/hooks/pre-commit`:</p>

``` sh
#!/bin/sh

if git rev-parse --verify HEAD >/dev/null 2>&1
then
  against=HEAD
else
  # Initial commit: diff against an empty tree object
  against=4b825dc642cb6eb9a060e54bf8d69288fbee4904
fi

# If there are whitespace errors, print the offending file names and fail.
exec git diff-index --check --cached $against --
```

Now before every commit and Git finds trailing whitespaces in your code it'll output something in the lines of:

``` sh
hello.txt:1: trailing whitespace.
+Hello World
```

Hopefully this small tip helps someone in the war against whitespace.

**Note**: You can bypass the pre-commit hook with `git commit --no-verify`.
