---
layout: base
title: Natgen
permalink: /natcountrygen/
search_exclude: true
---


<style>
    body {
        font-family: Arial, sans-serif;
        margin: 20px;
    }

    .container {
        max-width: 600px;
        margin: 0 auto;
    }

    .dish-info {
        margin-bottom: 20px;
    }

    .form-group {
        margin-bottom: 15px;
    }

    input,
    textarea {
        width: 100%;
        padding: 10px;
        margin-top: 5px;
        margin-bottom: 10px;
    }

    button {
        padding: 10px 20px;
        background-color: #4CAF50;
        color: white;
        border: none;
        cursor: pointer;
    }

    button:hover {
        background-color: #45a049;
    }
</style>
<div class="container">
    <h1>National Country Dish Generator</h1>

    <div class="dish-info">
        <h2 id="country-name">Country: </h2>
        <h3 id="dish-name">Dish: </h3>
        <p id="dish-description">Description: </p>
    </div>

    <button id="next-dish-btn">Next Dish</button>

    <hr>

    <h2>Create or Update a Country Dish</h2>
    <form id="create-update-form">
        <div class="form-group">
            <label for="country">Country:</label>
            <input type="text" id="country" name="country" required>
        </div>
        <div class="form-group">
            <label for="dish">Dish:</label>
            <input type="text" id="dish" name="dish" required>
        </div>
        <div class="form-group">
            <label for="description">Description:</label>
            <textarea id="description" name="description" required></textarea>
        </div>
        <button type="submit">Submit</button>
    </form>

    <hr>

    <h2>Your Posts</h2>
    <ul id="user-posts-list"></ul>
</div>

<script>
    var pythonURI;
    if (location.hostname === "localhost") {
        pythonURI = "http://localhost:8887";
    } else if (location.hostname === "127.0.0.1") {
        pythonURI = "http://127.0.0.1:8887";
    } else {
        pythonURI = "https://flocker.nighthawkcodingsociety.com";
    }

    const fetchOptions = {
        method: "GET",
        mode: "cors",
        cache: "default",
        credentials: "include",
        headers: {
            "Content-Type": "application/json",
            "X-Origin": "client",
        },
    };

    const nextDishBtn = document.getElementById('next-dish-btn');
    const createUpdateForm = document.getElementById('create-update-form');
    const countryName = document.getElementById('country-name');
    const dishName = document.getElementById('dish-name');
    const dishDescription = document.getElementById('dish-description');
    const userPostsList = document.getElementById('user-posts-list');

    let currentDishId = null;

    // Fetch a random dish and display it
    async function getRandomDish() {
        const response = await fetch(pythonURI + '/api/random');
        const data = await response.json();
        if (data) {
            countryName.textContent = `Country: ${data.country}`;
            dishName.textContent = `Dish: ${data.dish}`;
            dishDescription.textContent = `Description: ${data.description}`;
        }
    }

    // Fetch all user posts and display them
    async function getUserPosts() {
        const response = await fetch(pythonURI + '/api/countries');
        const data = await response.json();
        userPostsList.innerHTML = '';
        data.forEach(post => {
            const listItem = document.createElement('li');
            listItem.innerHTML = `
                    <strong>${post.country} - ${post.dish}</strong>: ${post.description}
                    <button onclick="editPost(${post.id}, '${post.country}', '${post.dish}', '${post.description}')">Edit</button>
                    <button onclick="deletePost(${post.id})">Delete</button>
                `;
            userPostsList.appendChild(listItem);
        });
    }

    // Create or update a post
    createUpdateForm.addEventListener('submit', async (e) => {
        e.preventDefault();
        const country = document.getElementById('country').value;
        const dish = document.getElementById('dish').value;
        const description = document.getElementById('description').value;

        const data = { country, dish, description };
        let url = pythonURI + '/api/add';
        let method = 'POST';

        if (currentDishId) {
            url = pythonURI + '/api/countries/update';
            method = 'PUT';
            data.id = currentDishId;
        }

        const response = await fetch(url, {
            method,
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify(data),
        });

        const result = await response.json();
        if (response.ok) {
            getRandomDish();
            getUserPosts();
            createUpdateForm.reset();
            currentDishId = null;
        } else {
            alert(result.error || 'An error occurred');
        }
    });

    // Edit a post (populate the form with the post details)
    function editPost(id, country, dish, description) {
        currentDishId = id;
        document.getElementById('country').value = country;
        document.getElementById('dish').value = dish;
        document.getElementById('description').value = description;
    }

    // Delete a post
    async function deletePost(id) {
        const response = await fetch(pythonURI + '/api/countries/delete', {
            method: 'DELETE',
            headers: {
                'Content-Type': 'application/json',
            },
            body: JSON.stringify({ id }),
        });

        const result = await response.json();
        if (response.ok) {
            getRandomDish();
            getUserPosts();
        } else {
            alert(result.error || 'An error occurred');
        }
    }

    // Initialize the page
    async function init() {
        await getRandomDish();
        await getUserPosts();
    }

    nextDishBtn.addEventListener('click', getRandomDish);

    init();
</script>