---
layout: post
title: Discover other recipes
search_exclude: true
hide: true
permalink: /navigation/buttons/posting
---



<head>
    <title>Recipe Posts</title>
    <style>
        body { font-family: Arial, sans-serif; background: #fdfdfd; margin: 20px; }
        .container { max-width: 800px; margin: 0 auto; padding: 20px; background: white; border-radius: 10px; box-shadow: 0 4px 8px rgba(0,0,0,0.1); }
        .post { border-bottom: 1px solid #ddd; padding: 10px 0; }
        h1, h2 { text-align: center; color: #333; }
        button { background-color: #007BFF; color: white; padding: 10px; border: none; border-radius: 5px; cursor: pointer; }
        button:hover { background-color: #0056b3; }
        .delete-button { background-color: #dc3545; }
        .delete-button:hover { background-color: #a71d2a; }
        .edit-button { background-color: #28a745; }
        .edit-button:hover { background-color: #218838; }
        #all-posts-section { margin-top: 30px; }
        body { font-family: Arial, sans-serif; background: #fdfdfd; margin: 20px; }
        .container { max-width: 800px; margin: 0 auto; padding: 20px; background: white; border-radius: 10px; box-shadow: 0 4px 8px rgba(0,0,0,0.1); }
        .post { border-bottom: 1px solid #ddd; padding: 10px 0; }
        h1, h2 { text-align: center; color: #333; }
        button { background-color: #007BFF; color: white; padding: 10px; border: none; border-radius: 5px; cursor: pointer; }
        button:hover { background-color: #0056b3; }
        .delete-button { background-color: #dc3545; }
        .delete-button:hover { background-color: #a71d2a; }
        .edit-button { background-color: #28a745; }
        .edit-button:hover { background-color: #218838; }
        #all-posts-section { margin-top: 30px; }
    </style>
</head>


<body>
<div class="container">
    <h1>Post a Recipe</h1>
    <form id="recipeForm">
        <p><label>Name: <input type="text" id="name" required></label></p>
        <p><label>Dish: <input type="text" id="dish" required></label></p>
        <p><label>Cuisine: <input type="text" id="cuisine" required></label></p>
        <p><label>Link: <input type="url" id="link" required></label></p>
        <p><label>Comments: <textarea id="comments" required></textarea></label></p>
        <p><button type="submit">Submit Recipe</button></p>
    </form>
    <div id="posting-data">Click a button to see recipes</div>
</div>
<!-- All Posts Section -->
<div id="all-posts-section">
    <h2>All Posts</h2>
    <div id="postsContainer"></div>
</div>

<script>

    var pythonURI;
    if (location.hostname === "localhost") {
        pythonURI = "http://localhost:8887";
    } else if (location.hostname === "127.0.0.1") {
        pythonURI = "http://127.0.0.1:8887";
    } else {
        pythonURI = "https://takeabyte.stu.nighthawkcodingsociety.com";
    }

document.getElementById("recipeForm").addEventListener("submit", async function (event) {
    event.preventDefault();

    const newPost = {
        name: document.getElementById("name").value,
        dish: document.getElementById("dish").value,
        cuisine: document.getElementById("cuisine").value,
        link: document.getElementById("link").value,
        comments: document.getElementById("comments").value
    };

    try {
        const response = await fetch(pythonURI + "/api/posting/create", {
            method: "POST",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(newPost)
        });

        if (response.ok) {
            alert("Recipe Posted Successfully!");
            document.getElementById("recipeForm").reset();
            fetchPosts();
        } else {
            alert("Error Posting Recipe.");
        }
    } catch (error) {
        console.error("Error:", error);
    }
});

async function fetchPosts() {
    try {
        const response = await fetch(pythonURI + "/api/posting/reading");
        const posts = await response.json();
        console.log(posts);  // Log the response to verify its structure
        const postsContainer = document.getElementById("postsContainer");
        postsContainer.innerHTML = ""; // Clear the current content

        if (!posts || posts.length === 0) {
            postsContainer.innerHTML = "<p>No recipes posted yet.</p>";
            return;
        }
        else {
            posts.forEach(post => {
                const postElement = document.createElement("div");
                postElement.classList.add("post");
                postElement.innerHTML = `
                    <p><strong>Name:</strong> ${post.name}</p>
                    <p><strong>Dish:</strong> ${post.dish}</p>
                    <p><strong>Cuisine:</strong> ${post.cuisine}</p>
                    <p><strong>Link:</strong> <a href="${post.link}" target="_blank">${post.link}</a></p>
                    <p><strong>Comments:</strong> ${post.comments}</p>
                    <button class="edit-button" onclick="editPost('${post.name}')">Edit</button>
                    <button class="delete-button" onclick="deletePost('${post.name}')">Delete</button>
                `;
                postsContainer.appendChild(postElement);
            });
        }
    } catch (error) {
        console.error("Error fetching posts:", error);
    }
}

// Edit a post
async function editPost(name) {
    const dish = prompt("Enter new dish:");
    const cuisine = prompt("Enter new cuisine:");
    const link = prompt("Enter new link:");
    const comments = prompt("Enter new comments:");

    const updatedPost = { name, dish, cuisine, link, comments };

    try {
        const response = await fetch(pythonURI + `/api/posting/update/`, {
            method: "PUT",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify(updatedPost)
        });

        if (response.ok) {
            alert("Recipe updated successfully!");
            fetchPosts(); // Reload posts after updating
        } else {
            alert("Error updating recipe.");
        }
    } catch (error) {
        console.error("Error:", error);
    }
}

// Delete a post
async function deletePost(name) {
    if (confirm("Are you sure you want to delete this post?")) {
        try {
            const response = await fetch(pythonURI + `/api/posting/delete`, {
                method: "DELETE",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({ name: name }) // Pass the name in the body
            });

            if (response.ok) {
                alert("Recipe deleted!");
                fetchPosts(); // Reload posts after deletion
            } else {
                alert("Error deleting recipe.");
            }
        } catch (error) {
            console.error("Error:", error);
        }
    }
}

// Load posts initially
fetchPosts();
</script>
</body>




<br><br>
<head>
    <title>Fetch Post Data</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: 50px;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            margin: 10px;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
        #posting-data {
            position: absolute; /* Allows positioning relative to the clicked button */
            display: none; /* Initially hidden */
            border: 1px solid #ddd;
            border-radius: 5px;
            background: #f9f9f9;
            padding: 10px;
            text-align: center;
            max-width: 400px;
            z-index: 10;
        }
    </style>
</head>




<body>
    <h4>Static users</h4>
    <button onclick="fetchStaticPosting('martha', event)">Martha</button>
    <button onclick="fetchStaticPosting('wayne', event)">Wayne</button>
    <!-- <div id="posting-data" style="display: none;">
    </div>-->
    <script>
        console.log("Script loaded! fetchPostingData function should be available.");
        async function fetchStaticPosting(posterName, event) {
            console.log(`Fetching data for: ${posterName}`);
            const apiUrl = pythonURI + `/api/posting/${posterName}`;
            try {
                const response = await fetch(apiUrl);
                if (!response.ok) throw new Error(`Could not fetch data for ${posterName}`);
                const data = await response.json();
                console.log("Data received:", data);
                // Display data on the page
                const postingDataDiv = document.getElementById('posting-data');
                postingDataDiv.innerHTML = `
                    <h2>${data.name}</h2>
                    <p><strong>Dish:</strong> ${data.dish}</p>
                    <p><strong>Cuisine:</strong> ${data.cuisine}</p>
                    <p><strong>Link:</strong> <a href="${data.link}" target="_blank">${data.link}</a></p>
                    <p><strong>Comments:</strong> ${data.comments}</p>
                `;
                // Position the div under the clicked button
                const buttonRect = event.target.getBoundingClientRect();
                postingDataDiv.style.position = 'absolute';
                postingDataDiv.style.top = `${buttonRect.bottom + window.scrollY}px`;
                postingDataDiv.style.left = `${buttonRect.left + window.scrollX}px`;
                postingDataDiv.style.display = 'block';
            } catch (error) {
                console.error("Fetch error:", error);
                document.getElementById('posting-data').innerText = `Error: ${error.message}`;
            }
        }
    </script>
</body>


<!-- Testing static data:
<body>
    <h4>From database</h4>
    <button onclick="fetchDBPosting('Martha', event)">Martha (DB)</button>
    <button onclick="fetchDBPosting('Wayne', event)">Wayne (DB)</button>
    <div id="posting-data">Click a button to see recipes</div>
    <script>
        async function fetchDBPosting(posterName, event) {
            const apiUrl = `http://127.0.0.1:8887/api/posting/read/${posterName}`; // Ensure correct API port
            await fetchData(apiUrl, posterName, event);
        }
        async function fetchData(apiUrl, posterName, event) {
            try {
                const response = await fetch(apiUrl);
                if (!response.ok) {
                    throw new Error(`Could not fetch data for ${posterName}`);
                }
                const data = await response.json();
                const postingDataDiv = document.getElementById('posting-data');
                postingDataDiv.innerHTML = `
                    <h2>${data.name}</h2>
                    <p><strong>Dish:</strong> ${data.dish}</p>
                    <p><strong>Cuisine:</strong> ${data.cuisine}</p>
                    <p><strong>Link:</strong> <a href="${data.link}" target="_blank">${data.link}</a></p>
                    <p><strong>Comments:</strong> ${data.comments}</p>
                `;
                const buttonRect = event.target.getBoundingClientRect();
                postingDataDiv.style.position = 'absolute';
                postingDataDiv.style.top = `${buttonRect.bottom + window.scrollY}px`;
                postingDataDiv.style.left = `${buttonRect.left + window.scrollX}px`;
                postingDataDiv.style.display = 'block';
            } catch (error) {
                document.getElementById('posting-data').innerText = `Error: ${error.message}`;
                document.getElementById('posting-data').style.display = 'block';
            }
        }
    </script>
</body> -->



<!-- Testing static data:
<body>
    <h4>From database</h4>
    <button onclick="fetchDBPosting('Martha', event)">Martha (DB)</button>
    <button onclick="fetchDBPosting('Wayne', event)">Wayne (DB)</button>
    <div id="posting-data">Click a button to see recipes</div>
    <script>
        async function fetchDBPosting(posterName, event) {
            const apiUrl = `http://127.0.0.1:8887/api/posting/read/${posterName}`; // Ensure correct API port
            await fetchData(apiUrl, posterName, event);
        }
        async function fetchData(apiUrl, posterName, event) {
            try {
                const response = await fetch(apiUrl);
                if (!response.ok) {
                    throw new Error(`Could not fetch data for ${posterName}`);
                }
                const data = await response.json();
                const postingDataDiv = document.getElementById('posting-data');
                postingDataDiv.innerHTML = `
                    <h2>${data.name}</h2>
                    <p><strong>Dish:</strong> ${data.dish}</p>
                    <p><strong>Cuisine:</strong> ${data.cuisine}</p>
                    <p><strong>Link:</strong> <a href="${data.link}" target="_blank">${data.link}</a></p>
                    <p><strong>Comments:</strong> ${data.comments}</p>
                `;
                const buttonRect = event.target.getBoundingClientRect();
                postingDataDiv.style.position = 'absolute';
                postingDataDiv.style.top = `${buttonRect.bottom + window.scrollY}px`;
                postingDataDiv.style.left = `${buttonRect.left + window.scrollX}px`;
                postingDataDiv.style.display = 'block';
            } catch (error) {
                document.getElementById('posting-data').innerText = `Error: ${error.message}`;
                document.getElementById('posting-data').style.display = 'block';
            }
        }
    </script>
</body> -->
