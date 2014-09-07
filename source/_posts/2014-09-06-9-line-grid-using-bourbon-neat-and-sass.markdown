---
layout: post
title: "9 Line Grid using Bourbon, Neat and Sass"
date: 2014-09-06 11:11
comments: true
categories: [SCSS, Bourbon, Neat, Grid, Frontend]
---

I've started created a lot of my projects using the tools Thoughtbot puts out there. One of the tools I've recently started using is [Broubon](http://bourbon.io) and [Neat](http://neat.bourbon.io). Bourbon is a lightweight mixin library for Sass, and Neat is a grid framework.
<!-- more -->

Neat allows you to make grids using mixins. It makes defining your own grid very easy, and fast.

Here is an example of how you might create some basic grid elements using Broubon and Neat

```sass
.container {
  @include outer-container;
}

.row {
  @include row;
  &:last-child {
    // Zeros out right padding to make the last element fit
    @include omega;
  }
}

.grid {
  .col-1 {
    @include span-columns(1)
  }
  ...
  .col-12 {
    @include span-columns(12)
  }
}
```

Now you can see above, that defining all 12 columns of your basic grid layout can get a little bit annoying. Luckily, Sass comes with some built in features that allow us to simplify this process.

Here is how you can cut the whole grid fundamentals down to less than 20 lines.

```sass
// Define your column numbers in an array
$columns: (1,2,3,4,5,6,7,8,9,10,11,12);

.container {
  @include outer-container;
}

.row {
  @include row;
  .grid:last-child {
    @include omega
  }
}
.grid {
  // Each loop, to go through the column sizes
  @each $col in $columns {
    // Dynmaically name each column size col-X where X is the number
    &.col-#{$col} {
      // Include the mixin to span X number of columns
      @include span-columns($col);
    }
  }
}
```

There you have it, a simple, quick way to get a fundamental grid system set up!

Thanks [thoughtbot](http://thoughtbot.com) for all of your awesome [open source tools](http://github.com/thoughtbot)
