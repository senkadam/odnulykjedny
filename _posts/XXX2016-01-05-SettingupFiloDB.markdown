---
layout: post
title:  "Setting up the FiloDB"
date:   2016-01-05 08:43:59
author: Ben Šenk
categories: FiloDB
tags:	FiloDB NoSQL BigData tutorial
cover:  "/assets/instacode.png"
---

In this tutorial I will describe the required steps for setting up a FiloDB on Ubuntu Linux 14.04 64-bit.


## The main pre-requisities
First, you have to install **Java8** and **SBT**.

### Java8

We will install Oracle Java. You can skip this section if you have Java already installed. These commands will add a custom apt repository and install Java8.

<pre><code class="shell">sudo apt-add-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer</code></pre>


###Scala and SBT

These commands will install Scala in version 2.11.5 and SBT in version in 0.13.9.

<pre><code class="shell">sudo apt-get remove scala-library scala
sudo wget www.scala-lang.org/files/archive/scala-2.11.5.deb
sudo dpkg -i scala-2.11.5.deb
sudo apt-get update
sudo apt-get install scala
wget https://bintray.com/artifact/download/sbt/debian/sbt-0.13.9.deb
sudo dpkg -i sbt-0.13.9.deb
sudo apt-get update
sudo apt-get install sbt</code></pre>

You can verify all installed tool by following commands. For Java verification use:
<pre><code class="shell">java -version</code></pre>

It should print the installed version of Java, which should be *1.8*

<pre><code class="shell">java version "1.8.0_66"
Java(TM) SE Runtime Environment (build 1.8.0_66-b17)
Java HotSpot(TM) 64-Bit Server VM (build 25.66-b17, mixed mode)</code></pre>

For scala verification use:
<pre><code class="shell">scala -version</code></pre>

It should print the installed version of scala, which should be *2.11.5*

<pre><code class="shell">Scala code runner version 2.11.5 -- Copyright 2002-2013, LAMP/EPFL</code></pre>

For sbt verification use:
<pre><code class="shell">sbt</code></pre>

This will run sbt, you can quit it by pressing `Ctrl+C`

##Cassandra
Now we will install and locally run Cassandra cluster. We use ccm (Cassandra CLuster Manager) - see [https://github.com/pcmanus/ccm]

###Installing pre-requisities and ccm
We have to install python and a couple of python tools, before running ccm
<pre><code class="shell">sudo apt-get install python
sudo apt-get install python-dev
sudo apt-get install python-pip
sudo pip install six
sudo pip instal pyYaml
sudo pip install psutil</code></pre>

Let us install ccm now.

<pre><code class="shell">sudo pip install ccm</code></pre>

Whe the instalation is finished, we can start 4 node local Cassandra cluster. The command is following

<pre><code class="shell">ccm create test -v 2.2.4 -n 4 -s</code></pre>

To check if the cluster is running, use this command:
<pre><code class="shell">ccm node1 ring</code></pre>


The output should look something like:
<pre><code class="shell">==========
Address    Rack        Status State   Load            Owns                Token                                       
                                                                          4611686018427387904                         
127.0.0.1  rack1       Up     Normal  99.94 KB        ?                   -9223372036854775808                        
127.0.0.2  rack1       Up     Normal  99.97 KB        ?                   -4611686018427387904                        
127.0.0.3  rack1       Up     Normal  113.14 KB       ?                   0                                           
127.0.0.4  rack1       Up     Normal  124.58 KB       ?                   4611686018427387904                         


  Note: Non-system keyspaces don't have the same replication settings, effective ownership information is meaningless</code></pre>

Cassandra cluster is now available at http://localhost:9042/

##Spark

Spark can be downloaded, unpacked and build by following instructions:

<pre><code class="shell">wget d3kbcqa49mib13.cloudfront.net/spark-1.5.2.tgz
tar xvf spark-1.5.2.tgz
cd spark-1.5.2/
build/sbt assembly</code></pre>

##FiloDB
You are now ready to install FIiloDB. Details are on [https://github.com/tuplejump/FiloDB]. This tutorial will guide you trough really quickstart.


### Tags and Categories

If you list one or more categories or tags in the front matter of your post, they will be included with the post on the page as links. Clicking the link will bring you to an auto-generated archive page for the category or tag, created using the [jekyll-archive][jekyll-archive] gem.

### Cover Images

To add a cover image to your post, set the "cover" property in the front matter with the relative URL of the image (i.e. <code>cover: "/assets/cover_image.jpg"</code>).

### Code Snippets

You can use [highlight.js][highlight] to add syntax highlig code snippets:

<pre><code class="hljs javascript">function demo(string, times) {
  for (var i = 0; i < times; i++) {
    console.log(string);
  }
}
demo("hello, world!", 10);</code></pre>

### Images

Lightbox has been enabled for images. To create the link that'll launch the lightbox, add <code>data-lightbox</code> and <code>data-title</code> attributes to an <code>&lt;a&gt;</code> tag around your <code>&lt;img&gt;</code> tag. The result is:

<a href="//bencentra.com/assets/images/falcon9_large.jpg" data-lightbox="falcon9-large" data-title="Check out the Falcon 9 from SpaceX">
  <img src="//bencentra.com/assets/images/falcon9_small.jpg" title="Check out the Falcon 9 from SpaceX">
</a>

For more information, check out the [Lightbox][lightbox] website.

Check out the [Jekyll docs][jekyll] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll’s dedicated Help repository][jekyll-help].

[jekyll]:      http://jekyllrb.com
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help
[highlight]:   https://highlightjs.org/
[lightbox]:    http://lokeshdhakar.com/projects/lightbox2/
[jekyll-archive]: https://github.com/jekyll/jekyll-archives
