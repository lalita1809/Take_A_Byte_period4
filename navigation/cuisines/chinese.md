---
layout: post
title: Chinese cuisines
search_exclude: true
hide: true
permalink: /navigation/cuisine/chinese
---


<h3>About Chinese cuisine: </h3>

- Chinese cuisine is a diverse and flavorful culinary tradition emphasizing fresh ingredients, balanced tastes, and techniques like stir-frying, steaming, and braising, with regional specialties showcasing unique flavors and ingredients.

<h1>Random Chinese Recipe Generator</h1>
<div class="container">
    <button id="generateRecipeBtn">Generate Random Recipe</button>
    <div id="recipe" class="recipe">
        <h2 id="recipeName"></h2>
        <div class="ingredients">
            <h3>Ingredients:</h3>
            <ul id="ingredientsList"></ul>
        </div>
        <div class="instructions">
            <h3>Instructions:</h3>
            <ol id="instructionsList"></ol>
        </div>
    </div>
</div>

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

<script>
    const recipes = {
        "Kung Pao Chicken": {
            ingredients: [
                "Chicken breast (500g)",
                "Dried red chilies (10-12)",
                "Peanuts (50g)",
                "Soy sauce (2 tbsp)",
                "Rice vinegar (1 tbsp)",
                "Sugar (1 tsp)",
                "Cornstarch (1 tsp)",
                "Garlic (3 cloves)",
                "Ginger (1-inch piece)",
                "Spring onions (2 stalks)"
            ],
            instructions: [
                "Cut chicken into small cubes and marinate with soy sauce and cornstarch for 10 minutes.",
                "Heat oil in a wok, fry dried chilies and peanuts until fragrant.",
                "Add garlic and ginger, stir-fry for 30 seconds.",
                "Add chicken and stir-fry until golden brown.",
                "Mix soy sauce, rice vinegar, sugar, and stir into the wok.",
                "Add spring onions and stir-fry for 2 more minutes before serving."
            ]
        },
        "Sweet and Sour Pork": {
            ingredients: [
                "Pork tenderloin (500g)",
                "Bell peppers (2, sliced)",
                "Pineapple chunks (1 cup)",
                "Soy sauce (2 tbsp)",
                "Rice vinegar (2 tbsp)",
                "Ketchup (3 tbsp)",
                "Sugar (2 tbsp)",
                "Cornstarch (1 tbsp)",
                "Garlic (2 cloves)",
                "Egg (1, beaten)",
                "Flour (for coating)"
            ],
            instructions: [
                "Cut pork into bite-sized cubes and coat in flour and beaten egg.",
                "Deep-fry pork until golden and crispy, then set aside.",
                "In a pan, stir-fry garlic and bell peppers until soft.",
                "Add pineapple, soy sauce, rice vinegar, ketchup, and sugar, cook until the sauce thickens.",
                "Add fried pork and stir to coat evenly.",
                "Serve hot."
            ]
        },
        "Chow Mein": {
            ingredients: [
                "Chow mein noodles (200g)",
                "Chicken breast (200g, sliced)",
                "Carrot (1, julienned)",
                "Bell peppers (2, sliced)",
                "Spring onions (3 stalks)",
                "Soy sauce (2 tbsp)",
                "Oyster sauce (2 tbsp)",
                "Sesame oil (1 tsp)",
                "Garlic (3 cloves)",
                "Ginger (1-inch piece)",
                "Vegetable oil (2 tbsp)"
            ],
            instructions: [
                "Cook noodles according to package instructions and set aside.",
                "Heat oil in a wok, stir-fry garlic and ginger for 30 seconds.",
                "Add chicken and cook until browned.",
                "Add vegetables and stir-fry until tender.",
                "Add noodles, soy sauce, oyster sauce, and sesame oil, stir well.",
                "Top with spring onions and serve hot."
            ]
        },
        "Hot and Sour Soup": {
            ingredients: [
                "Chicken broth (4 cups)",
                "Shiitake mushrooms (1 cup, sliced)",
                "Tofu (200g, cubed)",
                "Bamboo shoots (1/2 cup, sliced)",
                "Soy sauce (3 tbsp)",
                "Rice vinegar (3 tbsp)",
                "Chili paste (1 tsp)",
                "Cornstarch (2 tbsp)",
                "Egg (1, beaten)",
                "Spring onions (for garnish)"
            ],
            instructions: [
                "Bring chicken broth to a boil in a pot.",
                "Add mushrooms, tofu, and bamboo shoots. Simmer for 5 minutes.",
                "Mix soy sauce, rice vinegar, and chili paste into the soup.",
                "Dissolve cornstarch in water and stir into the soup to thicken.",
                "Slowly pour in beaten egg while stirring gently.",
                "Garnish with spring onions and serve hot."
            ]
        },
        "Fried Rice": {
            ingredients: [
                "Cooked rice (3 cups, cooled)",
                "Eggs (2, beaten)",
                "Carrot (1, diced)",
                "Green peas (1/2 cup)",
                "Soy sauce (3 tbsp)",
                "Sesame oil (1 tsp)",
                "Garlic (2 cloves, minced)",
                "Spring onions (2 stalks, chopped)",
                "Vegetable oil (2 tbsp)"
            ],
            instructions: [
                "Heat oil in a wok, scramble the eggs, and set aside.",
                "In the same wok, stir-fry garlic, carrot, and peas for 3 minutes.",
                "Add rice, soy sauce, and sesame oil, stir-fry for 5 minutes.",
                "Mix in scrambled eggs and spring onions.",
                "Serve hot."
            ]
        },
        "General Tso's Chicken": {
            ingredients: [
                "Chicken breast (500g, cubed)",
                "Egg (1, beaten)",
                "Cornstarch (1/2 cup)",
                "Garlic (2 cloves, minced)",
                "Ginger (1 tsp, minced)",
                "Soy sauce (2 tbsp)",
                "Rice vinegar (2 tbsp)",
                "Sugar (3 tbsp)",
                "Chili paste (1 tsp)",
                "Vegetable oil (for frying)"
            ],
            instructions: [
                "Coat chicken in beaten egg and cornstarch.",
                "Deep-fry chicken until golden brown and set aside.",
                "In a pan, stir-fry garlic and ginger for 1 minute.",
                "Add soy sauce, rice vinegar, sugar, and chili paste. Simmer for 3 minutes.",
                "Toss fried chicken in the sauce and serve."
            ]
        }
    };

    const generateRecipeBtn = document.getElementById("generateRecipeBtn");
    const recipeContainer = document.getElementById("recipe");
    const recipeNameElement = document.getElementById("recipeName");
    const ingredientsList = document.getElementById("ingredientsList");
    const instructionsList = document.getElementById("instructionsList");

    generateRecipeBtn.addEventListener("click", () => {
        const recipeNames = Object.keys(recipes);
        const randomRecipeName = recipeNames[Math.floor(Math.random() * recipeNames.length)];
        const recipe = recipes[randomRecipeName];

        recipeNameElement.textContent = randomRecipeName;
        ingredientsList.innerHTML = recipe.ingredients.map(ingredient => `<li>${ingredient}</li>`).join('');
        instructionsList.innerHTML = recipe.instructions.map(instruction => `<li>${instruction}</li>`).join('');

        recipeContainer.style.display = 'block';
    });
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

