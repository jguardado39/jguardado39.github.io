---
layout: post

title:  Creating a Category Based Collapsible List

date: 2017-04-10 11:54

categories: adv-jekyll

series: Advanced Customization of Jekyll

---
The idea behind this project was to have a collapsible list, containing links to specific anchors on the post page. This would make the site a bit easier to use and better show off the post series. Despite this, I still wished to keep functionality for those disabling JavaScript.

>Warning: This feature shall require JavaScript. You could rewrite this in Liquid, however the Collapse feature used requires JavaScript, thus making a fully Liquid solution not possible (and needlessly complicated).

## TL;DR
Here is the code that I used to generate the sidebar for this specific site. Also this post assumes that all posts have a `series` tag, which contains their category name in long form (alternatives below). **Very likely** you shall need to customize the CSS, as this CSS is pretty hard coded to my needs.


<button data-toggle="collapse" data-target="#nocss">CSS Free Version</button>

<div id="nocss" class="collapse">
<h4>HTML Anchor</h4>
<pre><code>
&lt;a id="noscript" href="/posts.html" data-toggle="collapse">Blog Series&lt;/a>
&lt;script>document.getElementById("noscript").href="#postCategories";&lt;/script>

&lt;div id="postCategories" class="collapse">
&lt;ul id="replace">
  &lt;li>JavaScript Failed</li>
&lt;/ul>
&lt;/div>
</code></pre>
<h4> JavaScript </h4>
<pre>
<code>
&lt;script&gt;
  var catArray = [];
  var list = "";

  &#123;% for pg in site.posts %&#125;
    var found=false;
    for(i = 0; i<catArray.length;i++)&#123;
      if(catArray[i]=="&#123;&#123;pg.categories&#125;&#125;") found=true;
    &#125;
    if(!found)&#123;
      catArray.push("&#123;&#123;pg.categories&#125;&#125;");
      list='&lt;li>&lt;a href="&#123;&#123;site.baseurl&#125;&#125;/posts.html#&#123;&#123;pg.categories&#125;&#125;">&#123;&#123;pg.series&#125;&#125;&lt;/a>&lt;/li&gt;'+list;
    &#125;

  &#123;% endfor %&#125;

  document.getElementById('replace').innerHTML = list;

&lt;/script&gt;
</code>
</pre>

</div>


<button data-toggle="collapse" data-target="#css">Adapted for Herring-Cove Version</button>

<div id="css" class="collapse">
<h4>HTML Anchor</h4>
<h6>Desktop</h6>
<pre><code>
&lt;a id="desktop_noscript" href="/posts.html" data-toggle="collapse">Blog Series&lt;/a>
&lt;script>document.getElementById("desktop_noscript").href="#desktop_postCategories";&lt;/script>

&lt;div id="desktop_postCategories" class="collapse">
&lt;ul id="desktop_replace" style="padding-left: 55px">
  &lt;li>JavaScript Failed</li>
&lt;/ul>
&lt;/div>

</code></pre>
<h6>Mobile</h6>
<pre><code>
&lt;a id="mobile_noscript" href="/posts.html" data-toggle="collapse">Blog Series&lt;/a>
&lt;script>document.getElementById("mobile_noscript").href="#mobile_postCategories";&lt;/script>

&lt;div id="mobile_postCategories" class="collapse">
&lt;ul id="mobile_replace" style="padding-left: 55px">
  &lt;li>JavaScript Failed</li>
&lt;/ul>
&lt;/div>
</code></pre>

<br><h4>JavaScript </h4>
<pre>
<code>
&lt;script&gt;
  var catArray = [];
  var list = "";

  &#123;% for pg in site.posts %&#125;
    var found=false;
    for(i = 0; i<catArray.length;i++)&#123;
      if(catArray[i]=="&#123;&#123;pg.categories&#125;&#125;") found=true;
    &#125;
    if(!found)&#123;
      catArray.push("&#123;&#123;pg.categories&#125;&#125;");
      list='&lt;li style="font-size: 13px; text-indent: 0;line-height: 15px; padding-bottom: 1px; padding-top: 2px;">&lt;a href="&#123;&#123;site.baseurl&#125;&#125;/posts.html#&#123;&#123;pg.categories&#125;&#125;">&#123;&#123;pg.series&#125;&#125;&lt;/a>&lt;/li&gt;'+list;
    &#125;

  &#123;% endfor %&#125;

  document.getElementById('desktop_replace').innerHTML = list;
  document.getElementById('mobile_replace').innerHTML = list;

&lt;/script&gt;
</code>
</pre>

</div>

## Requirements and Limitations
For this project we shall be using the `Collapse` scripts provided by [Bootstrap](http://getbootstrap.com/).
Like all my other projects, I am assuming that we are using one Category per post and that there is a series tag, which contains the post's Category in long form.

>Alternatives to Series tag: As an alternative, you could have a JavaScript function that has an entry parameter of


## HTML Portion
##### Creating the Anchor
```HTML
<a id="desktop_noscript" href="/posts.html" data-toggle="collapse">Blog Series</a>
<script>document.getElementById("desktop_noscript").href="#postCategories";</script>
```
As we are working with a section that is JavaScript based, it would be sensible to take into account, those wishing to use NoScript or similar JavaScript blocking tools. Therefore, we shall define our Anchor giving a link to the `posts.html` page. If JavaScript is enabled, the following script shall replace the anchor's `href` to collapse/expand the following list.

The data-toggle tag in the anchor, shall allow us to toggle whether or not the object ID'd as `#postCategories` is shown.

>Note for Herring-Cove Users: HC has two different navigation bars, so you are required to copy the code once for desktop and once for mobile/small screen devices. This is the reason behind the naming.

##### Collapsible List
```HTML
<div id="postCategories" class="collapse">
<ul id="desktop_replace" style="padding-left: 55px">
  <li>JavaScript Failed</li>
</ul>
</div>
```
Now seeing as we have created an anchor, we need to create the list in which we shall insert objects.

First of all, we shall place this list in a collapsible `div`. The ID of this div, shall be the same as the one referenced in the script's href (excluding the `#` of course).

Next you shall define a list of your choosing. In this case, I have chosen to use an unordered list (`ul`). You must give it a ID, to allow it to replaced by the JavaScript. The style elements I have included help me position the list correctly. You most likely will **not** need this.

Out of personal preference, I have added a List Item which says "JavaScript Failed", to help with debugging. This is not required, but may prove helpful.

## JavaScript
<div>
<pre>
<code>
&lt;script&gt;
  var catArray = [];
  var list = "";

  &#123;% for pg in site.posts %&#125;
    var found=false;
    for(i = 0; i<catArray.length;i++)&#123;
      if(catArray[i]=="&#123;&#123;pg.categories&#125;&#125;") found=true;
    &#125;
    if(!found)&#123;
      catArray.push("&#123;&#123;pg.categories&#125;&#125;");
      list='&lt;li style="font-size: 13px; text-indent: 0;line-height: 15px; padding-bottom: 1px; padding-top: 2px;">&lt;a href="&#123;&#123;site.baseurl&#125;&#125;/posts.html#&#123;&#123;pg.categories&#125;&#125;">&#123;&#123;pg.series&#125;&#125;&lt;/a>&lt;/li&gt;'+list;
    &#125;

  &#123;% endfor %&#125;

  document.getElementById('desktop_replace').innerHTML = list;

  //If needed, uncomment the following line
  //document.getElementById('mobile_replace').innerHTML = list;

&lt;/script&gt;
</code>
</pre>
</div>

The way this works is that you have an Array of categories (`catArray`) and a String `list`, which contains the final HTML code you are going to insert.

You will be going through each post and checking if its category is already within `catArray`. If it is not, then it shall be added to `catArray`. In addition, a list element containing the series name (so the long form of the category name), as well as linking to its respective anchor on the `posts.html` page.

Finally at the end of the script, we shall insert the text into the `desktop_replace` and `mobile_replace` unlisted lists.

>Note: Style elements are required for my specific theme. You will likely need your own CSS to make this look appropriately.  








<button title="Spoiler" type="button" onclick="if(document.getElementById('ccspoiler') .style.display=='none') {document.getElementById('ccspoiler') .style.display=''}else{document.getElementById('ccspoiler') .style.display='none'}">Click to expand/hide JavaScript after Liquid</button>

<div id="ccspoiler" style="display:none">
<pre>
<code>
&lt;script&gt;
var catArray = [];
var list = "";
{% for pg in site.posts %}
var found=false;
for(i = 0; i&lt;catArray.length;i++){
  if(catArray[i]=="{{pg.categories}}") found=true;
}
if(!found){
  catArray.push("{{pg.categories}}");
  list='&lt;li style="font-size: 13px; text-indent: 0;line-height: 15px; padding-bottom: 1px; padding-top: 2px;"&gt;&lt;a href="{{site.baseurl}}/posts.html#{{pg.categories}}"&gt;{{pg.series}}&lt;/a&gt;&lt;/li&gt;'+list;
}

{% endfor %}
document.getElementById('desktop_replace').innerHTML = list;
document.getElementById('mobile_replace').innerHTML = list;
&lt;/script&gt;
</code>
</pre>

</div>








## Sample
Here is a demo version of the feature.

<a id="demo_noscript" href="/posts.html" data-toggle="collapse">Click Here</a>
<script>document.getElementById("demo_noscript").href="#demo_postCategories";</script>

<div id="demo_postCategories" class="collapse" style="indent">
  <ul id="demo_replace" style="padding-left: 55px">

</ul>


<script>
var catArray = [];
var list = "";
{% for pg in site.posts %}
var found=false;
for(i = 0; i<catArray.length;i++){
  if(catArray[i]=="{{pg.categories}}") found=true;
}
if(!found){
  catArray.push("{{pg.categories}}");
  list='<li style="font-size: 13px; text-indent: 0;line-height: 15px; padding-bottom: 1px; padding-top: 2px;"><a href="{{site.baseurl}}/posts.html#{{pg.categories}}">{{pg.series}}</a></li>'+list;
}

{% endfor %}
document.getElementById('demo_replace').innerHTML = list;
</script>
