---
layout: index
paginate: true
alt_title: "Ayan's Compendium of Assorted Ramblings"
sub_title: "Ripping pages, welding joints, experimenting empirically, burning electronics, and tuning PIDs."
---

<!-- <div class="content-container" data-bg-image="assets/images/chevron2.png">
  This website is still under construction, while most of the structure and programming is complete content still remains.
</div> -->

<div class="content-container-scrolling scroll-container">
  <div class="scroll-text">
    Latest updates ||| 1st January, Happy New Year and NEW PROJECT! Electric Car see ↯ Projects for more details. ||| 3rd December, NEW PROJECT! Analog Task Manager, see ↯ Projects for more details. ||| 10th November, more content added in password-protected section, use password to access! ||| 1st November, the password-protected section has been updated with 128-bit encryption. ||| 23rd Oct, Research section has a new-old project. ||| 23rd Oct, New blog posts coming soon™. ||| 18th Oct, Updated additional information section. |||
  </div>
</div>

<div class="content-container-breathing">
  Admissions staff? Please click <a href="/admissions/">here</a> to be directed to additional documents that you may find useful.
</div>

<div class="content-container-blue">
  <ul>
    <li>Learn more about me in my <a href="/about/">about</a> section</li>
    <li>Discussions of niche topics and ramblings of things I&#39;ve learned in the <a href="/blog/">blog</a></li>
    <li>Various <a href="/projects/">projects</a> of projects that are complete and in-progress</li>
    <li>A 3D-Modeling course that has been deployed to 11 schools or ~2500 eligible students, and my EPQ in <a href="/research/">research</a></li>
    <li>Various 3D-art that I created in the <a href="/artwork/">artwork</a> section</li>
    <li>Resources, site documentation, and my reading list available at <a href="/miscellaneous/">miscellaneous</a></li>
  </ul>
</div> 

<!--
<div class="container">
  <div class="text">Learn more about me in my about section.</div>
  <div class="image-container" style="background-image: url({{ site.url }}{{ site.baseurl }}/assets/thumbnails/u.png);">
  </div>
</div>

<div class="container">
  <div class="text">Discussions of niche topics and ramblings of things I've learned in the blog.</div>
  <div class="image-container" style="background-image: url({{ site.url }}{{ site.baseurl }}/assets/thumbnails/uu.png);">
  </div>
</div>

<div class="container">
  <div class="text">Various projects of projects that are complete and in-progress.</div>
  <div class="image-container" style="background-image: url({{ site.url }}{{ site.baseurl }}/assets/thumbnails/uuu.png);">
  </div>
</div>

<div class="container">
  <div class="text">My research into various topics.</div>
  <div class="image-container" style="background-image: url({{ site.url }}{{ site.baseurl }}/assets/thumbnails/uv.png);">
  </div>
</div>

<div class="container">
  <div class="text">Various 3D-art that I created in the artwork section.</div>
  <div class="image-container" style="background-image: url({{ site.url }}{{ site.baseurl }}/assets/thumbnails/v.png);">
  </div>
</div>

<div class="container">
  <div class="text">YResources, site documentation, and my reading list available at miscellaneous</div>
  <div class="image-container" style="background-image: url({{ site.url }}{{ site.baseurl }}/assets/thumbnails/ov.png);">
  </div>
</div>
-->

<div class="content-container" data-bg-image="assets/images/chevron2.png">
  Have you been assigned 3D modeling homework? Please click <a href="/3d-exercises/">here</a> to be directed to exercises, the exercise number is mentioned in the bottom right corner of each technical drawing.
</div>

<div class="content-container" data-bg-image="assets/images/chevron2.png">
  Notes for the 19th of October available <a href="/19102023/">here</a>.
</div>

<style>
  .container {
    display: flex;
    align-items: center;
    margin: 20px auto;
    padding: 20px;
    background-color: #283741;
    border-radius: 15px;
    position: relative;
    overflow: hidden; /* Ensures nested elements don't overflow the rounded corners */
    width: 100%; /* Adjust width as needed */
  }
  .image-container {
    width: 100px; /* Adjust based on your preference */
    height: 100%; /* Makes the height match the parent container */
    background-color: #283741; /* Different color for the image container */
    background-size: cover; /* Ensure the image covers the full container */
    background-position: center; /* Center the background image */
    position: absolute;
    right: 5;
    top: 0;
    border-radius: 0 15px 15px 0; /* Only round the right side corners */
  }
  .text {
    flex: 1;
    z-index: 1; /* Ensures text appears above the image container for visibility */
    text-align: right;
    vertical-align: middle;
    padding-right: 10px; /* Adjust the padding to not overlap with the image container */
  }

/* Shiny swipe effect */
  .container::after {
    content: '';
    position: absolute;
    top: 0;
    left: -100%; /* Start from the left, outside of the view */
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, rgba(255, 255, 255, 0) 0%, rgba(255, 255, 255, 0.8) 50%, rgba(255, 255, 255, 0) 100%);
    transition: left 2s ease-out;
    pointer-events: none; /* Prevent the effect layer from interfering with container interactions */
  }
  
  .container:hover::after {
    left: 100%; /* Move to the right, creating the swipe effect */
  }
</style>