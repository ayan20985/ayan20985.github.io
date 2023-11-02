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

  .content-container-blue {
    border-radius: 10px; /* Add rounded corners to the container */
    padding: 20px; /* Add padding to the container */
    margin-bottom: 20px; /* Add bottom margin to create space between container and text below */
    background-color: #283741; /* Add a background color */
  }
  
  .content-container-breathing {
    border-radius: 10px; /* Add rounded corners to the container */
    padding: 20px; /* Add padding to the container */
    margin-bottom: 20px; /* Add bottom margin to create space between container and text below */
    background-size: cover;
    background-repeat: no-repeat;
    background-attachment: fixed; /* Optional, for a fixed background */
    animation: breathing 3s infinite; /* Apply the breathing animation */
  }

  @keyframes breathing {
    0% {
      background-color: #51454C; /* Start with red */
    }
    50% {
      background-color: #5D676E; /* Transition to yellow at 50% */
    }
    100% {
      background-color: #51454C; /* Return to red at 100% */
    }
  }
  
  .content-container a {
    color: #D37070; /* Change the color of hyperlinks */
    text-decoration: underline; /* Add underline to hyperlinks */
  }

  .content-container-scrolling {
    border-radius: 10px;
    padding: 20px;
    margin-bottom: 20px;
    background-color: #51454C;
    overflow: hidden; /* Hide the overflow content */
    white-space: nowrap; /* Prevent text from wrapping */
    width: 100%; /* Set the width to 100% to span the body */
    font-size: 17px;
  }

  .scroll-text {
    animation: scroll 22.5s linear infinite; /* Adjust the animation duration as needed */
    animation-delay: -50s; /* Reduce the delay to 3 seconds */
    display: inline-block;
    font-family: 'Fira Code', sans-serif;
  }

  @keyframes scroll {
    0% {
      transform: translateX(102.5%);
    }
    100% {
      transform: translateX(-102.5%); /* Adjust the distance for a smoother scroll */
    }
  }

  .content-container-scrolling:hover .scroll-text {
    animation-play-state: paused;
  }
</style>

<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Fira+Code&display=swap">

<!-- <div class="content-container" data-bg-image="assets/images/chevron2.png">
  This website is still under construction, while most of the structure and programming is complete content still remains.
</div> -->

<div class="content-container-scrolling scroll-container">
  <div class="scroll-text">
    Latest updates: 23rd Oct, Research section has a new-old project. 23rd Oct, New blog posts coming soon™. 18th Oct, Updated additional information section.
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

<div class="content-container" data-bg-image="assets/images/chevron2.png">
  Have you been assigned 3D modeling homework? Please click <a href="/3d-exercises/">here</a> to be directed to exercises, the exercise number is mentioned in the bottom right corner of each technical drawing.
</div>

<div class="content-container" data-bg-image="assets/images/chevron2.png">
  Notes for the 19th of October available <a href="/19102023/">here</a>.
</div>

<script>
  // Get all elements with the class "content-container"
  const contentContainers = document.querySelectorAll(".content-container");

  // Loop through the elements and set their background images
  contentContainers.forEach(container => {
    const bgImage = container.getAttribute("data-bg-image");
    container.style.backgroundImage = `url(${bgImage})`;
  });
</script>