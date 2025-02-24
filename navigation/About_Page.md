---
layout: post
title: About TAB!
search_exclude: true
hide: true
permalink: /navigation/about
---

<div style="text-align: center;" class="header">
<h3>Need a bite? Take A Byte! We are an online cookbook with recipies from different cuisines around the world 🌍️ </h3>

<br>
<html lang="en">
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
            position: absolute;
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
    <button onclick="fetchChefData()">Generate Chef List</button>
    <div id="button-container"></div>
    <div id="chef-data">Click a button to learn about each chef.</div>

    <form id="chef-form">
        <h2 id="form-title">Add a New Chef</h2>
        <input type="hidden" id="editing-chef" value="">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required>
        <label for="age">Age:</label>
        <input type="number" id="age" name="age" required>
        <label for="grade">Grade:</label>
        <input type="text" id="grade" name="grade" required>
        <label for="favorite_color">Favorite Color:</label>
        <input type="text" id="favorite_color" name="favorite_color" required>
        <button type="button" onclick="addOrUpdateChef()">Add Chef</button>
    </form>

    <script>
        var pythonURI = location.hostname.includes("localhost") || location.hostname.includes("127.0.0.1") ? "http://127.0.0.1:8887" : "https://takeabyte.stu.nighthawkcodingsociety.com";
        
        async function fetchChefData() {
            const apiUrl = `${pythonURI}/api/studentGet/`;
            try {
                const response = await fetch(apiUrl);
                if (!response.ok) throw new Error("Failed to fetch data");
                const data = await response.json();
                const container = document.getElementById('button-container');
                container.innerHTML = '';
                data.forEach(chef => {
                    const chefDiv = document.createElement('div');
                    chefDiv.innerHTML = `
                        <button onclick="displayChef(${chef.id})">${chef.name}</button>
                        <button onclick="editChef(${chef.id})">✏️</button>
                        <button onclick="confirmDeleteChef(${chef.id})">🗑️</button>
                    `;
                    container.appendChild(chefDiv);
                });
            } catch (error) {
                alert(`Error: ${error.message}`);
            }
        }

        function editChef(chefId) {
            fetch(`${pythonURI}/api/studentGet/${chefId}`)
                .then(res => res.json())
                .then(chef => {
                    document.getElementById("name").value = chef.name;
                    document.getElementById("age").value = chef.age;
                    document.getElementById("grade").value = chef.grade;
                    document.getElementById("favorite_color").value = chef.favorite_color;
                    document.getElementById("editing-chef").value = chef.id;
                    document.getElementById("form-title").textContent = "Edit Chef";
                });
        }

        function confirmDeleteChef(chefId) {
            const confirmation = prompt("Are you sure? Type 'delete' to confirm.");
            if (confirmation === "delete") deleteChef(chefId);
        }

        async function deleteChef(chefId) {
            try {
                await fetch(`${pythonURI}/api/student/delete`, {
                    method: 'DELETE',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify({ id: chefId })
                });
                alert("Chef deleted successfully");
                fetchChefData();
            } catch (error) {
                alert(`Error: ${error.message}`);
            }
        }

        async function addOrUpdateChef() {
            const form = document.getElementById('chef-form');
            const chefId = document.getElementById("editing-chef").value;
            const chefData = {
                name: form.name.value,
                age: form.age.value,
                grade: form.grade.value,
                favorite_color: form.favorite_color.value
            };
            const method = chefId ? 'PUT' : 'POST';
            const apiUrl = chefId ? `${pythonURI}/api/student/update` : `${pythonURI}/api/student/add`;
            if (chefId) chefData.id = chefId;
            
            try {
                await fetch(apiUrl, {
                    method: method,
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(chefData)
                });
                alert(`Chef ${chefId ? 'updated' : 'added'} successfully!`);
                form.reset();
                document.getElementById("form-title").textContent = "Add a New Chef";
                fetchChefData();
            } catch (error) {
                alert(`Error: ${error.message}`);
            }
        }
    </script>
</body>
</html>

