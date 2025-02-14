---
layout: post
title: Chinese cuisines
search_exclude: true
hide: true
permalink: /navigation/cuisine/chinese
---

<style>
#recipe-data {
    display: flex;
    flex-wrap: wrap; 
    justify-content: flex-start;  
    gap: 20px;  
    padding: 20px;
}


.recipe-card {
    background-color: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    min-height: 350px;
    width: 250px; 
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    margin-bottom: 20px;  
}


#recipe-data .recipe-card:nth-child(3n+1) {
    margin-left: 30px;
}


#recipe-data .recipe-card:nth-child(3n+2) {
    margin-left: auto;
    margin-right: auto; 
}


#recipe-data .recipe-card:nth-child(3n+3) {
    margin-left: auto;
}


#recipe-data .recipe-card:nth-child(4) {
    margin-left: 120px; 
}


.recipe-card:hover {
    transform: translateY(-10px);  
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15);
}


.recipe-card h3 {
    margin-top: 0;
    font-size: 1.2em;
    font-weight: bold;
}


.recipe-card p {
    margin: 5px 0;
    font-size: 1em;
    line-height: 1.5;
    flex-grow: 1;  
}


.recipe-card button {
    display: block;
    width: 100%;
    padding: 10px;
    background-color: #4CAF50;
    color: white;
    font-size: 16px;
    border: none;
    cursor: pointer;
    border-radius: 5px;
    margin-top: 10px;
    font-weight: bold;
}

.recipe-card button:hover {
    background-color: #45a049;
}

  
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
    .recipe-card {
    background-color: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    min-height: 350px;
    width: 250px; 
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    margin-bottom: 20px;
}

.recipe-card h3 {
    margin-top: 0;
    font-size: 1.2em;
    font-weight: bold;
    text-align: left;  /* Ensures title is aligned to the left */
}

.recipe-card p {
    margin: 5px 0;
    font-size: 1em;
    line-height: 1.5;
    text-align: left;  /* Align ingredients and instructions left */
    flex-grow: 1;
}

.recipe-card button {
    display: block;
    width: 100%;
    padding: 10px;
    background-color: #4CAF50;
    color: white;
    font-size: 16px;
    border: none;
    cursor: pointer;
    border-radius: 5px;
    margin-top: 10px;
}

.recipe-card button:hover {
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

<body>
    <h3>About Chinese cuisine: </h3>
    <ul>
        <li>Chinese cuisine is a diverse and flavorful culinary tradition emphasizing fresh ingredients, balanced tastes, and techniques like stir-frying, steaming, and braising, with regional specialties showcasing unique flavors and ingredients.</li>
    </ul>

  <button onclick="fetchRandomRecipes()">Shuffle Recipes</button>
  <button onclick="viewStoredRecipes()">Stored Recipes</button>
    <div id="recipe-data"></div>
    <div id="stored-recipes" style="margin-top: 20px;"></div>

  <script>
        var pythonURI;
    if (location.hostname === "localhost") {
        pythonURI = "http://localhost:8887";
    } else if (location.hostname === "127.0.0.1") {
        pythonURI = "http://127.0.0.1:8887";
    } else {
        pythonURI = "https://takeabyte.stu.nighthawkcodingsociety.com";
    }
    
      async function fetchRandomRecipes() {
          const apiUrls = {
                chicken: [
                    `${pythonURI}/api/chinese_recipe/KungPaoChicken`,
                    `${pythonURI}/api/chinese_recipe/OrangeChicken`,
                    `${pythonURI}/api/chinese_recipe/LemonChicken`,
                    `${pythonURI}/api/chinese_recipe/CrispySweetAndSourChicken`,
                    `${pythonURI}/api/chinese_recipe/ChickenWithCashews`,
                    `${pythonURI}/api/chinese_recipe/SzechuanChicken`
                ],
                beef: [
                    `${pythonURI}/api/chinese_recipe/BeefWithBroccoli`,
                    `${pythonURI}/api/chinese_recipe/MongolianBeef`,
                    `${pythonURI}/api/chinese_recipe/BeefWithBlackBeanSauce`,
                    `${pythonURI}/api/chinese_recipe/BeefAndPeppersStirFry`,
                    `${pythonURI}/api/chinese_recipe/ChineseSpicyBeef`
                ],
                vegan: [
                    `${pythonURI}/api/chinese_recipe/MapoTofu`,
                    `${pythonURI}/api/chinese_recipe/VeganKungPaoTofu`,
                    `${pythonURI}/api/chinese_recipe/VeganSweetAndSourTofu`,
                    `${pythonURI}/api/chinese_recipe/VeganHotAndSourSoup`,
                    `${pythonURI}/api/chinese_recipe/VeganFriedRice`,
                    `${pythonURI}/api/chinese_recipe/VeganStirFryWithTofu`
                ],
                fish: [
                    `${pythonURI}/api/chinese_recipe/FishInBlackBeanSauce`,
                    `${pythonURI}/api/chinese_recipe/SteamedFishWithGingerAndSoySauce`,
                    `${pythonURI}/api/chinese_recipe/FishTofuSoup`,
                    `${pythonURI}/api/chinese_recipe/CrispyFishFillets`,
                    `${pythonURI}/api/chinese_recipe/FishWithSoyAndGarlicSauce`,
                    `${pythonURI}/api/chinese_recipe/FishAndEggplantStirFry`
                ],
                lamb: [
                    `${pythonURI}/api/chinese_recipe/BraisedLambWithSoySauce`,
                    `${pythonURI}/api/chinese_recipe/LambStirFryWithPeppers`,
                    `${pythonURI}/api/chinese_recipe/LambWithBlackBeanSauce`,
                    `${pythonURI}/api/chinese_recipe/SzechuanLamb`,
                    `${pythonURI}/api/chinese_recipe/LambWithVegetablesStirFry`,
                    `${pythonURI}/api/chinese_recipe/LambCurry`
                ]
            };


            const selectedUrls = {
                chicken: apiUrls.chicken[Math.floor(Math.random() * apiUrls.chicken.length)],
                beef: apiUrls.beef[Math.floor(Math.random() * apiUrls.beef.length)],
                vegan: apiUrls.vegan[Math.floor(Math.random() * apiUrls.vegan.length)],
                fish: apiUrls.fish[Math.floor(Math.random() * apiUrls.fish.length)],
                lamb: apiUrls.lamb[Math.floor(Math.random() * apiUrls.lamb.length)]
            };

            try {
                const recipeDataDiv = document.getElementById('recipe-data');
                recipeDataDiv.innerHTML = ''; // Clear previous recipes

                const fetchPromises = Object.values(selectedUrls).map(async (url) => {
                    const response = await fetch(url);
                    if (response.ok) {
                        return await response.json();
                    } else {
                        throw new Error('Error fetching a recipe');
                    }
                });

                const recipes = await Promise.all(fetchPromises);

                recipes.forEach(recipe => {
                    const recipeDiv = document.createElement('div');
                    recipeDiv.classList.add('recipe-card');
                    recipeDiv.innerHTML = `
                        <h3>${recipe.dish}</h3>
                        <p><strong>Time:</strong> ${recipe.time} minutes</p>
                        <p><strong>Ingredients:</strong> ${Array.isArray(recipe.ingredients) ? recipe.ingredients.join(', ') : recipe.ingredients}</p>
                        <p><strong>Instructions:</strong> ${recipe.instructions}</p>
                        <button onclick='saveRecipe(${JSON.stringify(recipe)})'>Save Recipe</button>
                    `;
                    recipeDataDiv.appendChild(recipeDiv);
                });

                recipeDataDiv.style.display = 'flex';  
            } catch (error) {
                document.getElementById('recipe-data').innerText = `Error: ${error.message}`;
            }
        }

           async function saveRecipe(recipe) {
            try {
                const response = await fetch(`${pythonURI}/save_recipe`, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify({
                        "name": recipe.dish,
                        "dish": recipe.dish,
                        "time": recipe.time,
                        "ingredients": recipe.ingredients,
                        "instructions": recipe.instructions
                    })
                });

                const result = await response.json();
                alert(result.message);
            } catch (error) {
                alert(`Error: ${error.message}`);
            }
        }

        async function viewStoredRecipes() {
    try {
        const response = await fetch(`${pythonURI}/get_recipes`);
        const contentType = response.headers.get("content-type");

        if (contentType && contentType.indexOf("application/json") !== -1) {
            const recipes = await response.json();

            const recipeDataDiv = document.getElementById('recipe-data');
            recipeDataDiv.innerHTML = ''; // Clear previous recipes

            recipes.forEach(recipe => {
                const recipeDiv = document.createElement('div');
                recipeDiv.classList.add('recipe-card');
                recipeDiv.innerHTML = `
                    <h3>${recipe.dish}</h3>
                    <p><strong>Ingredients:</strong> ${recipe.ingredients}</p>
                    <p><strong>Instructions:</strong> ${recipe.instructions}</p>
                    <button onclick='deleteRecipe(${recipe.id})'>Delete Recipe</button>
                    <button onclick='editRecipe(${JSON.stringify(recipe)})'>Edit Recipe</button>

                `;
                recipeDataDiv.appendChild(recipeDiv);
            });
        } else {
            throw new Error('Invalid response from server');
        }
    } catch (error) {
        document.getElementById('recipe-data').innerText = `Error: ${error.message}`;
    }
}

async function editRecipe(recipe) {
    const formHTML = `
        <h3>Edit Recipe</h3>
        <label for="name">Recipe Name:</label>
        <input type="text" id="name" value="${recipe.dish}" required readonly>
        <label for="ingredients">Ingredients:</label>
        <textarea id="ingredients" required>${recipe.ingredients}</textarea>
        <label for="instructions">Instructions:</label>
        <textarea id="instructions" required readonly>${recipe.instructions}</textarea>
        <button onclick="submitEdit(${recipe.id})">Submit Changes</button>
        <button onclick="closeEditForm()">Cancel</button>
    `;
    
    const formContainer = document.getElementById('stored-recipes');
    formContainer.innerHTML = formHTML;
}

function closeEditForm() {
    const formContainer = document.getElementById('stored-recipes');
    formContainer.innerHTML = '';  // Close the form
}

async function submitEdit(recipeId) {
    const updatedRecipe = {
        name: document.getElementById('name').value,
        ingredients: document.getElementById('ingredients').value,
        instructions: document.getElementById('instructions').value
    };

    try {
        const response = await fetch(`${pythonURI}/api/chinese_recipe/edit_recipe/${recipeId}`, { 
            method: 'PUT',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(updatedRecipe)
        });

        if (response.ok) {
            alert('Recipe updated successfully');
            viewStoredRecipes();  // Refresh stored recipes
        } else {
            alert('Failed to update recipe');
        }
    } catch (error) {
        alert(`Error: ${error.message}`);
    }
}
      async function deleteRecipe(recipeId) {
    try {
        const response = await fetch(`${pythonURI}/api/chinese_recipe/delete_recipe/${recipeId}`, {
            method: 'DELETE',
        });

        if (response.ok) {
            alert('Recipe deleted successfully');
            // Optionally, refresh the list of recipes
            viewStoredRecipes();
        } else {
            const data = await response.json();
            alert(data.error || 'Error deleting recipe');
        }
    } catch (error) {
        alert(`Error: ${error.message}`);
    }
}

    </script>
</body>


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