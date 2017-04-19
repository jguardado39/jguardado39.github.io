---
title: Creating a Category Based Pagination in Liquid for Jekyll without Gems
date: 2017-04-02 17:26
categories: adv-jekyll
series:  Advanced Customization of Jekyll

---
In this post, I shall describe the Paginator I wrote purely in Liquid. This was my first main feature, thus was a little rough on the edges. It was also the feature that convinced me to ditch purely Liquid based solutions since documentation and debugging of it is atrocious.

## TL;DR
For those that are impatient, here is the code that I used.

>Limitation: One category per post.


<div id="spoiler" style="display:none">
<code>
&lt;ul class="pager"&gt;
&#123;% assign prev = "" %&#125;<br>
&#123;% assign next = "" %&#125;<br>
&#123;% assign stop = false %&#125;<br>

&#123;% for post in site.posts%&#125;<br>
  &#123;% if post == page %&#125;<br>
    &#123;% assign stop = true %&#125;<br>
  &#123;% elsif post.categories == page.categories %&#125;<br>
    &#123;% if stop %&#125;<br>
        &#123;% assign prev = post.url %&#125;<br>
        &#123;% assign pTitle = post.title %&#125;<br>
        &#123;% break %&#125;<br>
    &#123;% else %&#125;<br>
        &#123;% assign next = post.url %&#125;<br>
        &#123;% assign nTitle = post.title %&#125;<br>
    &#123;% endif %&#125;<br>
  &#123;% endif %&#125;<br>

&#123;% endfor%&#125;<br>

&#123;% if prev != "" %&#125;<br>
  &lt;li class="previous"&gt;&lt;a href="&#123;&#123; prev &#125;&#125;"&gt;&larr; Previous Page  -  &#123;&#123;pTitle&#125;&#125;&lt;/a&gt;&lt;/li&gt;<br>
&#123;% endif %&#125;<br>
&#123;% if next != "" %&#125;<br>
    &lt;li class="next"&gt;&lt;a href="&#123;&#123; next &#125;&#125;"&gt; Next Page  -  &#123;&#123;nTitle&#125;&#125; &rarr;&lt;/a&gt;&lt;/li&gt;<br>
&#123;% endif %&#125;<br>
&lt;/ul&gt;
</code>
</div>
<button title="Click to show/hide code" type="button" onclick="if(document.getElementById('spoiler') .style.display=='none') {document.getElementById('spoiler') .style.display=''}else{document.getElementById('spoiler') .style.display='none'}">Show/Hide Code</button>


## Concept
The concept behind this code is rather simple. Have a previous button and a next button, that only takes posts from the same category.

## Implementation
#### Declare Variables

<code>&#123;% assign prev = "" %&#125;<br>
&#123;% assign next = "" %&#125;<br>
&#123;% assign stop = false %&#125;<br>
</code>
I began by declaring some variables, namely prev and next, which shall hold their respective urls. These shall be initialized as blank strings (URLs will be Strings and Java habits kicked in).

Stop shall be declared as a Boolean, where it shall be true once the current page is found.

#### For Loop
<code>
&#123;% for post in site.posts%&#125;<br>
  &#123;% if post == page %&#125;<br>
    &#123;% assign stop = true %&#125;<br>
  &#123;% elsif post.categories == page.categories %&#125;<br>
    &#123;% if stop %&#125;<br>
        &#123;% assign prev = post.url %&#125;<br>
        &#123;% assign pTitle = post.title %&#125;<br>
        &#123;% break %&#125;<br>
    &#123;% else %&#125;<br>
        &#123;% assign next = post.url %&#125;<br>
        &#123;% assign nTitle = post.title %&#125;<br>
    &#123;% endif %&#125;<br>
    &#123;% endif %&#125;<br>
    &#123;% endfor %&#125;<br></code>


This is the main part of the code. It shall iterate through every post on the site (everything in `_posts` and as far as I am aware in its sub-folders too). It is important to note that you are **iterating from newest to oldest**.


  First we ask if the current post in the for loop is equal to the current post. If it is, we shall set stop to true and go on do the loop one more time (interrupted via a break), to obtain the previous post.
  >* Optimization Note: I suspect post is a complete copy of all the HTML, so I would advise using `post.title` if your post titles are unique.
  >* Limitation: We are assuming that all pages are unique (why would they not be, just link them if not).
  >* Limitation: All pages have one category, otherwise we are bunching up pages that share the exact same category list. Possible workaround would be to try and [splice](https://help.shopify.com/themes/liquid/filters/string-filters#slice) the category into multiple strings or simply to use tags for what multiple categories were planned to be used for.

Assuming `stop==false`, we shall record the current page's url as next. We shall also assign `nTitle` to the current pages title. When the correct page is found, nTitle and next shall be the data from the next page.

Assuming `stop==true`, we shall record the same data as before, simply in `prev` and `pTitle`. The difference being, that we break the for loop at the end, as we have completed our routine and have the data needed.

#### If Statements
<code>
&#123;% if prev != "" %&#125;<br>
  &lt;li class="previous"&gt;&lt;a href="&#123;&#123; prev &#125;&#125;"&gt;&larr; Previous Page  -  &#123;&#123;pTitle&#125;&#125;&lt;/a&gt;&lt;/li&gt;<br>
&#123;% endif %&#125;<br>
&#123;% if next != "" %&#125;<br>
    &lt;li class="next"&gt;&lt;a href="&#123;&#123; next &#125;&#125;"&gt; Next Page  -  &#123;&#123;nTitle&#125;&#125; &rarr;&lt;/a&gt;&lt;/li&gt;<br>
&#123;% endif %&#125;<br></code>


These if statements shall be in charge of displaying the two buttons that the user can click on. In the event that prev was not initialized, aka. the first post, it shall simply be skipped. The same applies for next, only that it is the newest post in the category. I am not sure, but you might need to use the HTML codes for the left and right arrows (`&larr;`, `&rarr;`).

#### CSS
The buttons were generated via CSS, using List Items in an Unordered List.
```
.pager{padding-left:0;margin:20px 0;text-align:center;list-style:none}
.pager:before,.pager:after{display:table;content:" "}.pager:after{clear:both}
.pager:before,.pager:after{display:table;content:" "}
.pager:after{clear:both}
.pager li{display:inline}
.pager li>a,.pager li>span{display:inline-block;padding:5px 14px;background-color:#fff;border:1px solid #ddd;border-radius:15px}
.pager li>a:hover,.pager li>a:focus{text-decoration:none;background-color:#eee}
.pager .next>a,.pager .next>span{float:right}
.pager .previous>a,
.pager .previous>span{float:left}
.pager .disabled>a,.pager .disabled>a:hover,.pager .disabled>a:focus,.pager .disabled>span{color:#999;cursor:not-allowed;background-color:#fff}
```
Credit: [Herring Cove](https://github.com/arnp/herring-cove), by [@Arnp](https://github.com/arnp)

Note: I suspect I may have gotten an enter wrong in the CSS, you can find the original [here](https://raw.githubusercontent.com/Aevyz/aevyz.github.io/master/css/bootstrap.min.css)

**EDIT**: In the event that you have long file names, you may wish to add `"max-width: 50%"` (or any number under `50%`, I currently have `47%`) to your CSS or to the `<a>` tags , as then the buttons do not flow to the other side.

## Working Copy

The current Paginator used is the one described here. Here are the links to the [Paginator](https://raw.githubusercontent.com/Aevyz/aevyz.github.io/master/_includes/seriespager.html) and [CSS](https://raw.githubusercontent.com/Aevyz/aevyz.github.io/master/css/bootstrap.min.css).

The Paginator is added via the standard Liquid
<code>&#123;% include seriespager.html %&#125;</code> tag. See my [`post.html`](https://raw.githubusercontent.com/Aevyz/aevyz.github.io/master/_layouts/post.html) file for an example to implementation.


## Evaluation
Whilst this project worked, it just proved to me that the Liquid Template Language has many small quirks that annoy me greatly. For instance, the inability to reverse an array. The inability to debug effectively without resorting to adding a comment in each line was annoying. Furthermore the fact that sometimes the page would not update itself when Liquid failed caused confusion as well (no error messages, build errors). That being said, I can see why Liquid is useful, as it can help write simple tasks out quickly and without Javascript. That being said, writing this out in Javascript only using liquid to obtain the page data and moving this data into a Javascript array would have been far more sensible use of time.

Evaluation TL;DR: Just use Javascript for most scripting.
