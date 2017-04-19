---
layout: post

title:  Customizing The Projects Page

date: 2017-04-04 22:11

categories: GitHub_Sites

series:  A Non-Programmers Guide To GitHub Sites

---

The Projects Page comes by default with some sliding panels, however not all of the features on the page are functional when forked.

## Non-Working Features
The default copy of the site can be found [here](https://aevyztutorial.github.io/herring-cove-original/projects.html
).

As you can tell, Photography and Coding Buttons do not work. Furthermore the Lorem Ipsum must be replaced with your actual project descriptions.


### YAML Header

```
---
title: Projects
---
```
This HTML page simply requires a title definition. As it is not a post, the page's layout shall be that defined under `default.html`. Webpages that are not posts (basically everything not in the `_posts` folder), are not required to have dates or categories.

In this case, I have titled this page `Projects`, which shall set the page title, that is displayed at the top of the browser and each tab.

![Browser Tab and Top](/images/top-bar-projects.png)

### Customizing Header Text and Images

```HTML
<div class="project-container" style="background-image: url( ... )">
    <h1> -->Header of the page<-- </h1>
    <p> -->Subtitle<-- </p>
    <br>
    <center>
    <a href="#category1"><span class="label label-danger">category1</span></a>
    <a href="#category2"><span class="label label-danger light">category2</span></a>
    </center>
</div>
```
To customize the header of the page, you need to edit this code. For the header and subtitle blocks, you simply need to replace the placeholder text with your own.

In order to change the image, you will need to specify your own file. To do this simply replace the `...` in the code above with an url, like this:

```
<div class="project-container" style="background-image: url(https://www.imperial.ac.uk/ImageCropToolT4/imageTool/uploaded-images/shutterstock_64199689--tojpeg_1408098461475_x2.jpg)">
```

You can either host the image on your own repo or simply link to a place where it is hosted. By default, Herring-Cove obtains random images from `http://lorempixel.com/` of the size 900x200. The image will be automatically cropped to have a maximum height of 170px.

### <a id = "custombuttons"></a>Customizing Buttons
For this, we shall use the afore discussed code block:
```HTML
<div class="project-container" style="background-image: url( ... )">
    <h1> -->Header of the page<-- </h1>
    <p> -->Subtitle<-- </p>
    <br>
    <center>
    <a href="#category1"><span class="label label-danger">category1</span></a>
    <a href="#category2"><span class="label label-danger light">category2</span></a>
    </center>
</div>
```
To alter the buttons, you must simply replace the two instances of `categoryX` (X being a specific name) with the chosen category name. For example, if one were to have a coding section, one would write:
```HTML
<a href="#coding"><span class="label label-danger light">coding</span></a>
```
If you want to add another button, simply copy and paste the code and alter the text appropriately.

>Note: The `#` symbol is important for this to work.

Adding functionality to the buttons is discussed [further down](#funcbutton).

### Adding Your Projects

One of the project containers is created using the following code.

```
<div class="container">
  <div class="project-box">
    <div class="row">
      <div class="col-md-3 project-image">
        <img src=" -->Add a url to a picture here<-- " style="max-width: 145px;">
      </div>
      <div class="col-md-9 project-post">
        <h1>  -->Title Goes Here<--  </h1>
        <h4>  -->Subtitle Goes Here<--  </h4>
        <p class="meta"><small>&nbsp;<i class="fa fa-calendar-o"></i>  -->This Posts Year<--  </small></p><hr/>
        <div class="post">

        -->Your Content Goes Here<--

        </ul>
        </div>
      </div>
    </div>
  </div>
```
Simply fill in the placeholders and copy this for as many blocks as are required. It is recommendable to categorise your projects, so that you can have the buttons jump to specific categories for ease of use ([more info](#custombuttons)).

The Javascript used to make each block expand/contract is supplied by the theme, meaning we do not have to do any Javascript programming.

### <a id="funcbutton"></a>Adding Button Functionality
The point of your buttons is to have them jump to a specific point on the same page. This is done using anchors.

Before the first project in a given category, add a `<a id="category-name"></a>` anchor, replacing the placeholder category-name with the category name [chosen prior](#custombuttons).

Example:

```
<a id="lorem-ipsum"></a>
<div class="container">
    <div class="project-box">
        <div class="row">
            <div class="col-md-3 project-image">
                <img src="http://lorempixel.com/g/400/400/">
            </div>
            <div class="col-md-9 project-post">
                <h1>Project Name</h1><h4>subheading</h4>
                <p class="meta"><small>&nbsp;<i class="fa fa-calendar-o"></i> 2013</small></p><hr/>
                <div class="post">
                    "Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem. Ut enim ad minima veniam, quis nostrum exercitationem ullam corporis suscipit laboriosam, nisi ut aliquid ex ea commodi consequatur? Quis autem vel eum iure reprehenderit qui in ea voluptate velit esse quam nihil molestiae consequatur, vel illum qui dolorem eum fugiat quo voluptas nulla pariatur?"
                </div>
            </div>
        </div>
    </div>
</div>
```

>Note: You can use `<a id="category-name" />` instead of `<a id="category-name"></a>`, however this feature is not supported by some older browsers.<br>
>Note: You can technically use `name` as opposed to `id`, but it is [technically deprecated with HTML5](https://www.w3schools.com/tags/att_a_name.asp).

### Working Copy
To see a working copy of this in action, look at the [custom copy of the site](https://aevyztutorial.github.io/herring-cove-custom/projects.html) ([Source](https://raw.githubusercontent.com/aevyztutorial/herring-cove-custom/master/projects.html)).