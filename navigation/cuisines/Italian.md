---
layout: post
title: Italian cuisines
search_exclude: true
hide: true
permalink: /navigation/cuisine/italian
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
    <h3>About Italian cuisine: </h3>
    <ul>
        <li>Italian cuisine is a celebration of simple, high-quality ingredients, featuring dishes like pasta, pizza, and risotto, often enhanced with olive oil, fresh herbs, and regional cheeses.</li>
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
                    `${pythonURI}/api/italian_recipe/ChickenParmesan`,
                    `${pythonURI}/api/italian_recipe/ChickenAlfredo`,
                    `${pythonURI}/api/italian_recipe/ChickenMarsala`,
                    `${pythonURI}/api/italian_recipe/ChickenPiccata`,
                    `${pythonURI}/api/italian_recipe/ChickenCacciatore`,
                    `${pythonURI}/api/italian_recipe/ChickenRisotto`
                ],
                beef: [
                    `${pythonURI}/api/italian_recipe/BeefLasagna`,
                    `${pythonURI}/api/italian_recipe/SpaghettiBolognese`,
                    `${pythonURI}/api/italian_recipe/BeefBraciole`,
                    `${pythonURI}/api/italian_recipe/BeefFlorentine`,
                    `${pythonURI}/api/italian_recipe/BeefOssobuco`,
                    `${pythonURI}/api/italian_recipe/BeefRisotto`
                ],
                vegan: [
                    `${pythonURI}/api/italian_recipe/VeganSpaghetti`,
                    `${pythonURI}/api/italian_recipe/VeganLasagna`,
                    `${pythonURI}/api/italian_recipe/VeganRisotto`,
                    `${pythonURI}/api/italian_recipe/VeganPizza`,
                    `${pythonURI}/api/italian_recipe/VeganGnocchi`,
                    `${pythonURI}/api/italian_recipe/VeganMinestrone`
                ],
                fish: [
                    `${pythonURI}/api/italian_recipe/ShrimpScampi`,
                    `${pythonURI}/api/italian_recipe/LinguineWithClams`,
                    `${pythonURI}/api/italian_recipe/Cioppino`,
                    `${pythonURI}/api/italian_recipe/GrilledSalmon`,
                    `${pythonURI}/api/italian_recipe/TunaCarpaccio`,
                    `${pythonURI}/api/italian_recipe/FishRisotto`
                ],
                lamb: [
                    `${pythonURI}/api/italian_recipe/LambRagu`,
                    `${pythonURI}/api/italian_recipe/LambChops`,
                    `${pythonURI}/api/italian_recipe/LambRisotto`,
                    `${pythonURI}/api/italian_recipe/LambOssoBuco`,
                    `${pythonURI}/api/italian_recipe/LambMeatballs`,
                    `${pythonURI}/api/italian_recipe/LambLasagna`
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
        <button onclick="closeEditForm()">Close</button>
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