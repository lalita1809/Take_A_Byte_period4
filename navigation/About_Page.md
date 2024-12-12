---
layout: post
title: About TAB!
search_exclude: true
hide: true
---
<h1>Welcome to Take A Byte </h1>
##

<h3> <span class="bike-emoji">🚴‍♂️</span> I really love to bike with my uncle and aunt on different trails, whenever they visit California or whenever I go to Colorado to see them. </h3>

<h3> 🏊‍♀️ I love to go swimming at the beach, with my friends and family. I also used to do competitive swim! </h3>

<h3> &#x1F9F5; I love stitching and I have started stitching clothes, and bags, and art pieces since middle school! </h3>


<h3> These are my favorite TV show** </h3>



<img src = "{{site.baseurl}}/images/notebooks/image copy.png" alt = "the office">
<img src= "{{site.baseurl}}/images/notebooks/image.png" alt = "friends">
<img src = "{{site.baseurl}}/images/notebooks/image copy 4.png" alt = "modern family">
<img src = "{{site.baseurl}}/images/notebooks/image copy 3.png" alt = "parks and rec">


### **Places I have lived!**

<style>
    /* Style looks pretty compact, trace grid-container and grid-item in the code */
    .grid-container {
        display: grid;
        grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); /* Dynamic columns */
        gap: 10px;
    }
    .grid-item {
        text-align: center;
    }
    .grid-item img {
        width: 100%;
        height: 100px; /* Fixed height for uniformity */
        object-fit: contain; /* Ensure the image fits within the fixed height */
    }
    .grid-item p {
        margin: 5px 0; /* Add some margin for spacing */
    }
</style>

<!-- This grid_container class is for the CSS styling, the id is for JavaScript connection -->
<div class="grid-container" id="grid_container">
    <!-- content will be added here by JavaScript -->
</div>

<script>
    // 1. Make a connection to the HTML container defined in the HTML div
    var container = document.getElementById("grid_container"); // This container connects to the HTML div

    // 2. Define a JavaScript object for our http source and our data rows for the Living in the World grid
    var http_source = "https://upload.wikimedia.org/wikipedia/commons/";
    var living_in_the_world = [
        {"flag": "0/01/Flag_of_California.svg", "greeting": "HEYYYYY", "description": "I loved here when I was 9 years old and have lived here ever since"},
        {"flag": "a/ac/Flag_of_Indiana.svg", "greeting":"Howdy" , "description": "I was born in Indiana and I lived in Indiana for 2 years"},
        {"flag": "4/41/Flag_of_India.svg", "greeting": "Namaste", "description": "I try visiting India every 2-3 years to see my family there"},
        {"flag": "9/9d/Flag_of_Arizona.svg", "greeting":"Hello from the heat", "description": "I lived there for 6.5 years, and I wasn't the biggest fan of the heat"},
    ]; 
    
    // 3a. Consider how to update style count for size of container
    // The grid-template-columns has been defined as dynamic with auto-fill and minmax

    // 3b. Build grid items inside of our container for each row of data
    for (const location of living_in_the_world) {
        // Create a "div" with "class grid-item" for each row
        var gridItem = document.createElement("div");
        gridItem.className = "grid-item";  // This class name connects the gridItem to the CSS style elements
        // Add "img" HTML tag for the flag
        var img = document.createElement("img");
        img.src = http_source + location.flag; // concatenate the source and flag
        img.alt = location.flag + " Flag"; // add alt text for accessibility

        // Add "p" HTML tag for the description
        var description = document.createElement("p");
        description.textContent = location.description; // extract the description

        // Add "p" HTML tag for the greeting
        var greeting = document.createElement("p");
        greeting.textContent = location.greeting;  // extract the greeting

        // Append img and p HTML tags to the grid item DIV
        gridItem.appendChild(img);
        gridItem.appendChild(description);
        gridItem.appendChild(greeting);

        // Append the grid item DIV to the container DIV
        container.appendChild(gridItem);
    }
</script>




### **These are photos of my friends and I**

<div class="image-gallery">
<img src = "{{site.baseurl}}/images/notebooks/image copy 11.png" alt = "at the beach!" width = "340" height = "200">
<img src = "{{site.baseurl}}/images/notebooks/image copy 12.png" alt = "with my friends!" width = "340" height = "200">
<img src = "{{site.baseurl}}/images/notebooks/image copy 13.png" alt = "with my friends!" width = "340" height = "200">
<img src = "{{site.baseurl}}/images/notebooks/image copy 14.png" alt = "with my friends!" width = "340" height = "200">
</div>

<body style ="background-color:pink;">



<script src="https://utteranc.es/client.js"
        repo="lalita1809/lalita_2025"
        issue-term="title"
        label="utterances"
        theme="github-light"
        crossorigin="anonymous"
        async>
</script>

