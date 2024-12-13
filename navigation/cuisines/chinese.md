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
        "Mapo Tofu": {
            ingredients: [
                "Tofu (400g, firm)",
                "Ground pork (100g)",
                "Doubanjiang (1 tbsp)",
                "Soy sauce (1 tbsp)",
                "Rice wine (1 tbsp)",
                "Chili paste (1 tsp)",
                "Garlic (2 cloves)",
                "Ginger (1-inch piece)",
                "Spring onions (2 stalks)",
                "Sichuan peppercorns (1 tsp)",
                "Cornstarch (1 tsp)",
                "Vegetable oil (2 tbsp)"
            ],
            instructions: [
                "Cut tofu into cubes and blanch in hot water for 2 minutes.",
                "Heat oil in a pan and fry ground pork until browned.",
                "Add garlic, ginger, doubanjiang, and chili paste, stir-fry for 1 minute.",
                "Add soy sauce, rice wine, and a bit of water, bring to a simmer.",
                "Add tofu cubes and simmer for 10 minutes.",
                "Mix cornstarch with water and stir into the sauce to thicken.",
                "Top with spring onions and Sichuan peppercorns before serving."
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
        "Peking Duck": {
            ingredients: [
                "Whole duck (1, about 2kg)",
                "Hoisin sauce (3 tbsp)",
                "Soy sauce (2 tbsp)",
                "Chinese five-spice powder (1 tsp)",
                "Rice vinegar (2 tbsp)",
                "Honey (2 tbsp)",
                "Scallions (for garnish)",
                "Mandarin pancakes (optional)"
            ],
            instructions: [
                "Clean and dry the duck, then rub with Chinese five-spice powder and soy sauce.",
                "Place the duck in a hanging position for 6-12 hours to air-dry.",
                "Preheat the oven to 180°C (350°F) and roast the duck for about 2 hours.",
                "Mix hoisin sauce, rice vinegar, and honey to make the glaze.",
                "During the last 30 minutes, glaze the duck every 10 minutes.",
                "Serve with thin pancakes, hoisin sauce, and scallions."
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
