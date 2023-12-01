---
title: "Syllabus for 3D Modelling in an Engineering Context"
layout: page
---
12 Chapters, 18 weeks of study, 11 schools, ~2500 eligible students, and Fusion 360. Designed to teach students from Grades 9 to 12 industry standard CAD practices that emphasize design thinking and modelling intuition. Skills learned can be transferred to programs outside of fusion 360. <!-- Plans to deploy to ~53 schools or ~15000 eligible students. --> Open-source and free forever.

A brief history of solar flight with analysis of existing data; an explanation on the concepts leading to solar flight; narrowing existing technology to a feasible flight model; modeling through fluid simulation and power-metrics; and producing a possible prototype. Plans to extend paper and publish instead of just submitting as an EPQ.

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
</style>

<div class="content-container" data-bg-image="/assets/images/chevron2.png">
    Currently being updated and reworked for the new academic year as according to feedback given in the initial feedback stage. Updated version to be posted in the month of February. Below are specimen documents.
</div>

<div class="content-container" data-bg-image="/assets/images/chevron2.png">
    Suggestions? Want to discuss a certain aspect of my work? Want to collaborate? Please contact me at ayanali20985@gmail.com, or use the direct email link in the bottom of the menu on the left.
</div>

<div class="content-container-blue">
    <div class="dropdown-header">
        <span class="dropdown-icon">&#9660;</span> <!-- Down-arrow icon -->
        Final submission for NEA is as follows, scored full marks and Pearson-Edexcel OPLA highest in the middle east for this project.
    </div>
    <div class="dropdown-header" class="dropdown-content">
        <div class="pdf-container">
            <object class="pdf-object" data="/assets/pdf/UAVs v0.6.pdf" type="application/pdf">
                <div class="pdf-fallback">
                    PDF cannot be displayed. Please use a browser that supports native PDF representation such as Firefox, Microsoft Edge, or Chrome.
                </div>
            </object>
        </div>
    </div>
</div>

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

*All documents uploaded here are under the [CC BY-NC-SA 4.0 DEED License](https://creativecommons.org/licenses/by-nc-sa/4.0/).*