---
title: "Design for Modular Water-Catcher for Arid Mountainscapes"
layout: page
---
Mountain regions placed a certain altitudes can become arid due to the scarcity of water. This is due to the mountains being too high for a viable well to be dug to tap into the ground water table; the mountains having certain meterological conditions that prevent precipitation; and are mild in temperature and thus there is no rainwater and or snow. Through biomimicry of "cloud forests" we are able to provide water for such regions and support communities who would have to otherwise traverse 5-6 hours for water.

<style>
    .pdf-container {
    width: 100%; /* Set the width to fill the container */
    height: 100vh; /* Adjust the height as needed */
    border-radius: 0; /* Remove the border-radius if you want the PDF to span the entire box */
    overflow: hidden; /* Hide any overflow */
    position: relative;
    }

    .pdf-object {
    width: 100%; /* Set the width to fill the container */
    height: 100%; /* Set the height to fill the container */
    border: none; /* Remove any border */
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

    }

    .content-container-normal {
    border-radius: 10px; /* Add rounded corners to the container */
    padding: 20px; /* Add padding to the container */
    margin-bottom: 20px; /* Add bottom margin to create space between container and text below */
    background-color: #283741; /* Add a background color */
    }

    .dropbtn {
    border-radius: 10px; /* Add rounded corners to the container */
    padding: 20px; /* Add padding to the container */
    margin-bottom: 20px; /* Add bottom margin to create space between container and text below */
    background-color: #283741; /* Add a background color */
    }

    .dropdown-content {
    display: none;
    padding: 5px;
    margin-top: 5px;
    border-radius: 10px;
    background-color: #f9f9f9;
    box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
    }

    .show {
    display: block;
    }
</style>

<div class="content-container-normal">
  Suggestions? Want to discuss a certain aspect of my work? Want to collaborate? Please contact me at ayanali20985@gmail.com, or use the direct email link in the bottom of the menu on the left.
</div>

Final submission as for NEA is as follows, scored full marks and Pearson-Edexcel OPLA highest in the middle east for this project:
<div class="content-container-blue">
  <button onclick="toggleDropdown('dropdown1')" class="dropbtn">Final Submission NEA</button>
  <div id="dropdown1" class="dropdown-content">
    <!-- Your existing PDF display code goes here -->
    <div class="pdf-container">
      <object class="pdf-object" data="/assets/pdf/NEA.pdf" type="application/pdf">
        <div class="pdf-fallback">
          PDF cannot be displayed. Please use a browser that supports native PDF representation such as Firefox, Microsoft Edge, or Firefox.
        </div>
      </object>
    </div>
  </div>
</div>

Technical drawings for the final design as follows:
Graphic design for the assembly booklet as follows:
Some posters and miscellaneous material surrounding the project as follows:

<script>
    function toggleDropdown(dropdownId) {
    var dropdown = document.getElementById(dropdownId);
    dropdown.classList.toggle("show");
    }

    // Close the dropdown if the user clicks outside of it
    window.onclick = function(event) {
    if (!event.target.matches('.dropbtn')) {
        var dropdowns = document.getElementsByClassName("dropdown-content");
        for (var i = 0; i < dropdowns.length; i++) {
        var openDropdown = dropdowns[i];
        if (openDropdown.classList.contains('show')) {
            openDropdown.classList.remove('show');
        }
        }
    }
    };
</script>
