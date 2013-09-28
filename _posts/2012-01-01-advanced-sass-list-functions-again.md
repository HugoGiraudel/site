---
title: "Advanced Sass list functions - 2"
published: true
preview: true
comments: false
layout: post
---

<section>
<p class="explanation">In case you have missed my <a href="http://hugogiraudel.com/2013/08/08/advanced-sass-list-functions/">first article about this Advanced Sass List Functions library</a>, I recommand you to read it.</p>
<p>Heys guys, it's been a while I haven't posted anything! I have been pretty buse lately but I really miss writing so here it is: a short article about what's new on my Sass list functions library.</p>
<p>Well first of all, it has been added as a <a href="https://github.com/Team-Sass">Team-Sass</a> repository on GitHub. You probably know the Team-Sass collective. They have done ton of awesome things like <a href="https://github.com/Team-Sass/breakpoint">Breakpoint</a>, <a href="https://github.com/Team-Sass/Sassy-math">Sassy Math</a> and <a href="https://github.com/Team-Sass/uikit">UIKit</a>.</p>
<p>I am very glad to see my repo in there, so big thanks to them. :)</p>
</section>
<section id="added-functions">
<h2>New functions <a href="#added-functions">#</a></h2>
<p>I have added a couple of functions to make the library even more awesome like <code>purge()</code>, <code>is-symmetrical()</code>, <code>sum()</code>, <code>chunk()</code>, <code>count-values()</code> and <code>remove-duplicates()</code>.</p>
<h3>Purge</h3>
<p>I can't believe I didn't make the <code>purge()</code> function a while ago. Basically, it removes all non-true value of a list. Compass includes the <code>compact()</code> function which does pretty much the same thing.</p> 
<pre class="language-scss"><code>@function purge($list) {
  $result: ();
  
  @each $item in $list {
    @if $item != null 
    and $item != false 
    and $item != "" {
      $result: append($result, $item);
    }
  }
  
  @return $result;
}</code></pre>
<p>I think the code is self-explanatory. We loop through all items of the list: if it's not false, we append it. Then we return the new list. Easy peasy! It would be even easier if Sass had a boolean converter function. Then we could do something like this <code>@if !!$item { $result: append($result, $item); }</code>. Unfortunately, we can't.</p>
<h3>Is symmetrical</h3>
<p>I don't think this function has any major usecase, but you know, just in case I added it. It checks whether your list is symmetrical. It's based on my <code>reverse()</code> function.</p>
<pre class="language-scss"><code>@function is-symmetrical($list) {
  $result: ();

  @each $item in $list {
    $result: append($result, $item, space); 
  }
      
  @return $result == reverse($result); 
}</code></pre>
<p>Why do we recreate a list from the given one? Because <code>$result == reverse($result)</code> may fail depending on the list separator. If anyone has a better idea for this one, I'd be glad.</p>
<h3>Sum</h3>
<p>Same here, I don't think it has much point but I wanted to add it anyway. It takes all unitless number from the list and add them. The second parameter is a boolean enabling / disabling the removing of units. Basically, you can parseInt the value to get only the number.</p>
<pre class="language-scss"><code>@function sum($list, $force: false) {
  $result: 0;
  
  @each $item in $list {
    @if type-of($item) == number {
      @if $force and unit($item) {
        $item: $item / ($item * 0 + 1);
      }
      @if unitless($item) {
        $result: $result + $item;
      }
    }
  }
  
  @return $result;
}</code></pre>
<h3>Chunk</h3>
<p>The <code>chunk()</code> function is based on the equivalent PHP function <code>array_chunk()</code>. From the <a href="http://php.net/manual/en/function.array-chunk.php">PHP.net manual</a>:</p>
<blockquote class="quote">Chunks an <code>$array</code> into <code>$size</code> large chunks. The last chunk may contain less than <code>$size</code> elements.</blockquote>
<pre class="language-scss"><code>@function chunk($list, $size) {
  $result: ();
  $n: ceil(length($list) / $size);
  $temp-index: 0;

  @for $i from 1 through $n {
    $temp-list: ();

    @for $j from 1 + $temp-index through $size + $temp-index {
      @if $j <= length($list) {
        $temp-list: append($temp-list, nth($list, $j));
      }
    }

    $result: append($result, $temp-list);
    $temp-index: $temp-index + $size;
  }

  @return $result;
}</code></pre>
<p>We could probably make the code slightly lighter but I didn't want to dig too deep into this. I'll probably clean this up later. Meanwhile, it works great. If you find a usecase, hit me up!</p>
<h3>Count values</h3>
<p>Same as above, the <code>count-values()</code> function is inspired by <code>array_count_values()</code> that counts each value of the given array.</p>
<blockquote class="quote">Returns an array using the values of <code>$array</code> as keys and their frequency in <code>$array</code> as values.</blockquote>
<pre class="language-scss"><code>@function count-values($list) {
  $keys   : ();
  $counts : ();

  @each $item in $list {
    $index: index($keys, $item);

    @if not $index {
      $keys   : append($keys, $item);
      $counts : append($counts, 1);
    }

    @else {
      $count  : nth($counts, $index) + 1;
      $counts : replace-nth($counts, $index, $count);
    }
  }

  @return zip($keys, $counts);
}</code></pre>
<p>It's based on the built-in <code>zip()</code> function that merges several lists into a multi-dimensional list by preserving indexes.</p>
<pre class="language-scss"><code>$list: a, b, c, a, d, b, a, e;
$count-values: count-values($list);
// -> a 3, b 2, c 1, d 1, e 1</code></pre>
<h3>Remove duplicates</h3>
<p>There are times when you want to remove values that are present multiple times in a list. You had to do it by hand. Not anymore, I got your back.</p>
<pre class="language-scss"><code>@function remove-duplicates($list, $recursive: false) {
  $result: ();
  
  @each $item in $list {

    @if not index($result, $item) {
      @if type-of($item) == list and $recursive {
        $result: append($result, remove-duplicates($item, $recursive));
      }
      
      @else {
        $result: append($result, $item);
      }
    }

  }
  
  @return $result;
}</code></pre>
<p>You can even do it recursively if you feel so, by enabling recursivity with <code>true</code> as a 2nd argument. Nice, isn't it?</p>
</section>
<section id="improvements">
<h2>Improvements <a href="#improvements">#</a></h2>
<p>Not only I try to add new functions but I also do my best to make all functions as fast as they can be and the library as simple to understand as it can be so you can dig into it to change / learn stuff.</p>
<p>For example, you know we have <a href="http://hugogiraudel.com/2013/08/08/advanced-sass-list-functions/#removing">two remove functions</a>: <code>remove()</code> and <code>remove-nth()</code>. I have simplified those two greatly:</p>
<pre class="language-scss"><code>@function remove($list, $value, $recursive: false) {
  @return replace($list, $value, "", $recursive);
}

@function remove-nth($list, $index) {
  @return replace-nth($list, $index, "");
}</code></pre>
<p>Crazy simple, right? How come I haven't done this earlier? Well let's be honest, it has been a pain in the ass to come to this actually. I have faced an annoying issue: replacing by an empty string didn't remove the element from the list, it simply made it disappear. The difference is that the length of the list remained unchanged and this is a big deal.</p>
<p>This is why I had to create the <code>purge()</code> function. Both <code>replace()</code> and <code>replace-nth()</code> functions return a purged list, which means the empty strings get actually deleted from the list.</p>
<p>I have also used quite a couple of ternary operators along the way to make code lighter.</p>
</section>
<section id="what-now">
<h2>What now? <a href="#what-now">#</a></h2>
<p>Quite a few things! I still have to clean some functions because they are kind of messy at the time. I could still add new functions if you think of something.</p>
<p>I am unable to wait for Sass 3.3, it is going to be awesome. First, we will have a real ternary operator so the <code>if()</code> function will stop bugging around. </p>
<p>But there will also be new string manipulation functions and the <code>call()</code> function which will allow me to make a lot of new functions like <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/every">every()</a>.</p>
<p>Oh, and of course Sass 3.3 will bring map support which will be a whole another story, with a ton of new functions to make. It is going to be awesome, really!</p>
</section>