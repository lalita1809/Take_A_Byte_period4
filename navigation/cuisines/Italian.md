---
layout: post
title: Italian cuisines
search_exclude: true
hide: true
permalink: /navigation/cuisine/italian
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
    .recipe-card {
        background-color: #fff;
        margin-bottom: 20px;
        padding: 20px;
        border-radius: 8px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
    .recipe-card h3 {
        margin-top: 0;
    }
    .recipe-card p {
        margin: 5px 0;
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
    <h3>About Italian cuisine: </h3>
    <ul>
        <li>Italian cuisine is a celebration of simple, high-quality ingredients, featuring dishes like pasta, pizza, and risotto, often enhanced with olive oil, fresh herbs, and regional cheeses.</li>
    </ul>

<button onclick="fetchRandomRecipes()">Shuffle Recipes</button>
<button onclick="viewStoredRecipes()">Stored Recipes</button>
    <div id="recipe-data"></div>
    <div id="stored-recipes" style="margin-top: 20px;"></div>

<script>
    async function fetchRandomRecipes() {
        const apiUrls = {
                chicken: [
                    'http://127.0.0.1:8887/api/italian_recipe/ChickenParmesan',
                    'http://127.0.0.1:8887/api/italian_recipe/ChickenAlfredo',
                    'http://127.0.0.1:8887/api/italian_recipe/ChickenMarsala',
                    'http://127.0.0.1:8887/api/italian_recipe/ChickenPiccata',
                    'http://127.0.0.1:8887/api/italian_recipe/ChickenCacciatore',
                    'http://127.0.0.1:8887/api/italian_recipe/ChickenRisotto'
                ],
                beef: [
                    'http://127.0.0.1:8887/api/italian_recipe/BeefLasagna',
                    'http://127.0.0.1:8887/api/italian_recipe/SpaghettiBolognese',
                    'http://127.0.0.1:8887/api/italian_recipe/BeefBraciole',
                    'http://127.0.0.1:8887/api/italian_recipe/BeefFlorentine',
                    'http://127.0.0.1:8887/api/italian_recipe/BeefOssobuco',
                    'http://127.0.0.1:8887/api/italian_recipe/BeefRisotto'
                ],
                vegan: [
                    'http://127.0.0.1:8887/api/italian_recipe/VeganSpaghetti',
                    'http://127.0.0.1:8887/api/italian_recipe/VeganLasagna',
                    'http://127.0.0.1:8887/api/italian_recipe/VeganRisotto',
                    'http://127.0.0.1:8887/api/italian_recipe/VeganPizza',
                    'http://127.0.0.1:8887/api/italian_recipe/VeganGnocchi',
                    'http://127.0.0.1:8887/api/italian_recipe/VeganMinestrone'
                ],
                fish: [
                    'http://127.0.0.1:8887/api/italian_recipe/ShrimpScampi',
                    'http://127.0.0.1:8887/api/italian_recipe/LinguineWithClams',
                    'http://127.0.0.1:8887/api/italian_recipe/Cioppino',
                    'http://127.0.0.1:8887/api/italian_recipe/GrilledSalmon',
                    'http://127.0.0.1:8887/api/italian_recipe/TunaCarpaccio',
                    'http://127.0.0.1:8887/api/italian_recipe/FishRisotto'
                ],
                lamb: [
                    'http://127.0.0.1:8887/api/italian_recipe/LambRagu',
                    'http://127.0.0.1:8887/api/italian_recipe/LambChops',
                    'http://127.0.0.1:8887/api/italian_recipe/LambRisotto',
                    'http://127.0.0.1:8887/api/italian_recipe/LambOssoBuco',
                    'http://127.0.0.1:8887/api/italian_recipe/LambMeatballs',
                    'http://127.0.0.1:8887/api/italian_recipe/LambLasagna'
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
                        throw new Error(`Error fetching a recipe from ${url}`);
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

        function saveRecipe(recipe) {
            let savedRecipes = JSON.parse(localStorage.getItem('savedRecipes')) || [];
            savedRecipes.push(recipe);
            localStorage.setItem('savedRecipes', JSON.stringify(savedRecipes));
            alert(`${recipe.dish} has been saved.`);
        }

        function viewStoredRecipes() {
            const savedRecipes = JSON.parse(localStorage.getItem('savedRecipes')) || [];
            const storedRecipesDiv = document.getElementById('stored-recipes');
            storedRecipesDiv.innerHTML = ''; // Clear previous recipes

            savedRecipes.forEach(recipe => {
                const recipeDiv = document.createElement('div');
                recipeDiv.classList.add('recipe-card');
                recipeDiv.innerHTML = `
                    <h3>${recipe.dish}</h3>
                    <p><strong>Time:</strong> ${recipe.time} minutes</p>
                    <p><strong>Ingredients:</strong> ${Array.isArray(recipe.ingredients) ? recipe.ingredients.join(', ') : recipe.ingredients}</p>
                    <p><strong>Instructions:</strong> ${recipe.instructions}</p>
                `;
                storedRecipesDiv.appendChild(recipeDiv);
            });

            storedRecipesDiv.style.display = 'flex';  
        }
    </script>
</body>