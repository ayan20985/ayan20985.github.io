---
layout: page
paginate: true
alt_title: "Ayan's Compendium of Assorted Ramblings"
sub_title: "Ripping pages, welding joints, experimenting empirically, burning electronics, and tuning PIDs."
---

<style>
  .content-container {
    border-radius: 10px; /* Add rounded corners to the container */
    padding: 20px; /* Add padding to the container */
    margin-bottom: 20px; /* Add bottom margin to create space between container and text below */
    background-size: cover;
    background-repeat: no-repeat;
    background-attachment: fixed; /* Optional, for a fixed background */
  }
  
  .content-container-breathing {
    border-radius: 10px; /* Add rounded corners to the container */
    padding: 20px; /* Add padding to the container */
    margin-bottom: 20px; /* Add bottom margin to create space between container and text below */
    background-size: cover;
    background-repeat: no-repeat;
    background-attachment: fixed; /* Optional, for a fixed background */
    animation: breathing 2s infinite; /* Apply the breathing animation */
  }

  @keyframes breathing {
    0% {
      background-color: #5D676E; /* Start with red */
    }
    50% {
      background-color: #51454C; /* Transition to yellow at 50% */
    }
    100% {
      background-color: #5D676E; /* Return to red at 100% */
    }
  }
  
  .content-container a {
    color: #D37070; /* Change the color of hyperlinks */
    text-decoration: underline; /* Add underline to hyperlinks */
  }

  .content-container b {
    color: #D37070; /* Change the color of hyperlinks */
    text-decoration: underline; /* Add underline to hyperlinks */
  }
</style>
<div class="content-container" data-bg-image="assets/images/chevron2.png">
  This website is still under construction, while most of the structure and programming is complete content still remains.
</div>

<div class="content-container-breathing">
  Admissions staff? Please click <a href="/admissions/">here</a> to be directed to additional documents that you may find useful.
</div>

<div class="content-container" data-bg-image="assets/images/chevron2.png">
  Have you been assigned 3D modeling homework? Please click <b href="/3d-exercises/">here</b> to be directed to exercises, the exercise number is mentioned in the bottom right corner of each technical drawing.
</div>

<div class="content-container" data-bg-image="assets/images/chevron2.png">
  Notes for the 19th of October available <a href="/19102023/">here</a>.
</div>

- Learn more about me in my <a href="/about/">about</a> section
- Discussions of niche topics and ramblings of things I've learned in the <a href="/blog/">blog</a>
- Various <a href="/projects/">projects</a> of projects that are complete and in-progress
- A 3D-Modeling course that has been deployed to 11 schools or ~3100 eligible students, and my EPQ in <a href="/research/">research</a>
- Various 3D-art that I created in the <a href="/artwork/">artwork</a> section
- Resources, site documentation, and my reading list are all in the <a href="/miscellaneous/">miscellaneous</a> section

<script>
  // Get all elements with the class "content-container"
  const contentContainers = document.querySelectorAll(".content-container");

  // Loop through the elements and set their background images
  contentContainers.forEach(container => {
    const bgImage = container.getAttribute("data-bg-image");
    container.style.backgroundImage = `url(${bgImage})`;
  });
</script>