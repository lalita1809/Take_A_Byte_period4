---
layout: post
title: Indian cuisines
search_exclude: true
hide: true
permalink: /navigation/cuisine/indian
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
    <h3>About Indian cuisine: </h3>
    <ul>
        <li>Indian cuisine is a rich tapestry of bold flavors and aromatic spices, featuring diverse dishes like curries, biryanis, and flatbreads, often tailored to regional and cultural traditions.</li>
    </ul>

<button onclick="fetchRandomRecipes()">Shuffle Recipes</button>
<button onclick="viewStoredRecipes()">Stored Recipes</button>
    <div id="recipe-data"></div>

<script>
    async function fetchRandomRecipes() {
        const apiUrls = {
                chicken: [
                    'http://127.0.0.1:8887/api/indian_recipe/ButterChicken',
                    'http://127.0.0.1:8887/api/indian_recipe/ChickenTikkaMasala',
                    'http://127.0.0.1:8887/api/indian_recipe/ChickenKorma',
                    'http://127.0.0.1:8887/api/indian_recipe/ChickenVindaloo',
                    'http://127.0.0.1:8887/api/indian_recipe/ChickenSaag',
                    'http://127.0.0.1:8887/api/indian_recipe/ChickenBiryani'
                ],
                beef: [
                    'http://127.0.0.1:8887/api/indian_recipe/BeefCurry',
                    'http://127.0.0.1:8887/api/indian_recipe/BeefVindaloo',
                    'http://127.0.0.1:8887/api/indian_recipe/BeefKeema',
                    'http://127.0.0.1:8887/api/indian_recipe/BeefRoganJosh',
                    'http://127.0.0.1:8887/api/indian_recipe/BeefBiryani'
                ],
                vegan: [
                    'http://127.0.0.1:8887/api/indian_recipe/ChanaMasala',
                    'http://127.0.0.1:8887/api/indian_recipe/AlooGobi',
                    'http://127.0.0.1:8887/api/indian_recipe/BainganBharta',
                    'http://127.0.0.1:8887/api/indian_recipe/VeganTikkaMasala',
                    'http://127.0.0.1:8887/api/indian_recipe/VeganBiryani'
                ],
                fish: [
                    'http://127.0.0.1:8887/api/indian_recipe/FishCurry',
                    'http://127.0.0.1:8887/api/indian_recipe/GoanFishCurry',
                    'http://127.0.0.1:8887/api/indian_recipe/FishTikka',
                    'http://127.0.0.1:8887/api/indian_recipe/FishFry',
                    'http://127.0.0.1:8887/api/indian_recipe/MasalaFish'
                ],
                lamb: [
                    'http://127.0.0.1:8887/api/indian_recipe/LambCurry',
                    'http://127.0.0.1:8887/api/indian_recipe/LambRoganJosh',
                    'http://127.0.0.1:8887/api/indian_recipe/LambKorma',
                    'http://127.0.0.1:8887/api/indian_recipe/LambKeema',
                    'http://127.0.0.1:8887/api/indian_recipe/LambBiryani'
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
                    <h3>${recipe.dish}</h3>
                    <p><strong>Ingredients:</strong> ${recipe.ingredients}</p>
                    <p><strong>Instructions:</strong> ${recipe.instructions}</p>
                    <button onclick='deleteRecipe(${recipe.id})'>Delete Recipe</button>  <!-- Add delete button -->
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

        async function deleteRecipe(recipeId) {
    try {
        const response = await fetch(`http://127.0.0.1:8887/api/chinese_recipe/delete_recipe/${recipeId}`, {
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