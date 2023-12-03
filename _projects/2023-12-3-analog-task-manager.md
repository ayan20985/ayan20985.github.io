---
title: "Analog Gauge-Based Task Manager"
layout: page
image:
  thumbnail: /assets/projects/analog.png
---
Let's make a Analog task manager inspired that allows us to display the CPU core loads, CPU core temperatures, CPU power consumption, GPU load, GPU temperature, GPU power consumption, and memory usage.

<style>
    .pdf-container {
    width: 100%;
    height: 100vh;
    border-radius: 20px; /* Adjust the value for the desired roundness */
    overflow: hidden; /* This hides any overflow outside the rounded container */
    position: relative;
    }

    .pdf-object {
    width: 100%;
    height: 100%;
    }

    .pdf-fallback {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #283741;
    border-radius: 20px;
    }

    .content-container-blue {
    border-radius: 10px; /* Add rounded corners to the container */
    padding: 20px; /* Add padding to the container */
    margin-bottom: 20px; /* Add bottom margin to create space between container and text below */
    background-color: #283741; /* Add a background color */
    }

    .content-container {
    border-radius: 10px; /* Add rounded corners to the container */
    padding: 20px; /* Add padding to the container */
    margin-bottom: 20px; /* Add bottom margin to create space between container and text below */
    background-size: cover;
    background-repeat: no-repeat;
    background-attachment: fixed; /* Optional, for a fixed background */
    }

    .dropdown-content {
        display: none;
        overflow: hidden;
    }
    
    /* Adjusted styles for dropdown-header */
    .dropdown-header {
        display: flex;
        align-items: center;
        cursor: pointer;
        padding-left: 10px;
    }

    .dropdown-header:hover {
        color: #D37070;
    }

    .dropdown-icon {
        font-size: 56px;
        transition: transform 0.3s;
        margin-right: 25px;
    }

    .rotate-icon {
        transform: rotate(-180deg);
    }

    .dropdown-content {
        display: none;
        overflow: hidden;
        margin-top: 10px;
    }

    .content-container a {
    color: #D37070; /* Change the color of hyperlinks */
    text-decoration: underline; /* Add underline to hyperlinks */
    }
</style>

<div class="content-container" data-bg-image="/assets/images/chevron2.png">
    This project is available as a Github Repository <a href="https://github.com/420Ayan420/analog-task-manager">here</a>.
</div>

<div class="content-container" data-bg-image="/assets/images/chevron2.png">
    Suggestions? Want to discuss a certain aspect of my work? Please contact me at ayanali20985@gmail.com, use the direct email link in the bottom of the menu on the left, or create a Github pull request.
</div>

This project is in inspired by [this](https://www.youtube.com/watch?v=4J-DTbZlJ5I).

<script>
    // Select all dropdown-header elements
    var dropdownHeaders = document.querySelectorAll(".dropdown-header");

    // Add click event listener to each dropdown-header
    dropdownHeaders.forEach(function(header) {
        header.addEventListener("click", function() {
            // Find the next sibling element which is the dropdown content
            var content = this.nextElementSibling;
            var icon = this.querySelector(".dropdown-icon");

            // Toggle display and icon rotation
            if (content.style.display === "block") {
                content.style.display = "none";
                icon.classList.remove("rotate-icon");
            } else {
                content.style.display = "block";
                icon.classList.add("rotate-icon");
            }
        });
    });

    // Get all elements with the class "content-container"
    const contentContainers = document.querySelectorAll(".content-container");

    // Loop through the elements and set their background images
    contentContainers.forEach(container => {
        const bgImage = container.getAttribute("data-bg-image");
        container.style.backgroundImage = `url(${bgImage})`;
    });
</script>


