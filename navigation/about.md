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
    <title>Fridge</title>
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
        table {
            width: 100%;
            border-collapse: collapse;
            margin-top: 20px;
        }
        th, td {
            border: 1px solid #ccc;
            padding: 8px;
            text-align: left;
        }
        th {
            background-color: #f2f2f2;
        }
    </style>
</head>
<body>
<div class="container">
    <h1>Fridge</h1>
    <div class="form-group">
        <label for="grocery">Grocery:</label>
        <input type="text" id="grocery" placeholder="e.g., chicken, garlic, lemon">
    </div>
    <div class="form-group">
        <label for="quantity">Quantity:</label>
        <input type="number" id="quantity" placeholder="Enter quantity">
    </div>
    <button id="addFridgeBtn">Add Grocery to Fridge</button>
    <div id="fridgeTableWrapper">
        <h2>Your Fridge</h2>
        <table>
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Grocery</th>
                    <th>Quantity</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody id="fridgeTableBody">
                <!-- Dynamic rows will be inserted here -->
            </tbody>
        </table>
    </div>
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

const API_URL = (pythonURI + "/api/fridge");

// Add grocery
document.getElementById('addFridgeBtn').addEventListener('click', async () => {
    const grocery = document.getElementById('grocery').value;
    const quantity = parseInt(document.getElementById('quantity').value);

    try {
        // const response = await fetch(`${API_URL}/add`, { 
        const response = await fetch(pythonURI + `/fridge/add`, { 
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ grocery, quantity })
        });
        if (response.ok) {
            alert("Grocery added!");
            fetchGrocerys();
        } else {
            alert("Failed to add Grocery.");
        }
    } catch (err) {
        console.error(err);
    }
});

// Fetch Grocerys
async function fetchGrocerys() {
    try {
        const response = await fetch(API_URL);
        if (response.ok) {
            const data = await response.json();
            renderTable(data);
        }
    } catch (err) {
        console.error(err);
    }
}

// Render table
function renderTable(data) {
    const tableBody = document.getElementById('fridgeTableBody');
    tableBody.innerHTML = '';
    data.forEach(Grocery => {
        const row = document.createElement('tr');
        row.innerHTML = `
            <td>${Grocery.id}</td>
            <td>${Grocery.grocery}</td>
            <td>${Grocery.quantity}</td>
            <td>
                <button onclick="updateGrocery(${Grocery.id}, '${Grocery.grocery}', ${Grocery.quantity})">Edit</button>
                <button onclick="deleteGrocery(${Grocery.id})">Delete</button>
            </td>
        `;
        tableBody.appendChild(row);
    });
}

// Update Grocery
async function updateGrocery(id, grocery, currentQuantity) {
    const newQuantity = prompt(`Update quantity for ${grocery}:`, currentQuantity);
    if (newQuantity !== null) {
        try {
            const response = await fetch(`${API_URL}/update`, {
                method: 'PUT',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ id, quantity: parseInt(newQuantity) })
            });
            if (response.ok) {
                alert("Grocery updated!");
                fetchGrocerys();
            }
        } catch (err) {
            console.error(err);
        }
    }
}

// Delete Grocery
async function deleteGrocery(id) {
    try {
        const response = await fetch(`${API_URL}/delete`, {
            method: 'DELETE',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ id })
        });
        if (response.ok) {
            alert("Grocery deleted!");
            fetchGrocerys();
        }
    } catch (err) {
        console.error(err);
    }
}

// Fetch Grocerys on page load
fetchGrocerys();
</script>
</body>
</html>
