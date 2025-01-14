---
layout: post
title: Chinese cuisines
search_exclude: true
hide: true
permalink: /navigation/cuisine/chinese
---


<h3>About Chinese cuisine: </h3>

- Chinese cuisine is a diverse and flavorful culinary tradition emphasizing fresh ingredients, balanced tastes, and techniques like stir-frying, steaming, and braising, with regional specialties showcasing unique flavors and ingredients.


<style>
    body {
        font-family: Arial, sans-serif;
        margin: 0;
        padding: 20px;
        background-color: #f4f4f9;
    }
    h1 {
        text-align: center;
        color: #4CAF50;
    }
    .container {
        max-width: 600px;
        margin: 0 auto;
        background-color: white;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
    button {
        display: block;
        width: 100%;
        padding: 15px;
        background-color: #4CAF50;
        color: white;
        font-size: 18px;
        border: none;
        cursor: pointer;
        border-radius: 5px;
        margin-bottom: 20px;
    }
    button:hover {
        background-color: #45a049;
    }
    .recipe {
        display: none;
        font-size: 16px;
    }
    .recipe h2 {
        color: #333;
    }
    .ingredients, .instructions {
        margin-top: 15px;
    }
    .ingredients ul, .instructions ol {
        padding-left: 20px;
    }
</style>

<button onclick="fetchRandomRecipe()">Get Random Recipe</button>
<div id="recipe-data" style="display:none;"></div>

<script>
    async function fetchRandomRecipe() {
        const apiUrls = [
            'http://127.0.0.1:8887/api/chinese_recipe/KungPaoChicken',
            'http://127.0.0.1:8887/api/chinese_recipe/OrangeChicken',
            'http://127.0.0.1:8887/api/chinese_recipe/BeefWithBroccoli'
            // Add more URLs as needed
        ];

        // Randomly select an API URL from the array
        const randomIndex = Math.floor(Math.random() * apiUrls.length);
        const apiUrl = apiUrls[randomIndex];

        try {
            const response = await fetch(apiUrl);

            if (response.ok) {
                const recipe = await response.json();

                const recipeDataDiv = document.getElementById('recipe-data');
                recipeDataDiv.innerHTML = `
                    <h3>${recipe.dish}</h3>
                    <p><strong>Time:</strong> ${recipe.time} minutes</p>
                    <p><strong>Ingredients:</strong> ${recipe.ingredients}</p>
                    <p><strong>Instructions:</strong> ${recipe.instructions}</p>
                `;

                recipeDataDiv.style.display = 'block';  
            } else {
                document.getElementById('recipe-data').innerText = 'Error: Could not fetch a recipe';
            }
        } catch (error) {
            document.getElementById('recipe-data').innerText = `Error: ${error.message}`;
        }
    }
</script>


<style>
/* General Container Styling */
.chat-room-container {
  max-width: 800px;
  margin: 50px auto;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 10px;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15);
  font-family: 'Arial', sans-serif;
}

/* Header Styling */
.chat-header {
  font-size: 1.8em;
  text-align: center;
  margin-bottom: 20px;
  color: black; /* Changed text color to black */
}

/* Chat Box Styling */
.chat-box {
  border: 1px solid #ddd;
  border-radius: 8px;
  height: 300px;
  overflow-y: scroll;
  padding: 15px;
  font-size: 1.2em;
  background-color: #000;
  box-shadow: inset 0 2px 4px rgba(0, 0, 0, 0.1);
  color: black; /* Changed text color to black */
}

/* Message Styling */
.message {
  margin-bottom: 10px;
  padding: 5px 10px;
  border-radius: 5px;
  background-color: #eef2f7;
  color: black; /* Changed text color to black */
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

/* Feedback Section Styling */
.feedback-section {
  margin-top: 20px;
  text-align: center;
}

.feedback-buttons {
  display: flex;
  justify-content: center;
  gap: 15px;
}

.feedback-button {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 80px;
  height: 80px;
  background-color: #4CAF50;
  color: #fff;
  border: none;
  border-radius: 50%;
  font-size: 2em;
  cursor: pointer;
  transition: background-color 0.3s ease;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.feedback-button:hover {
  background-color: #3e8e41;
}

.feedback-button.thumbs-down {
  background-color: #f44336;
}

.feedback-button.thumbs-down:hover {
  background-color: #d32f2f;
}

.chat-input {
  display: flex;
  margin-top: 15px;
}

.chat-message {
  flex: 1;
  padding: 10px;
  font-size: 1.2em;
  border: 1px solid #ddd;
  border-radius: 5px;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  margin-right: 10px;
  color: black; /* Changed text color to black */
}

.send-button {
  padding: 10px 15px;
  font-size: 1.2em;
  background-color: #007BFF;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.send-button:hover {
  background-color: #0056b3;
}
</style>

<div class="chat-room-container">
  <h1 class="chat-header">Recipe Feedback</h1>
  <div class="chat-box" id="feedbackBox">
    <!-- Submitted feedback will appear here -->
  </div>
  
  <!-- Feedback Section -->
  <div class="feedback-section">
    <h2>Share your feedback!</h2>
    
    <div class="feedback-buttons">
      <button class="feedback-button thumbs-up" onclick="submitFeedback('up')">&#128077;</button>
      <button class="feedback-button thumbs-down" onclick="submitFeedback('down')">&#128078;</button>
    </div>
    
    <div class="chat-input">
      <input type="text" class="chat-message" id="userMessage" placeholder="Write your feedback here..." />
      <button class="send-button" onclick="submitMessage()">Submit</button>
    </div>
  </div>
</div>

<script>
  // Function to submit the feedback message
  function submitMessage() {
    const message = document.getElementById("userMessage").value;
    if (message) {
      const feedbackBox = document.getElementById("feedbackBox");
      const messageElement = document.createElement("div");
      messageElement.classList.add("message");
      messageElement.textContent = message;
      feedbackBox.appendChild(messageElement);
      document.getElementById("userMessage").value = ''; // Clear input after submit
    }
  }

  // Function to submit thumbs-up or thumbs-down feedback
  function submitFeedback(type) {
    const feedbackBox = document.getElementById("feedbackBox");
    const feedbackElement = document.createElement("div");
    feedbackElement.classList.add("message");

    if (type === "up") {
      feedbackElement.innerHTML = '<span style="color: #4CAF50;">👍</span> Thumbs Up';
    } else {
      feedbackElement.innerHTML = '<span style="color: #f44336;">👎</span> Thumbs Down';
    }

    feedbackBox.appendChild(feedbackElement);
  }
</script>

