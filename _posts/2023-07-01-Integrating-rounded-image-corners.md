---
title: "Integrating Rounded Image Corners"
categories:
  - Site Documentation
tags:
last_modified_at: 2023-06-28T14:25:52-05:00
comments: false
---
Adding rounded corners would make the website a lot more pleasant to look at, allow for a more seamless design especially on the art work page, and add just a little bit more spice.

{% raw %}
<br>
# Overview 
First let us start by listing the locations I need to implement rounded image corners; retrospectively speaking, in order from easiest to hardest to implement:
1.	Rounded corners on images that are inserted onto pages called posts such as this one.
2.	Rounded corners on images that are in image carousels.
3.	Rounded corners on images that are displayed as thumbnails for the different entries on pages such as artwork or projects.

<br>
# The actual code required
To add rounded image corners some simple css   must be used:
```css
border-radius: 10px;
```
```html
<style>
.rounded-image {
    border-radius: 10px; /* Adjust the value to control the roundness of corners */
}
</style>
```
Now, the challenge lies in us figuring out how to insert this code into the already existing infrastructure th  at has been already created in the Jekyll theme.

<br>
# (1) Rounded corners on images that are inserted on pages.
This is the most simple implementation of rounded image corners, when an image is inserted into a markdown file we use the following code:
```md
![alternative text]({{ site.url }}{{ site.baseurl }}\assets\images\sticky notes.jpg){: .align-center}
```

The .align-center class can thus be the location where we insert our css to create the rounded corners. To do this we can just simply use vscode's search menu and search for "align-center". This leads us to the following file in: 
```
\_sass\theme name\utilities\_align.scss.
```

From there we can just simply insert our code by doing the following:
```scss
.align-baseline { vertical-align: baseline !important; } //Browser default
.align-top { vertical-align: top !important; }
.align-middle { vertical-align: middle !important; }
.align-bottom { vertical-align: bottom !important; }
.align-text-bottom { vertical-align: text-bottom !important; }
.align-text-top { vertical-align: text-top !important; }

.align-center,
div.align-center,
a img.align-center {
  display: block;
  margin-right: auto;
  margin-left: auto;
  border-radius: 15px; //Adding rounded corners here for images.
}

figure.align-center {
  img {
    display: block;
    margin-right: auto;
    margin-left: auto;
    border-radius: 15px; //Adding rounded corners here for images.
  }

  figcaption {
    text-align: center;
  }
}

.align-right,
a img.align-right {
  margin-bottom: 1rem;
  margin-left: 1rem;
  float: right;
  border-radius: 15px; //Adding rounded corners here for images.
}

.align-left,
a img.align-left {
  margin-right: 1rem;
  margin-bottom: 1rem;
  float: left;
  border-radius: 15px; //Adding rounded corners here for images.
}

.is--pushed {
  transform: translateX(1 * $sidebar-width);
  transform-origin: right;

  @include breakpoint($large) {
    transform: translateX(1.5 * $sidebar-width);
  }
}
```

This sort of implementation also ensures that whatever layout of image we use on a page all the image's corners will be rounded.

<br>
# (2) Rounding the corners of images in image carousels.
During the implementation of image carousels noted [here]({{ site.url }}{{ site.baseurl }}/site%20documentation/2023/06/30/Integrating-Image-Carousel.html) we created a file called carousel.html to handle the rendering of the image carousel, it is located at:
```
\_includes\carousel.html
```
From there we can simply insert our code into the .carousel_slide class:
```scss
.carousel__slide {
  height: 100%;
  position: absolute;
  opacity: 0;
  overflow: hidden;
  border-radius: 15px; /* Adding rounded corners to the images in the image carousel. */
}
```
Here we have rounded the corners of the image carousel. If you would like to know how the overall image carousel code works please refer to the post linked in this section.

<br>
# (3) Adding rounded corners to thumbnails in collection layout.
Whenever a page is created, there is a front matter that defines the attributes of the page, for example:
```markdown
---
title: "↯ projects"
layout: collection
permalink: /projects/
collection: projects
entries_layout: grid
---
```
The page uses the layout collection which is located at:
```
\_layouts\collection.html.
```
When we look inside collection.html:
```html
---
layout: page
---
{{ content }}

<div class="entries-{{ page.entries_layout | default: 'list' }}">
  {% include documents-collection.html collection=page.collection sort_by=page.sort_by sort_order=page.sort_order %}
</div>
```
We can see that we are referencing a documents-collection.html element which is located at:
```
\_includes\document-collection.html\
```
When we look inside document-collection.html:
```html
{% assign entries = site[include.collection] %}

{% if include.sort_by == 'title' %}
  {% if include.sort_order == 'reverse' %}
    {% assign entries = entries | sort: 'title' | reverse %}
  {% else %}
    {% assign entries = entries | sort: 'title' %}
  {% endif %}
{% elsif include.sort_by == 'date' %}
  {% if include.sort_order == 'reverse' %}
    {% assign entries = entries | sort: 'date' | reverse %}
  {% else %}
    {% assign entries = entries | sort: 'date' %}
  {% endif %}
{% endif %}

{%- for post in entries -%}
  {% include entry.html %}
{%- endfor -%}
```
We can see that we are referencing a entry.html element which is located at:
```
\_includes\entry.html\
```
And finally when we look inside entry.html we are able to add our css for rounded corners by doing the following changes.
```html
{% if post.id %}
  {% assign title = post.title | markdownify | strip_html %}
{% else %}
  {% assign title = post.title %}
{% endif %}

<article class="entry">
  <header class="entry-header">
    <h3 class="entry-title">
      <a href="{{ post.url | relative_url }}" rel="bookmark">{{ title }}</a>
    </h3>
    {% if post.image.thumbnail %}
      {% assign entry_image = post.image.thumbnail | relative_url | escape %}
      <div class="entry-thumbnail rounded-thumbnail">
        <img class="entry-image u-photo" src="{{ entry_image }}" alt="">
      </div>
    {% endif %}
  </header>
  <footer class="entry-meta">
    <ul>
      {% if post.date %}
        <li><span class="icon">{% include icon-calendar.svg %}</span><time class="entry-time" datetime="{{ post.date | date_to_xmlschema }}">{{ post.date | date: "%B %-d, %Y" }}</time></li>
      {% endif %}
      {% if post.read_time %}
        <li><span class="icon">{% include icon-stopwatch.svg %}</span>{% capture read_time %}{% include read-time.html %}{% endcapture %}{{ read_time | strip }}</li>
      {% endif %}
    </ul>
  </footer>
  <div class="entry-excerpt">
    {% if post.excerpt %}
      {{ post.excerpt | markdownify }}
      <p><a href="{{ post.url | relative_url }}" class="more-link">{{ site.data.theme.t.read_more | default: 'Read More' }} <span class="icon icon--arrow-right">{% include icon-arrow-right.svg %}</span></a></p>
    {% endif %}
  </div>
</article>

<style>
  .rounded-thumbnail img {
    border-radius: 10px; /*Adding rounded corners to the thumbnail images.*/
  }
</style>
```
Specifically, I have added:
```html
<style>
  .rounded-thumbnail img {
    border-radius: 10px; /*Adding rounded corners to the thumbnail images.*/
  }
</style>
```
```html
<div class="entry-thumbnail rounded-thumbnail">
  <img class="entry-image u-photo" src="{{ entry_image }}" alt="">
</div>
```
<br>
# Conclusion
While rounded corners on images may seem to be a simple task some of the techniques I have mentioned here may prove to be useful for integrating further features to the existing Jekyll theme if I so wish to do so.
{% endraw %}