---
layout: post
title: About TAB!
search_exclude: true
hide: true
permalink: /navigation/about
---

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Chef Management</title>
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
            background-color: #4CAF50;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        button:hover {
            background-color: #0056b3;
        }
        #chef-data {
            display: none;
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
    <h1>About The Chefs</h1>
    <button onclick="fetchChefData()">Generate Chefs</button>

    <div id="button-container"></div>
    <div id="chef-data"></div>

    <form id="chef-form">
        <h2 id="form-title">Add a New Chef</h2>
        <input type="hidden" id="editing-chef-id">
        <label for="name">Name:</label>
        <input type="text" id="name" required>
        
        <label for="age">Age:</label>
        <input type="number" id="age" required>
        
        <label for="grade">Grade:</label>
        <input type="text" id="grade" required>
        
        <label for="favorite_color">Favorite Color:</label>
        <input type="text" id="favorite_color" required>
        
        <button type="button" onclick="addOrUpdateChef()">Add Chef</button>
    </form>

    <script>
        var pythonURI = location.hostname.includes("localhost") || location.hostname.includes("127.0.0.1")
            ? "http://127.0.0.1:8887"
            : "https://takeabyte.stu.nighthawkcodingsociety.com";

        async function fetchChefData() {
            try {
                const response = await fetch(`${pythonURI}/api/studentGet/`);
                if (!response.ok) throw new Error("Failed to fetch chefs.");
                const data = await response.json();
                const container = document.getElementById("button-container");
                container.innerHTML = "";
                data.forEach(chef => {
                    const button = document.createElement("button");
                    button.textContent = chef.name;
                    button.onclick = () => displayChef(chef);
                    container.appendChild(button);
                });
            } catch (error) {
                console.error(error);
            }
        }

        function displayChef(chef) {
            const chefDataDiv = document.getElementById("chef-data");
            chefDataDiv.innerHTML = `
                <h2>${chef.name}</h2>
                <p><strong>Age:</strong> ${chef.age}</p>
                <p><strong>Grade:</strong> ${chef.grade}</p>
                <p><strong>Favorite Color:</strong> ${chef.favorite_color}</p>
                <button onclick="editChef(${JSON.stringify(chef)})">✏️ Edit</button>
                <button onclick="confirmDeleteChef('${chef.name}')">🗑️ Delete</button>
            `;
            chefDataDiv.style.display = "block";
        }

        function editChef(chef) {
            document.getElementById("form-title").textContent = "Edit Chef";
            document.getElementById("name").value = chef.name;
            document.getElementById("age").value = chef.age;
            document.getElementById("grade").value = chef.grade;
            document.getElementById("favorite_color").value = chef.favorite_color;
        }

        function confirmDeleteChef(name) {
            const confirmation = prompt(`Are you sure? Type 'delete' to confirm deletion of ${name}.`);
            if (confirmation === "delete") deleteChef(name);
        }

        async function deleteChef(name) {
            try {
                const response = await fetch(`${pythonURI}/api/student/delete`, {
                    method: "DELETE",
                    headers: { "Content-Type": "application/json" },
                    body: JSON.stringify({ name })
                });
                if (!response.ok) throw new Error("Failed to delete chef.");
                alert("Chef deleted successfully!");
                fetchChefData();
            } catch (error) {
                alert(error.message);
            }
        }

        async function addOrUpdateChef() {
            const name = document.getElementById("name").value.trim();
            const age = document.getElementById("age").value;
            const grade = document.getElementById("grade").value;
            const favorite_color = document.getElementById("favorite_color").value;
            const editingChefId = document.getElementById("editing-chef-id").value;
            
            const apiUrl = editingChefId ? `${pythonURI}/api/student/update` : `${pythonURI}/api/student/add`;
            const method = editingChefId ? "PUT" : "POST";
            
            try {
                const response = await fetch(getApiUrl);
                const data = await response.json();
                const existingChef = data.find(chef => chef.name.toLowerCase() === name.toLowerCase());
                
                const apiUrl = existingChef ? updateApiUrl : addApiUrl;
                const method = existingChef ? "PUT" : "POST";
                
                const saveResponse = await fetch(apiUrl, {
                    method,
                    headers: { "Content-Type": "application/json" },
                    body: JSON.stringify({ name, age, grade, favorite_color })
                });
                
                if (!saveResponse.ok) throw new Error("Failed to save chef.");
                alert("Chef successfully saved!");
                fetchChefData();
            } catch (error) {
                alert(error.message);
            }
        }
    </script>
</body>


