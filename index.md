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
        }
        .search-container input[type="text"] {
            width: calc(100% - 90px);
            padding: 10px;
            font-size: 16px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        .search-container button {
            padding: 10px 15px;
            font-size: 16px;
            border: none;
            background-color: #4CAF50;
            color: white;
            cursor: pointer;
            border-radius: 5px;
        }
        .search-container button:hover {
            background-color: #45a049;
        }
        .results {
            margin-top: 10px;
            background: #f9f9f9;
            border: 1px solid #ccc;
            border-radius: 5px;
            padding: 10px;
            max-height: 200px;
            overflow-y: auto;
        }
        .results a {
            display: block;
            margin: 5px 0;
            color: blue;
            text-decoration: none;
        }
        .results a:hover {
            text-decoration: underline;
        }
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
        // List of pages with keywords
        const pages = [
            { url: 'navigation/about', keywords: ['about', 'team', 'company'] },
            { url: 'navigation/cuisine/thai', keywords: ['thai', 'asia', 'thia'] },
            { url: 'navigation/cuisine/indian', keywords: ['india', 'indian', 'India'] },
            { url: 'navigation/cuisine/italian', keywords: ['Italian', 'italy', 'Italy'] }
        ];

        function performSearch() {
            const query = document.getElementById('searchInput').value.trim().toLowerCase();
            const resultsContainer = document.getElementById('results');
            resultsContainer.innerHTML = ''; // Clear previous results

            if (!query) {
                resultsContainer.innerHTML = '<p>Please enter a search term.</p>';
                return;
            }

            const matchingPages = pages.filter(page => 
                page.keywords.some(keyword => keyword.includes(query))
            );

            if (matchingPages.length === 0) {
                resultsContainer.innerHTML = '<p>No results found.</p>';
                return;
            }

            matchingPages.forEach(page => {
                const link = document.createElement('a');
                link.href = page.url;
                link.textContent = `Visit ${page.url}`;
                resultsContainer.appendChild(link);
            });
        }
    </script>
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
        let currentRotation = 0; // Track the current rotation of the wheel
        const spinButton = document.getElementById('spinButton');
        const resultDiv = document.getElementById('result');

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
            Chinese: "{{site.baseurl}}/navigation/cuisine/chinese",
            Indian: "{{site.baseurl}}/navigation/cuisine/indian",
            Japanese: "{{site.baseurl}}/navigation/cuisine/japanese",
            Mexican: "{{site.baseurl}}/navigation/cuisine/mexican",
            Thai: "{{site.baseurl}}/navigation/cuisine/thai",
            Italian: "{{site.baseurl}}/navigation/cuisine/italian",
};


        function spinWheel() {
            // Disable the spin button
            spinButton.disabled = true;

            const wheel = document.getElementById('wheel');
            const randomRotations = Math.floor(Math.random() * 4) + 5; // Random number of rotations (5 to 8)
            const randomSlice = Math.floor(Math.random() * 360); // Random degree for the final position
            const totalRotation = randomRotations * 360 + randomSlice; // Total rotation amount

            currentRotation += totalRotation; // Increment the total rotation
            wheel.style.transform = `rotate(${currentRotation}deg)`;

            // Determine which slice is selected after the spin
            setTimeout(() => {
                spinButton.disabled = false;

                // Calculate the final rotation position
                const normalizedRotation = currentRotation % 360;
                const sliceIndex = Math.floor((360 - normalizedRotation) / 60) % 6;

                // Get the selected cuisine
                const cuisines = ["Chinese", "Indian", "Japanese", "Mexican", "Thai", "Italian"];
                const selectedCuisine = cuisines[sliceIndex];

                // Display the result
                resultDiv.textContent = `The Spinner Chose: ${selectedCuisine}`;
                // Call the function with the variable
                createDynamicButton(selectedCuisine);
            }, 5000); // Matches the transition duration (5s)
        }


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
    formContainer.innerHTML = `
        <p>Your recipe has been posted!</p>
        <p><a href="{{site.baseurl}}/navigation/buttons/posting" class="discover-more-button">Discover More</a></p>
    `;
    });
  </script>

<!-- Full-Page byte Bot -->
<div
  id="byte-bot-container"
  style="
    display: flex;
    flex-direction: column;
    height: 100vh; /* Full page height */
    background: linear-gradient(
      135deg,
      #66bb6a,
      #388e3c
    ); /* Green gradient */
    font-family: 'Arial', sans-serif;
    color: white;
  "
>
  <!-- Header -->
  <div
    style=" 
      background-color: #2e7d32; /* Darker green for header */
      padding: 20px;
      text-align: center;
      font-size: 2rem;
      font-weight: bold;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
    "
  >
    Byte Bot
  </div>

  <!-- Chat Section -->
  <div
    id="chat-box"
    style="
      flex-grow: 1; /* Take up remaining space */
      padding: 20px;
      overflow-y: auto;
      background-color: rgba(200, 230, 201, 0.85); /* Semi-transparent light green */
      border-top: 2px solid #2e7d32;
      border-bottom: 2px solid #2e7d32;
      box-shadow: inset 0 4px 8px rgba(0, 0, 0, 0.1);
      border-radius: 10px; /* Slightly rounded corners */
    "
  ></div>

  <!-- Input Section -->
  <div
    style=" 
      display: flex;
      padding: 20px;
      background-color: #2e7d32; /* Same dark green as header */
      box-shadow: 0 -4px 8px rgba(0, 0, 0, 0.3);
    "
  >
    <input
      type="text"
      id="question"
      placeholder="Type your question here"
      style="
        flex-grow: 1; /* Take up as much space as possible */
        padding: 15px;
        border: none;
        border-radius: 5px;
        margin-right: 10px;
        font-size: 1rem;
        color: #2e7d32; /* Dark text */
        background-color: white; /* Input background */
      "
    />
    <button
      onclick="sendQuestion(document.getElementById('question').value)"
      style="
        padding: 15px 20px;
        background-color: white; /* Contrasting button background */
        color: #2e7d32; /* Dark green text */
        font-size: 1rem;
        font-weight: bold;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        transition: background-color 0.3s ease, color 0.3s ease;
      "
    >
      Ask byte bot
    </button>
  </div>
</div>

<!-- JavaScript for Chatbot -->
<script>
  var pythonURI;
  if (location.hostname === "localhost") {
    pythonURI = "http://localhost:8887";
  } else if (location.hostname === "127.0.0.1") {
    pythonURI = "http://127.0.0.1:8887";
  } else {
    pythonURI = "https://flocker.nighthawkcodingsociety.com";
  }

  const fetchOptions = {
    method: "GET",
    mode: "cors",
    cache: "default",
    credentials: "include",
    headers: {
      "Content-Type": "application/json",
      "X-Origin": "client",
    },
  };

  // Chatbot Logic
  async function sendQuestion(question) {
    const chatBox = document.getElementById("chat-box");

    // Display the user's question
    chatBox.innerHTML += `
            <div style="margin-bottom: 20px; background: rgba(232, 244, 200, 0.85); padding: 15px; border-radius: 8px;">
                <strong style="color: #2e7d32;">You:</strong> 
                <span style="color: #2e7d32;">${question}</span>
            </div>`;

    // Send the question to the backend
    const response = await fetch(`${pythonURI}/api/ai/help`, {
      ...fetchOptions,
      method: "POST",
      body: JSON.stringify({ question }),
    });

    // Display the AI's response
    const data = await response.json();
    const aiResponse = data.response || "Error: Unable to fetch response.";

    chatBox.innerHTML += `
            <div style="margin-bottom: 20px; background: #388e3c; padding: 15px; border-radius: 8px; color: white;">
                <strong>byte bot:</strong> ${aiResponse}
            </div>`;
    document.getElementById("question").value = ""; // Clear input
    chatBox.scrollTop = chatBox.scrollHeight; // Auto-scroll
  }

  // Attach the sendQuestion function to the "Ask byte bot" button
  document
    .querySelector('button[onclick="sendQuestion()"]')
    .addEventListener("click", () => {
      const question = document.getElementById("question").value.trim();
      if (question) {
        sendQuestion(question);
      } else {
        alert("Please enter a question!");
      }
    });
</script>

<!-- Optional CSS -->
<style>
  /* Chatbox Scrollbar Styling */
  #chat-box::-webkit-scrollbar {
    width: 8px;
  }

  #chat-box::-webkit-scrollbar-thumb {
    background: #388e3c;
    /* Match header and footer */
    border-radius: 5px;
  }

  /* Button Hover Effect */
  button:hover {
    background-color: #66bb6a;
    color: white;
  }
</style>

<h3>
  <a class="Fridge" href="{{site.baseurl}}/about" style="font-family: 'Roboto', sans-serif; font-size: 24px; font-weight: bold; text-transform: uppercase; text-decoration: none; background-color: #00aaff; color: white; padding: 12px 24px; border-radius: 8px; transition: all 0.3s ease-in-out; box-shadow: 0px 4px 15px rgba(0, 0, 0, 0.1); display: inline-block;">
    Fridge
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
