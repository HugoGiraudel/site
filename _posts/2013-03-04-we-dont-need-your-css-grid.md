---
title: We don’t need your CSS grid
keywords:
  - css
  - grid
  - layout
---

> You know what would be awesome? Another CSS grid system!  
> &mdash; No one ever.

In this era of multi devices, responsive design, frameworks and all this stuff, CSS grids have become more and more popular. The main purpose of these tools is to define a baseline in order to have a consistent and predictable layout in all situations.

This is a good idea, even an important one. Being consistent on all devices is a big deal, and CSS grids really help to figure this out.

So in the last few months, we have assisted to a bunch of new CSS grid systems, including [Twitter Bootstrap Grid module](https://getbootstrap.com/), [Zurb Fundation](https://foundation.zurb.com/), [960.gs](https://960.gs/), [The 1140px Grid](https://www.ramotion.com/agency/web-design/cssgrid/), [Blueprint](http://www.blueprintcss.org/), [KNACSS](https://www.knacss.com/),  [YAML](http://www.yaml.de/), [Ingrid](http://piira.se/projects/ingrid/), [Golden Grid System](https://goldengridsystem.com/), [InuitCSS Grid module](https://github.com/inuitcss), [Toast](https://daneden.github.io/Toast/) and I probably forget [a bunch of those](http://usablica.github.io/frontend-frameworks/compare.html).

**They all are great grid systems**. This makes me get to the point…

## We don’t need yours

Sad but true. We do not need your CSS grid, framework or whatever you like to call it. There are already too much, some of them are built by professional, teams and CSS architects, which means they will always be better than yours.

Now don’t get me wrong: **building your own is a good thing**. But people don’t need it. Ask yourself this: between all the existing grids, including ones with hundreds of closed issues, why would I chose yours?

Unless you’re coming up with something **really** interesting and innovative like [Trevor Davis](https://twitter.com/trevor_davis) did with his [Diamond Grid](https://viget.com/inspire/who-says-the-web-is-just-for-squares), or [Harry Roberts](https://twitter.com/csswizardry) with [CSSWizardry-Grids](https://csswizardry.com/2013/02/introducing-csswizardry-grids/), there is no reason people should pick yours among all the others. Sorry.

But wait… There’s more.

## You don’t need yours either

Yes. Even you, do not need your own grid system. At least in most cases. Let’s think about it: either your project truely need a grid and you’d better go with an existing one which had proven to be reliable, or you project is small enough to not need one thus you don’t even need your own.

Given this postulate, we can ask ourself why are there that many grid systems? Because it’s fun to do, especially when you’re building it upon a CSS preprocessor. It is a very good exercise to practice CSS skills and preprocessor learning.

## Keep It Simple, Stupid!

You may be familiar with the KISS principle which says things are generally better when they are simple. This works for CSS grids too.

If you are working on a simple layout, even a responsive one, you’ll find that you can do things by hand without much hassle. I was first using 1140px Grid on this site until I realized it weigh a few kilobytes for what could be done in about 6 or 7 lines of CSS.

Once again, don’t get me wrong. **I don’t say grids are bad, or shouldn’t be used. I’m just warning you from using a grid when you don’t need one.** It can do more harm than good sometimes.

## Final words

If you haven’t read [this good article](https://css-tricks.com/dont-overthink-it-grids/) by Chris Coyier about not overthinking grids, then you definitely should.

Just don’t overthink grids. Unless you’re building a fully fluid responsive 3+ columns layout, try doing your CSS architecture without loading thousand of bytes.

Keep it simple.
