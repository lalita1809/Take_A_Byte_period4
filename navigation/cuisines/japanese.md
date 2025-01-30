---
layout: post
title: Japanese cuisines
search_exclude: true
hide: true
permalink: /navigation/cuisine/japanese
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
    <h3>About Japanese cuisine: </h3>
    <ul>
        <li>Japanese cuisine is elegant and refined, focusing on seasonal ingredients and balance in dishes like sushi, ramen, and tempura, often highlighting umami flavors and meticulous presentation.</li>
    </ul>

<button onclick="fetchRandomRecipes()">Shuffle Recipes</button>
<button onclick="viewStoredRecipes()">Stored Recipes</button>
    <div id="recipe-data"></div>
    <div id="stored-recipes" style="margin-top: 20px;"></div>

<script>
     async function fetchRandomRecipes() {
        const apiUrls = {
                chicken: [
                    'http://127.0.0.1:8887/api/japanese_recipe/ChickenTeriyaki',
                    'http://127.0.0.1:8887/api/japanese_recipe/ChickenKatsu',
                    'http://127.0.0.1:8887/api/japanese_recipe/ChickenYakitori',
                    'http://127.0.0.1:8887/api/japanese_recipe/ChickenRamen',
                    'http://127.0.0.1:8887/api/japanese_recipe/ChickenKaraage',
                    'http://127.0.0.1:8887/api/japanese_recipe/ChickenDonburi'
                ],
                beef: [
                    'http://127.0.0.1:8887/api/japanese_recipe/BeefTeriyaki',
                    'http://127.0.0.1:8887/api/japanese_recipe/BeefSukiyaki',
                    'http://127.0.0.1:8887/api/japanese_recipe/Gyudon',
                    'http://127.0.0.1:8887/api/japanese_recipe/BeefYakiniku',
                    'http://127.0.0.1:8887/api/japanese_recipe/BeefShabuShabu',
                    'http://127.0.0.1:8887/api/japanese_recipe/BeefTataki'
                ],
                vegan: [
                    'http://127.0.0.1:8887/api/japanese_recipe/VeganRamen',
                    'http://127.0.0.1:8887/api/japanese_recipe/VeganSushi',
                    'http://127.0.0.1:8887/api/japanese_recipe/VeganTempura',
                    'http://127.0.0.1:8887/api/japanese_recipe/VeganGyoza',
                    'http://127.0.0.1:8887/api/japanese_recipe/VeganDonburi',
                    'http://127.0.0.1:8887/api/japanese_recipe/VeganMisoSoup'
                ],
                fish: [
                    'http://127.0.0.1:8887/api/japanese_recipe/GrilledSalmon',
                    'http://127.0.0.1:8887/api/japanese_recipe/SabaShioyaki',
                    'http://127.0.0.1:8887/api/japanese_recipe/UnagiDonburi',
                    'http://127.0.0.1:8887/api/japanese_recipe/TunaTataki',
                    'http://127.0.0.1:8887/api/japanese_recipe/FishKaraage',
                    'http://127.0.0.1:8887/api/japanese_recipe/FishMisoSoup'
                ],
                lamb: [
                    'http://127.0.0.1:8887/api/japanese_recipe/BraisedLambShanks',
                    'http://127.0.0.1:8887/api/japanese_recipe/LambKatsu',
                    'http://127.0.0.1:8887/api/japanese_recipe/LambTeriyaki',
                    'http://127.0.0.1:8887/api/japanese_recipe/LambDonburi',
                    'http://127.0.0.1:8887/api/japanese_recipe/LambRamen',
                    'http://127.0.0.1:8887/api/japanese_recipe/LambYakiniku'
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