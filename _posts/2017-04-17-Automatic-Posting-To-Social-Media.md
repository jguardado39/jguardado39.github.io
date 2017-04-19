---
title: Automatically Posting Jekyll Posts to Social Media
date: 2017-04-17 15:48
categories: adv-jekyll
series:  Advanced Customization of Jekyll
---


Having a Social Media presence on Websites such as Twitter, Facebook, Pinterest, Reddit, Tumblr, just to name a few, can drive huge amounts of traffic to your posts, as well as offering you the opportunity to interact with your viewers, however posting things to all different Social Media accounts for every post can be a tedious task, and you may even forget to post on a particular site.  

### Setup
To set up automatic posting, we shall need to create an RSS Feed. The Feed shall automatically update itself whenever a new post is created. To do this, simply add `jekyll-feed` to your `_config.yml`'s gem list. Upon your site compiling, you will have an RSS Feed located at `<Your Site Domian>/feed.xml`.

Very likely, you shall require metadata. Using [OpenGraph Metadata](http://ogp.me/) should work for most sites, however consider checking for each Social Media Site for it's best practice notes. Here is a tutorial how to configure this in [Jekyll](http://davidensinger.com/2013/04/adding-open-graph-tags-to-jekyll/).

>Note: Twitter has it's own [protocol](https://dev.twitter.com/cards/getting-started), however [supposedly](https://blog.kissmetrics.com/open-graph-meta-tags/) accepts Open Graph as well.

### IFTTT
![IFTTT](/images/ifttt.png "IFTTT")


'If This Then That' does exactly what the name implies. Given a certain condition, a specific action will be executed. We shall be using this tool to post stuff to your social media. Simply [register](https://ifttt.com/join) for the site

### Creating an Automatic Post System

<br><br>
#### 1) To create an auto poster, simply press your user name followed by `New Applet`

![IFTTT New Applet](/images/ifttt-new-applet.png "IFTTT New Applet")

<br><br>
#### 2) Now press the `This` button

![IFTTT This](/images/ifttt-this.png "IFTTT This")

<br><br>
#### 3) Followed by RSS Feed

![IFTTT RSS](/images/ifttt-rss.png "IFTTT RSS")

<br><br>
#### 4) Choose New Feed Item or New Feed Item Matches
Choose whether or not you wish to have posts filtered, or simply just have every post trigger IFTTT.

![IFTTT Choice](/images/ifttt-rss-choice.png "IFTTT Choice")

<br><br>
#### 5) Configure your trigger to your specifications
>If you choose the item matches option, you will need to add a keyword.

![](/images/ifttt-rss-trigger.png)

<br><br>
#### 6) Select the `that` button

![](/images/ifttt-that.png)

<br><br>
#### 7) Select a Social Media Site and the Subsequent Posting method

![](/images/ifttt-social-choice.png)

<br><br>
#### 8) Configure the Post Text

> Ingrediants are Variables you can use to expand your social media posts.

![](/images/ifttt-twitter.png)


<br><br>
#### 9) And simply hit finish.

<br>Simply repeat this process as many times as necessary for each of your social media.
