---
layout: base
title: About
permalink: /about
search_exclude: true
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fridge API</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            padding: 20px;
            background-color: #f4f4f4;
        }
        .container {
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
            background-color: white;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        h1 {
            text-align: center;
        }
        .form-group {
            margin-bottom: 15px;
        }
        input, button {
            width: 100%;
            padding: 10px;
            margin: 5px 0;
            border-radius: 4px;
            border: 1px solid #ccc;
        }
        button {
            background-color: #4CAF50;
            color: white;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049;
        }
        .fridge-list {
            margin-top: 30px;
        }
        .fridge-item {
            padding: 10px;
            background-color: #f8f8f8;
            border-radius: 4px;
            margin-bottom: 10px;
        }
    </style>
</head>
<body>
<div class="container">
<h1>Fridge API</h1>
<div class="form-group">
    <label for="ingredients">Ingredients:</label>
    <input type="text" id="ingredients" placeholder="e.g., chicken, garlic, lemon">
</div>
<div class="form-group">
    <label for="user_id">User ID:</label>
    <input type="number" id="user_id" placeholder="Enter your User ID">
</div>
<button id="addFridgeBtn">Add Ingredients to Fridge</button>

<div class="fridge-list" id="fridgeList">
    <h2>Your Fridge</h2>
    <!-- Fridge entries will be displayed here -->
</div>
</div>

<script>
const addFridgeBtn = document.getElementById('addFridgeBtn');
const ingredientsInput = document.getElementById('ingredients');
const userIdInput = document.getElementById('user_id');
const fridgeList = document.getElementById('fridgeList');

const API_URL = "http://localhost:8887/fridge";

// Add ingredients to fridge
addFridgeBtn.addEventListener('click', async () => {
    try {
        const response = await fetch(API_URL, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify({
                ingredients: ingredientsInput.value,
                user_id: userIdInput.value,
            }),
        });

        if (!response.ok) {
            throw new Error(`HTTP error! Status: ${response.status}`);
        }

        const data = await response.json();
        alert('Ingredients added successfully');
        displayFridgeItems(userIdInput.value);
    } catch (error) {
        console.error('Error:', error);
        alert(`An error occurred: ${error.message}`);
    }
});

// Fetch fridge items for the user
async function displayFridgeItems(userId) {
    try {
        const response = await fetch(`${API_URL}?user_id=${userId}`);
        if (!response.ok) {
            throw new Error(`HTTP error! Status: ${response.status}`);
        }

        const data = await response.json();
        fridgeList.innerHTML = '<h2>Your Fridge</h2>'; // Reset fridge list
        if (data.length > 0) {
            data.forEach((item) => {
                const fridgeItem = document.createElement('div');
                fridgeItem.classList.add('fridge-item');
                fridgeItem.textContent = `Ingredients: ${item.ingredients}`;
                fridgeList.appendChild(fridgeItem);
            });
        } else {
            fridgeList.innerHTML += '<p>No items found in your fridge.</p>';
        }
    } catch (error) {
        console.error('Error:', error);
        alert('An error occurred while fetching fridge items.');
    }
}
</script>
</body>
</html>
