---
layout: post
title: Take A Byte
search_exclude: true
hide: true
---

<!--menu: nav/home.html-->

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Website Search</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
        }
        .search-container {
            position: absolute;
            top: 20px;
            right: 20px;
            width: 300px;
            transition: all 0.3s ease;
        }
        .search-container input[type="text"] {
            width: calc(100% - 20px);
            padding: 15px 45px 15px 20px;
            font-size: 16px;
            border: 2px solid #e0e0e0;
            border-radius: 25px;
            background: rgba(255, 255, 255, 0.9);
            backdrop-filter: blur(5px);
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            transition: all 0.3s ease;
        }
        .search-container input[type="text"]:focus {
            width: calc(100% + 50px);
            border-color: #4CAF50;
            box-shadow: 0 6px 20px rgba(76, 175, 80, 0.2);
            outline: none;
        }
        .search-container button {
            position: absolute;
            right: 5px;
            top: 50%;
            transform: translateY(-50%);
            background: none;
            border: none;
            padding: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        .search-container button:hover {
            transform: translateY(-50%) scale(1.1);
        }
        .search-icon {
            width: 20px;
            height: 20px;
            border: 2px solid #4CAF50;
            border-radius: 50%;
            position: relative;
        }
        .search-icon::after {
            content: '';
            position: absolute;
            right: -7px;
            bottom: -7px;
            width: 10px;
            height: 2px;
            background: #4CAF50;
            transform: rotate(45deg);
        }
        .results {
            position: absolute;
            top: 100%;
            left: 0;
            right: 0;
            margin-top: 10px;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 15px;
            box-shadow: 0 8px 25px rgba(0, 0, 0, 0.1);
            max-height: 300px;
            overflow-y: auto;
            opacity: 0;
            transform: translateY(-10px);
            transition: all 0.3s ease;
            z-index: 1000;
        }
        .results.show {
            opacity: 1;
            transform: translateY(0);
        }
        .results a {
            display: block;
            padding: 12px 20px;
            color: #333;
            text-decoration: none;
            border-bottom: 1px solid #eee;
            transition: all 0.2s ease;
        }
        .results a:hover {
            background: rgba(76, 175, 80, 0.1);
            padding-left: 25px;
        }
        .results a:last-child {
            border-bottom: none;
        }
        .aboutButton {
        display: inline-block;
        padding: 10px 20px;
        font-size: 18px;
        color: white;
        background-color: #4CAF50;
        text-decoration: none;
        border-radius: 8px;
        transition: background 0.3s ease, transform 0.2s ease;
        }
        .aboutButton:hover {
        background-color: #45a049;
        transform: scale(1.05);
    </style>
</head>
<body>
    <div class="search-container">
        <input type="text" id="searchInput" placeholder="Search for content...">
        <button onclick="performSearch()">Search</button>
        <div class="results" id="results">
            <!-- Search results will appear here -->
        </div>
    </div>
    
<script>
        // List of all pages and their content
        const pages = [
            { url: '/flocker_frontend_period4/navigation/about', title: 'About', keywords: ['about', 'team', 'company', 'fridge'] },
            { url: '/flocker_frontend_period4/navigation/cuisine/thai', title: 'Thai Cuisine', keywords: ['thai', 'food', 'asian', 'cuisine'] },
            { url: '/flocker_frontend_period4/navigation/cuisine/indian', title: 'Indian Cuisine', keywords: ['indian', 'food', 'curry', 'cuisine'] },
            { url: '/flocker_frontend_period4/navigation/cuisine/italian', title: 'Italian Cuisine', keywords: ['italian', 'pasta', 'pizza', 'cuisine'] },
            { url: '/flocker_frontend_period4/navigation/buttons/posting', title: 'Post Recipe', keywords: ['post', 'recipe', 'share', 'create'] },
            { url: '/flocker_frontend_period4/navigation/feedback', title: 'Feedback', keywords: ['feedback', 'comments', 'suggestions'] },
            { url: '/flocker_frontend_period4/natcountrygen', title: 'NatCountryGen', keywords: ['generator', 'country', 'national'] }
            // Add more pages as needed
        ];

        function performSearch() {
            const query = document.getElementById('searchInput').value.trim().toLowerCase();
            const resultsContainer = document.getElementById('results');
            resultsContainer.innerHTML = '';

            if (!query) {
                resultsContainer.classList.remove('show');
                return;
            }

            const matchingPages = pages.filter(page => 
                page.keywords.some(keyword => keyword.includes(query)) ||
                page.title.toLowerCase().includes(query)
            );

            if (matchingPages.length === 0) {
                resultsContainer.innerHTML = '<div style="padding: 12px 20px; color: #666;">No results found</div>';
            } else {
                matchingPages.forEach(page => {
                    const link = document.createElement('a');
                    link.href = page.url;
                    link.textContent = page.title;
                    resultsContainer.appendChild(link);
                });
            }

            resultsContainer.classList.add('show');
        }

        // Add event listener for real-time search
        document.getElementById('searchInput').addEventListener('input', performSearch);

        // Close results when clicking outside
        document.addEventListener('click', (e) => {
            const resultsContainer = document.getElementById('results');
            const searchContainer = document.querySelector('.search-container');
            if (!searchContainer.contains(e.target)) {
                resultsContainer.classList.remove('show');
            }
        });
    </script>

    <h3></h3>
    <h3>
      <a class="FridgeButton" href="{{site.baseurl}}/about">
        <div class="mini-fridge">
          <div class="mini-handle"></div>
          <div class="mini-display">4°C</div>
          <div class="mini-shelf"></div>
          <div class="mini-shelf"></div>
        </div>
      </a>
    </h3>

    <style>
      .FridgeButton {
        display: inline-block;
        width: 150px;
        height: 225px;
        text-decoration: none;
        position: absolute;
        right: 20px;
        top: 150px;
        transition: all 0.3s ease;
        transform-style: preserve-3d;
        perspective: 1000px;
        z-index: 9999;
        margin: 0;
        padding: 0;
        background: none;
      }

      .mini-fridge {
        width: 100%;
        height: 100%;
        background: linear-gradient(145deg, #e8e8e8, #d4d4d4);
        border-radius: 15px;
        position: relative;
        box-shadow: 
          0 8px 15px rgba(0,0,0,0.2),
          inset 0 0 0 2px rgba(255,255,255,0.1);
        overflow: hidden;
        transition: all 0.3s ease;
        transform-origin: left center;  /* Changed from right to left */
      }

      .FridgeButton:hover .mini-fridge {
        transform: rotateY(15deg);    /* Changed from -15deg to 15deg */
        box-shadow: 
          -20px 8px 15px rgba(0,0,0,0.2),  /* Changed shadow direction */
          inset 0 0 0 2px rgba(255,255,255,0.2);
      }

      /* Adjust inner shadow direction */
      .mini-fridge::before {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background: linear-gradient(
          to left,          /* Changed from right to left */
          rgba(0,0,0,0.2) 0%,
          transparent 20%
        );
        opacity: 0;
        transition: opacity 0.3s ease;
        pointer-events: none;
      }

      .FridgeButton:hover .mini-fridge::before {
        opacity: 1;
      }

      .mini-handle {
        position: absolute;
        right: 12px;      /* Adjusted for larger size */
        top: 50%;
        transform: translateY(-50%);
        width: 10px;      /* Slightly wider handle */
        height: 60%;
        background: linear-gradient(90deg, #888, #999);
        border-radius: 4px;
        box-shadow: 
          inset -1px 0 3px rgba(0,0,0,0.3),
          1px 0 2px rgba(255,255,255,0.5);
      }

      .mini-display {
        position: absolute;
        top: 15px;        /* Adjusted for larger size */
        left: 50%;
        transform: translateX(-50%);
        background: #000;
        color: #00ff00;
        padding: 4px 10px;  /* Slightly larger padding */
        border-radius: 4px;
        font-family: 'Digital', monospace;
        font-size: 14px;    /* Increased font size */
        box-shadow: 
          inset 0 0 3px rgba(0,255,0,0.5),
          0 0 5px rgba(0,0,0,0.2);
      }

      .mini-shelf {
        position: absolute;
        left: 10%;
        width: 80%;
        height: 1px;
        background: rgba(0,0,0,0.1);
        box-shadow: 0 1px 2px rgba(255,255,255,0.5);
      }

      .mini-shelf:nth-child(3) { top: 40%; }
      .mini-shelf:nth-child(4) { top: 70%; }

      .mini-fridge::after {
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        background: 
          repeating-linear-gradient(
            45deg,
            rgba(255,255,255,0.05) 0px,
            rgba(255,255,255,0.05) 1px,
            transparent 1px,
            transparent 3px
          );
        pointer-events: none;
      }
    </style>
</body>
</html>

<h3> <a class="aboutButton" href="{{site.baseurl}}/navigation/about">About page</a></h3>


<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Random Cuisine Spinner</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f4f4f9;
        }
        .wheel-container {
            position: relative;
            width: 300px;
            height: 300px;
            border-radius: 50%;
            border: 5px solid #000;
            overflow: hidden;
        }
        .wheel {
            width: 100%;
            height: 100%;
            position: absolute;
            transform-origin: center;
            transition: transform 5s cubic-bezier(0.33, 1, 0.68, 1);
            a
        }
        .slice {
            position: absolute;
            width: 50%;
            height: 50%;
            background-color: #eee;
            border: 2px solid #ccc;
            box-sizing: border-box;
            clip-path: polygon(0% 0%, 100% 0%, 50% 100%);
            transform-origin: 100% 100%;
               display: flex; 
            justify-content: center;  
            align-items: center; 
            color: white;  
            font-size: 12px;  
           text-align: center; 
            padding: 5px;  
        }
        .slice:nth-child(1) { background: #f94144; transform: rotate(0deg); }
        .slice:nth-child(2) { background: #f3722c; transform: rotate(60deg); }
        .slice:nth-child(3) { background: #f8961e; transform: rotate(120deg); }
        .slice:nth-child(4) { background: #f9c74f; transform: rotate(180deg); }
        .slice:nth-child(5) { background: #90be6d; transform: rotate(240deg); }
        .slice:nth-child(6) { background: #43aa8b; transform: rotate(300deg); }
        .pointer {
            position: absolute;
            top: -15px;
            left: 50%;
            width: 0;
            height: 0;
            border-left: 15px solid transparent;
            border-right: 15px solid transparent;
            border-bottom: 30px solid #000;
            transform: translateX(-50%);
            z-index: 1;
        }
        button {
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            background-color: #4caf50;
            color: white;
            border: none;
            border-radius: 5px;
        }
        button:disabled {
            background-color: #aaa;
            cursor: not-allowed;
        }
        #result {
            margin-top: 20px;
            font-size: 20px;
            font-weight: bold;
            color: #333;
        }
        #spinButton {
          transform: translateX(50%)
        }
    </style>
</head>
<body>
    <div class="wheel-container">
        <div class="pointer"></div>
        <div class="wheel" id="wheel">
            <div class="slice">Italian food</div>
            <div class="slice">Chinese food</div>
            <div class="slice">Indian food</div>
            <div class="slice">Japanese food</div>
            <div class="slice">Mexican food</div>
            <div class="slice">Thai food</div>
        </div>
    </div>
    <button id="spinButton" onclick="spinWheel()">Spin the Wheel</button>
    <div id="result"></div>

<script>
        let currentRotation = 0;
        const spinButton = document.getElementById('spinButton');
        const resultDiv = document.getElementById('result');

        // Add single wheel sound effect
        const spinSound = new Audio('https://cdn.freesound.org/previews/242/242501_4414128-lq.mp3');  // Click sound for spin

        function spinWheel() {
            spinButton.disabled = true;
            
            // Play spin sound
            spinSound.volume = 0.3;
            spinSound.play();

            const wheel = document.getElementById('wheel');
            const randomRotations = Math.floor(Math.random() * 4) + 5;
            const randomSlice = Math.floor(Math.random() * 360);
            const totalRotation = randomRotations * 360 + randomSlice;

            currentRotation += totalRotation;
            wheel.style.transform = `rotate(${currentRotation}deg)`;

            setTimeout(() => {
                spinButton.disabled = false;
                const normalizedRotation = currentRotation % 360;
                const sliceIndex = (6 - Math.floor(normalizedRotation / 60)) % 6;
                const slices = document.querySelectorAll('.slice');
                const selectedCuisine = slices[sliceIndex].textContent;
                resultDiv.textContent = `The Spinner Chose: ${selectedCuisine}`;
                createDynamicButton(selectedCuisine);
            }, 5000);
        }

        // Function to create a button and set its link based on the selected cuisine
        function createDynamicButton(selectedCuisine) {
            // Clear any existing button
            const existingButton = document.querySelector(".dynamic-link");
            if (existingButton) existingButton.remove();

            // Get the link associated with the selected cuisine
            const link = cuisinePages[selectedCuisine];

            if (link) {
                // Create a button element
                const button = document.createElement("button");
                button.textContent = `Go to ${selectedCuisine.charAt(0).toUpperCase() + selectedCuisine.slice(1)} Cuisine`;
                button.classList.add("dynamic-link");

                // Add a click event to redirect to the page
                button.addEventListener("click", () => {
                    window.location.href = link;
                });

                // Append the button to the document body (or another container)
                document.body.appendChild(button);
            }
        }

        // Object mapping variable values to URLs
        const cuisinePages = {
            "Italian food": "{{site.baseurl}}/navigation/cuisine/italian",
            "Chinese food": "{{site.baseurl}}/navigation/cuisine/chinese",
            "Indian food": "{{site.baseurl}}/navigation/cuisine/indian",
            "Japanese food": "{{site.baseurl}}/navigation/cuisine/japanese",
            "Mexican food": "{{site.baseurl}}/navigation/cuisine/mexican",
            "Thai food": "{{site.baseurl}}/navigation/cuisine/thai"
        };
    </script>
</body>







<head>
  <title>Recipe Posting System</title>
  <style>
        /* Wrapper to isolate the container */
        .recipe-wrapper {
        position: absolute; /* Position the container */
        top: 50%; /* Center vertically */
        left: 20px; 
        transform: translateY(-50%); /* Adjust for vertical centering */
        padding: 30px;
        max-width: 700px;
        background-color: #f4f4f9;
        border: 1px solid #ddd;
        border-radius: 10px;
        box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        body {
        margin: 0;
        padding: 0;
        background-color: #fdfdfd;
        }
        .container {
        background: white;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
        }
        form label {
        display: block; /* Labels on their own line */
        margin-bottom: 5px; /* Small spacing below the label */
        font-weight: bold;
        color: #333;
        }
  </style>
</head>

<body>
  <section class="recipe-wrapper">
    <div class="container">
        <h1>Recipe Posting System</h1>
        <form id="recipeForm">
        <label for="name">Your Name:</label>
        <input type="text" id="name" placeholder="Enter your name" required>
        <label for="dish">Dish Name:</label>
        <input type="text" id="dish" placeholder="Enter the dish name" required>
        <label for="cuisine">Cuisine:</label>
        <input type="text" id="cuisine" placeholder="Enter the cuisine type" required>
        <label for="link">Recipe Link:</label>
        <input type="url" id="link" placeholder="Enter the recipe URL" required>
        <label for="comments">Comments:</label>
        <textarea id="comments" placeholder="Enter your comments" required></textarea>
        <button type="submit">Post Recipe</button>
        </form>
        <div id="postsContainer">
        </div>
    </div>


<style>
    .discover-more-button {
    display: inline-block;
    margin-top: 10px;
    padding: 10px 15px;
    background-color: #007BFF;
    color: white;
    text-decoration: none;
    border-radius: 5px;
    font-size: 1rem;
}

.discover-more-button:hover {
    background-color: #0056b3;
}
</style>

<script>
    document.getElementById("recipeForm").addEventListener("submit", function (e) {
    e.preventDefault();

    // Get form inputs
    const name = document.getElementById("name").value;
    const dish = document.getElementById("dish").value;
    const cuisine = document.getElementById("cuisine").value;
    const link = document.getElementById("link").value;
    const comments = document.getElementById("comments").value;

    // Create a post object
    const post = { name, dish, cuisine, link, comments };

    // Retrieve existing posts from localStorage
    const posts = JSON.parse(localStorage.getItem("posts")) || [];

    // Add the new post
    posts.push(post);

    // Save back to localStorage
    localStorage.setItem("posts", JSON.stringify(posts));

    // Display confirmation message
    const formContainer = document.querySelector(".container");
    formContainer.innerHTML = 
        <p>Your recipe has been posted!</p>
        <p><a href="{{site.baseurl}}/navigation/buttons/posting" class="discover-more-button">Discover More</a></p>
    ;
    });
  </script>

<h3>
  <a class="Fridge" href="{{site.baseurl}}/natcountrygen" style="font-family: 'Roboto', sans-serif; font-size: 24px; font-weight: bold; text-transform: uppercase; text-decoration: none; background-color: #00aaff; color: white; padding: 12px 24px; border-radius: 8px; transition: all 0.3s ease-in-out; box-shadow: 0px 4px 15px rgba(0, 0, 0, 0.1); display: inline-block;">
    NatCountryGen
  </a>
  
</h3>

<style>
  .Fridge:hover {
    background-color: #0077cc;  /* Darker blue on hover */
    transform: scale(1.05);  /* Slight zoom effect on hover */
    box-shadow: 0px 8px 20px rgba(0, 0, 0, 0.15);  /* Stronger shadow on hover */
  }

  .Fridge:focus {
    outline: none;  /* Remove outline on focus */
    border: 2px solid #ffcc00;  /* Add a cool yellow border when focused */
  }
</style>

<h3>
  <a class="Fridge" href="{{site.baseurl}}/navigation/buttons/posting" style="font-family: 'Roboto', sans-serif; font-size: 24px; font-weight: bold; text-transform: uppercase; text-decoration: none; background-color: #00aaff; color: white; padding: 12px 24px; border-radius: 8px; transition: all 0.3s ease-in-out; box-shadow: 0px 4px 15px rgba(0, 0, 0, 0.1); display: inline-block;">
    Posting
  </a>
  
</h3>

<style>
  .Fridge:hover {
    background-color: #0077cc;  /* Darker blue on hover */
    transform: scale(1.05);  /* Slight zoom effect on hover */
    box-shadow: 0px 8px 20px rgba(0, 0, 0, 0.15);  /* Stronger shadow on hover */
  }

  .Fridge:focus {
    outline: none;  /* Remove outline on focus */
    border: 2px solid #ffcc00;  /* Add a cool yellow border when focused */
  }
</style>

<h3>
  <a class="Fridge" href="{{site.baseurl}}/navigation/feedback" style="font-family: 'Roboto', sans-serif; font-size: 24px; font-weight: bold; text-transform: uppercase; text-decoration: none; background-color: #00aaff; color: white; padding: 12px 24px; border-radius: 8px; transition: all 0.3s ease-in-out; box-shadow: 0px 4px 15px rgba(0, 0, 0, 0.1); display: inline-block;">
    Feedback
  </a>
  
</h3>

<style>
  .Fridge:hover {
    background-color: #0077cc;  /* Darker blue on hover */
    transform: scale(1.05);  /* Slight zoom effect on hover */
    box-shadow: 0px 8px 20px rgba(0, 0, 0, 0.15);  /* Stronger shadow on hover */
  }

  .Fridge:focus {
    outline: none;  /* Remove outline on focus */
    border: 2px solid #ffcc00;  /* Add a cool yellow border when focused */
  }
</style>
