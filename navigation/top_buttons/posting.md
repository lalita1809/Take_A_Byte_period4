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
        body {
            font-family: 'Poppins', sans-serif;
            background:rgb(146, 160, 219);
            margin: 20px;
            color: #333;
            display: flex;
            justify-content: center;
        }
        .container {
            max-width: 700px;
            width: 100%;
            padding: 20px;
            background:rgb(184, 204, 235);
            border-radius: 20px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
            text-align: center;
        }
        .post { border-bottom: 1px solid #ddd; padding: 10px 0; }
        h1, h2 {
            color:rgb(45, 53, 110);
            font-family: 'Pacifico', cursive;
            margin-bottom: 15px;
        }
        button {
            background-color:rgb(72, 70, 135);
            color: white;
            padding: 12px 18px;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease;
            font-size: 14px;
        }
        button:hover {
            transform: scale(1.05);
            background-color:rgb(169, 172, 230);
        }
        .delete-button {
            background-color:rgb(186, 108, 94);
        }
        .delete-button:hover {
            background-color:rgb(137, 60, 27);
        }
        .edit-button {
            background-color:rgb(168, 225, 168);
        }
        .edit-button:hover {
            background-color:rgb(103, 164, 133);
        }
        #all-posts-section {
            margin-top: 30px;
        }
        .edit-fields {
            display: none; 
        }
        .post a {
            color:rgb(38, 34, 87); /* Change to any color you prefer */
            font-size: 18px; /* Adjust size as needed */
            text-decoration: none;
            font-weight: bold;
            display: block;
            margin-top: 5px;
        }
        .post a:hover {
            text-decoration: underline;
            color:rgb(173, 173, 229); /* Change hover color */
        }
    </style>
</head>

<body>

<div class="container">
    <h1>All Posts</h1>
    <div id="all-posts-section">
        <h2>Recipes</h2>
        <div id="postsContainer"></div>
    </div>
<br>
<button onclick="window.location.href='https://lalita1809.github.io/flocker_frontend_period4/'">Back to Home</button>


<script>
    var pythonURI;
    if (location.hostname === "localhost") {
        pythonURI = "http://localhost:8887";
    } else if (location.hostname === "127.0.0.1") {
        pythonURI = "http://127.0.0.1:8887";
    } else {
        pythonURI = "https://takeabyte.stu.nighthawkcodingsociety.com";
    }

    async function fetchPosts() {
        try {
            const response = await fetch(pythonURI + "/api/posting/reading");
            const posts = await response.json();
            const postsContainer = document.getElementById("postsContainer");
            postsContainer.innerHTML = "";

            if (!posts || posts.length === 0) {
                postsContainer.innerHTML = "<p>No recipes posted yet.</p>";
                return;
            }

            posts.forEach(post => {
                const postElement = document.createElement("div");
                postElement.classList.add("post");
                postElement.innerHTML = `
                    <p><strong>Name:</strong> ${post.name}</p>
                    <p><strong>Dish:</strong> <span class="post-dish">${post.dish}</span></p>
                    <p><strong>Cuisine:</strong> <span class="post-cuisine">${post.cuisine}</span></p>
                    <p><strong>Link:</strong> <a class="post-link" href="${post.link}" target="_blank">${post.link}</a></p>
                    <p><strong>Comments:</strong> <span class="post-comments">${post.comments}</span></p>
                    <div class="edit-fields">
                        <input type="text" class="edit-dish" value="${post.dish}">
                        <input type="text" class="edit-cuisine" value="${post.cuisine}">
                        <input type="url" class="edit-link" value="${post.link}">
                        <textarea class="edit-comments">${post.comments}</textarea>
                        <button onclick="saveEdit('${post.name}', this)">Save</button>
                    </div>
                    <button class="edit-button" onclick="toggleEdit(this)">Edit</button>
                    <button class="delete-button" onclick="deletePost('${post.name}')">Delete</button>
                `;
                postsContainer.appendChild(postElement);
            });
        } catch (error) {
            console.error("Error fetching posts:", error);
        }
    }

    function toggleEdit(button) {
        const postElement = button.parentElement;
        const displayFields = postElement.querySelectorAll(".post-dish, .post-cuisine, .post-link, .post-comments");
        const editFields = postElement.querySelector(".edit-fields");
        
        displayFields.forEach(field => field.style.display = "none");
        editFields.style.display = "block";
    }

    async function saveEdit(name, button) {
        const postElement = button.parentElement.parentElement;
        const updatedPost = {
            name: name,
            dish: postElement.querySelector(".edit-dish").value,
            cuisine: postElement.querySelector(".edit-cuisine").value,
            link: postElement.querySelector(".edit-link").value,
            comments: postElement.querySelector(".edit-comments").value
        };

        try {
            const response = await fetch(pythonURI + `/api/posting/update/`, {
                method: "PUT",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify(updatedPost)
            });

            if (response.ok) {
                alert("Recipe updated successfully!");
                fetchPosts();
            } else {
                alert("Error updating recipe.");
            }
        } catch (error) {
            console.error("Error:", error);
        }
    }

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
    fetchPosts();
</script>













<!-- 
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
</head> -->



<!-- 
<body>
    <h4>Static users</h4>
    <button onclick="fetchStaticPosting('martha', event)">Martha</button>
    <button onclick="fetchStaticPosting('wayne', event)">Wayne</button>
    <!-- <div id="posting-data" style="display: none;">
    </div>
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
