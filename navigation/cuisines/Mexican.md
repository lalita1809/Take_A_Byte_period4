---
layout: post
title: Mexican cuisines
search_exclude: true
hide: true
permalink: /navigation/cuisine/mexican
---

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

<body>
    <h3>About Mexican cuisine: </h3>
    <ul>
        <li>Mexican cuisine is vibrant and flavorful, featuring staples like corn, beans, and chili peppers in dishes such as tacos, enchiladas, and mole, often accented with fresh herbs, spices, and zesty sauces.</li>
    </ul>

<button onclick="fetchRandomRecipes()">Shuffle Recipes</button>
<button onclick="viewStoredRecipes()">Stored Recipes</button>
    <div id="recipe-data"></div>

<script>
        async function fetchRandomRecipes() {
            const apiUrls = {
                chicken: [
                    'http://127.0.0.1:8887/api/mexican_recipe/ChickenEnchiladas',
                    'http://127.0.0.1:8887/api/mexican_recipe/ChickenTacos',
                    'http://127.0.0.1:8887/api/mexican_recipe/ChickenFajitas',
                    'http://127.0.0.1:8887/api/mexican_recipe/PolloAsado',
                    'http://127.0.0.1:8887/api/mexican_recipe/ChickenQuesadillas',
                    'http://127.0.0.1:8887/api/mexican_recipe/ChickenTamales'
                ],
                beef: [
                    'http://127.0.0.1:8887/api/mexican_recipe/BeefEnchiladas',
                    'http://127.0.0.1:8887/api/mexican_recipe/BeefTacos',
                    'http://127.0.0.1:8887/api/mexican_recipe/BeefFajitas',
                    'http://127.0.0.1:8887/api/mexican_recipe/BeefBurritos',
                    'http://127.0.0.1:8887/api/mexican_recipe/BeefTostadas',
                    'http://127.0.0.1:8887/api/mexican_recipe/CarneAsada'
                ],
                vegan: [
                    'http://127.0.0.1:8887/api/mexican_recipe/VeganTacos',
                    'http://127.0.0.1:8887/api/mexican_recipe/VeganBurritos',
                    'http://127.0.0.1:8887/api/mexican_recipe/VeganEnchiladas',
                    'http://127.0.0.1:8887/api/mexican_recipe/VeganQuesadillas',
                    'http://127.0.0.1:8887/api/mexican_recipe/VeganFajitas',
                    'http://127.0.0.1:8887/api/mexican_recipe/VeganTamales'
                ],
                fish: [
                    'http://127.0.0.1:8887/api/mexican_recipe/FishTacos',
                    'http://127.0.0.1:8887/api/mexican_recipe/CrispyFishTacos',
                    'http://127.0.0.1:8887/api/mexican_recipe/GrilledFishBurritos',
                    'http://127.0.0.1:8887/api/mexican_recipe/FishVeracruz',
                    'http://127.0.0.1:8887/api/mexican_recipe/FishCeviche',
                    'http://127.0.0.1:8887/api/mexican_recipe/FishFajitas'
                ],
                lamb: [
                    'http://127.0.0.1:8887/api/mexican_recipe/LambTacos',
                    'http://127.0.0.1:8887/api/mexican_recipe/LambBurritos',
                    'http://127.0.0.1:8887/api/mexican_recipe/LambFajitas',
                    'http://127.0.0.1:8887/api/mexican_recipe/LambEnchiladas',
                    'http://127.0.0.1:8887/api/mexican_recipe/BraisedLambShank',
                    'http://127.0.0.1:8887/api/mexican_recipe/LambQuesadillas'
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
                const response = await fetch('http://127.0.0.1:8887/save_recipe', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify(recipe)
                });
                const result = await response.json();
                alert(result.message);
            } catch (error) {
                alert(`Error: ${error.message}`);
            }
        }

        async function viewStoredRecipes() {
            try {
                const response = await fetch('http://127.0.0.1:8887/get_recipes');
                const contentType = response.headers.get("content-type");

                if (contentType && contentType.indexOf("application/json") !== -1) {
                    const recipes = await response.json();

                    const recipeDataDiv = document.getElementById('recipe-data');
                    recipeDataDiv.innerHTML = ''; // Clear previous recipes

                    recipes.forEach(recipe => {
                        const recipeDiv = document.createElement('div');
                        recipeDiv.classList.add('recipe-card');
                        recipeDiv.innerHTML = `
                            <h3>${recipe.title}</h3>
                            <p><strong>Ingredients:</strong> ${recipe.ingredients}</p>
                            <p><strong>Instructions:</strong> ${recipe.instructions}</p>
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
    </script>
</body>