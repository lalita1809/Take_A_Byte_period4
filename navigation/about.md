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
            background-color: #2c3e50;
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        .container {
            width: 90%;
            max-width: 1000px;
            margin: 0 auto;
            padding: 40px 80px;
            background: linear-gradient(145deg, #e8e8e8, #d4d4d4);
            border-radius: 20px;
            position: relative;
            border: 2px solid #ccc;
            box-shadow: 
                0 0 0 2px rgba(255,255,255,0.1),
                0 8px 32px rgba(0,0,0,0.3);
        }
        /* Fridge Handle */
        .container::before {
            content: '';
            position: absolute;
            right: 20px;
            top: 50%;
            transform: translateY(-50%);
            width: 40px;
            height: 70%;
            background: linear-gradient(90deg, #888, #999);
            border-radius: 8px;
            box-shadow: 
                inset -2px 0 5px rgba(0,0,0,0.3),
                2px 0 5px rgba(255,255,255,0.5);
        }
        /* Fridge Logo */
        .container::after {
            content: 'FRIDGE';
            position: absolute;
            left: 40px;
            top: 20px;
            font-size: 14px;
            color: #666;
            letter-spacing: 2px;
            font-weight: bold;
        }
        /* Metallic Texture */
        .metallic-overlay {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: 
                repeating-linear-gradient(
                    45deg,
                    rgba(255,255,255,0.05) 0px,
                    rgba(255,255,255,0.05) 1px,
                    transparent 1px,
                    transparent 3px
                );
            border-radius: 20px;
            pointer-events: none;
        }
        .form-group {
            margin-bottom: 20px;
            background: rgba(255, 255, 255, 0.9);
            padding: 15px;
            border-radius: 10px;
            box-shadow: 
                inset 0 2px 8px rgba(0,0,0,0.1),
                0 1px 2px rgba(255,255,255,0.3);
            backdrop-filter: blur(5px);
        }
        input {
            width: 100%;
            padding: 12px;
            margin: 8px 0;
            border-radius: 8px;
            border: 2px solid #e0e0e0;
            transition: all 0.3s ease;
        }
        input:focus {
            border-color: #4CAF50;
            outline: none;
            box-shadow: 0 0 8px rgba(76,175,80,0.2);
        }
        button {
            width: 100%;
            padding: 12px;
            margin: 8px 0;
            border-radius: 8px;
            border: none;
            background-color: #4CAF50;
            color: white;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: bold;
        }
        button:hover {
            background-color: #45a049;
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(76,175,80,0.2);
        }
        table {
            width: 100%;
            border-collapse: separate;
            border-spacing: 0;
            margin-top: 25px;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 
                inset 0 2px 8px rgba(0,0,0,0.1),
                0 1px 2px rgba(255,255,255,0.3);
            backdrop-filter: blur(5px);
        }
        th, td {
            padding: 15px;
            text-align: left;
            border-bottom: 1px solid #eee;
        }
        th {
            background-color: #2c3e50;
            font-weight: bold;
            color: white;
            text-transform: uppercase;
            letter-spacing: 1px;
            font-size: 0.9em;
        }
        tr:last-child td {
            border-bottom: none;
        }
        tr:hover {
            background-color: #f5f5f5;
        }
        td button {
            width: auto;
            padding: 8px 16px;
            margin: 0 4px;
        }
        td button:first-child {
            background-color: #3498db;
        }
        td button:first-child:hover {
            background-color: #2980b9;
        }
        td button:last-child {
            background-color: #e74c3c;
        }
        td button:last-child:hover {
            background-color: #c0392b;
        }
        
        /* Custom Modal Styles */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            z-index: 1000;
            opacity: 0;
            transition: opacity 0.3s ease-in-out;
        }
        
        .modal.show {
            display: flex;
            opacity: 1;
        }
        
        .modal-content {
            background: white;
            padding: 30px;
            border-radius: 15px;
            width: 90%;
            max-width: 400px;
            margin: auto;
            text-align: center;
            position: relative;
            transform: scale(0.7);
            transition: transform 0.3s ease-in-out;
            box-shadow: 0 5px 30px rgba(0, 0, 0, 0.3);
        }
        
        .modal.show .modal-content {
            transform: scale(1);
        }
        
        .modal h2 {
            color: #2c3e50;
            margin-bottom: 20px;
        }
        
        .modal p {
            color: #666;
            margin-bottom: 30px;
        }
        
        .modal-buttons {
            display: flex;
            justify-content: center;
            gap: 15px;
        }
        
        .modal-button {
            padding: 10px 25px;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            transition: all 0.3s ease;
        }
        
        .confirm-button {
            background-color: #e74c3c;
            color: white;
        }
        
        .cancel-button {
            background-color: #95a5a6;
            color: white;
        }
        
        .modal-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0,0,0,0.15);
        }
        
        /* Edit Modal Styles */
        .edit-modal-content {
            background: white;
            padding: 30px;
            border-radius: 15px;
            width: 90%;
            max-width: 400px;
            margin: auto;
            text-align: center;
            position: relative;
            transform: scale(0.7);
            transition: transform 0.3s ease-in-out;
            box-shadow: 0 5px 30px rgba(0, 0, 0, 0.3);
        }
        
        .modal.show .edit-modal-content {
            transform: scale(1);
        }
        
        .edit-input {
            width: 100%;
            padding: 12px;
            margin: 15px 0;
            border-radius: 8px;
            border: 2px solid #e0e0e0;
            font-size: 16px;
        }
        
        .edit-button {
            background-color: #3498db;
            color: white;
        }
        
        .edit-button:hover {
            background-color: #2980b9;
        }
        /* Temperature Display */
        .temp-display {
            position: absolute;
            top: 20px;
            right: 100px;
            background: #000;
            color: #00ff00;
            padding: 5px 10px;
            border-radius: 4px;
            font-family: 'Digital', monospace;
            font-size: 14px;
            box-shadow: 
                inset 0 0 5px rgba(0,255,0,0.5),
                0 0 10px rgba(0,0,0,0.2);
        }
    </style>
</head>
<body>
<div class="container">
    <div class="metallic-overlay"></div>
    <div class="temp-display">38°F</div>
    <h1>Fridge</h1>
    
    <!-- Add Byte Bot Section -->
    <div class="form-group" style="
        margin-bottom: 30px;
        border: 2px solid #3498db;
        border-radius: 15px;
        padding: 20px;
        background: rgba(255, 255, 255, 0.8);
        box-shadow: 0 4px 15px rgba(52, 152, 219, 0.2);
    ">
        <h2 style="
            color: #2c3e50;
            margin-top: 0;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 2px solid #3498db;
        ">Ask for recommendations</h2>
        <div id="chat-box" style="
            height: 300px;
            overflow-y: auto;
            background: rgba(255, 255, 255, 0.95);
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 15px;
            border: 1px solid #e0e0e0;
            box-shadow: inset 0 2px 8px rgba(0,0,0,0.05);
        "></div>
        <div style="display: flex; gap: 10px;">
            <input 
                type="text" 
                id="question" 
                placeholder="Ask byte bot a question..."
                style="
                    flex-grow: 1;
                    margin: 0;
                    border: 2px solid #3498db;
                    transition: all 0.3s ease;
                "
            >
            <button 
                id="sendButton"
                style="
                    width: auto;
                    margin: 0;
                    background-color: #3498db;
                    padding: 12px 25px;
                    font-weight: bold;
                    letter-spacing: 0.5px;
                "
            >Ask</button>
        </div>
    </div>

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

<!-- Add Modal HTML -->
<div id="deleteModal" class="modal">
    <div class="modal-content">
        <h2>Confirm Deletion</h2>
        <p>Are you sure you want to remove this item from your fridge?</p>
        <div class="modal-buttons">
            <button class="modal-button cancel-button" onclick="closeModal()">Cancel</button>
            <button class="modal-button confirm-button" onclick="confirmDelete()">Delete</button>
        </div>
    </div>
</div>

<!-- Add Edit Modal HTML -->
<div id="editModal" class="modal">
    <div class="edit-modal-content">
        <h2>Edit Quantity</h2>
        <p>Update the quantity for <span id="editItemName"></span></p>
        <input type="number" id="editQuantityInput" class="edit-input" min="1">
        <div class="modal-buttons">
            <button class="modal-button cancel-button" onclick="closeEditModal()">Cancel</button>
            <button class="modal-button edit-button" onclick="confirmEdit()">Update</button>
        </div>
    </div>
</div>

<!-- Add the new Add Modal HTML right after the other modals -->
<div id="addModal" class="modal">
    <div class="modal-content">
        <h2>Confirm Addition</h2>
        <p>Are you sure you want to add this item to your fridge?</p>
        <div id="addItemDetails"></div>
        <div class="modal-buttons">
            <button class="modal-button cancel-button" onclick="closeAddModal()">Cancel</button>
            <button class="modal-button confirm-button" onclick="confirmAdd()">Add</button>
        </div>
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

// Add grocery - modified to use modal
document.getElementById('addFridgeBtn').addEventListener('click', () => {
    const grocery = document.getElementById('grocery').value;
    const quantity = parseInt(document.getElementById('quantity').value);
    
    if (!grocery || !quantity) {
        alert("Please fill in both fields");
        return;
    }
    
    const details = document.getElementById('addItemDetails');
    details.innerHTML = `<p>Item: ${grocery}<br>Quantity: ${quantity}</p>`;
    
    const modal = document.getElementById('addModal');
    modal.classList.add('show');
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
    if (!Array.isArray(data)) {
        console.error("Data is not an array:", data);
        return;
    }
    data.forEach(Grocery => {
        const row = document.createElement('tr');
        row.innerHTML = `
            <td>${Grocery.id}</td>
            <td>${Grocery.grocery}</td>
            <td>${Grocery.quantity}</td>
            <td>
                <button onclick="showEditModal(${Grocery.id}, '${Grocery.grocery}', ${Grocery.quantity})">Edit</button>
                <button onclick="showModal(${Grocery.id})">Delete</button>
            </td>
        `;
        tableBody.appendChild(row);
    });
}

let deleteItemId = null;
let editItemId = null;
let editItemName = null;

function showModal(id) {
    deleteItemId = id;
    const modal = document.getElementById('deleteModal');
    modal.classList.add('show');
}

function closeModal() {
    const modal = document.getElementById('deleteModal');
    modal.classList.remove('show');
    deleteItemId = null;
}

function confirmDelete() {
    if (deleteItemId !== null) {
        performDelete(deleteItemId);
    }
    closeModal();
}

async function performDelete(id) {
    try {
        const response = await fetch(pythonURI + `/fridge/delete`, {
            method: 'DELETE',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ id })
        });
        
        if (response.ok) {
            fetchGrocerys();
        } else {
            alert("Failed to delete item.");
        }
    } catch (err) {
        console.error("Delete error:", err);
        alert("Error deleting item.");
    }
}

function showEditModal(id, grocery, currentQuantity) {
    editItemId = id;
    editItemName = grocery;
    const modal = document.getElementById('editModal');
    const quantityInput = document.getElementById('editQuantityInput');
    const itemNameSpan = document.getElementById('editItemName');
    
    itemNameSpan.textContent = grocery;
    quantityInput.value = currentQuantity;
    modal.classList.add('show');
}

function closeEditModal() {
    const modal = document.getElementById('editModal');
    modal.classList.remove('show');
    editItemId = null;
    editItemName = null;
}

async function confirmEdit() {
    if (editItemId !== null) {
        const newQuantity = parseInt(document.getElementById('editQuantityInput').value);
        try {
            const response = await fetch(pythonURI + `/fridge/update`, {
                method: 'PUT',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ id: editItemId, quantity: newQuantity })
            });
            
            if (response.ok) {
                fetchGrocerys();
            } else {
                alert("Failed to update item.");
            }
        } catch (err) {
            console.error("Update error:", err);
            alert("Error updating item.");
        }
    }
    closeEditModal();
}

function closeAddModal() {
    const modal = document.getElementById('addModal');
    modal.classList.remove('show');
}

async function confirmAdd() {
    const grocery = document.getElementById('grocery').value;
    const quantity = parseInt(document.getElementById('quantity').value);

    try {
        const response = await fetch(pythonURI + `/fridge/add`, { 
            method: 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ grocery, quantity })
        });
        if (response.ok) {
            alert("Grocery added!");
            fetchGrocerys();
            document.getElementById('grocery').value = '';
            document.getElementById('quantity').value = '';
        } else {
            alert("Failed to add Grocery.");
        }
    } catch (err) {
        console.error(err);
    }
    closeAddModal();
}

// Fetch Grocerys on page load
fetchGrocerys();

// Byte Bot Logic
async function sendQuestion(question) {
    if (!question.trim()) {
        alert("Please enter a question!");
        return;
    }

    const chatBox = document.getElementById("chat-box");

    // Display user's question
    chatBox.innerHTML += `
        <div style="margin-bottom: 15px; background: #f5f5f5; padding: 10px; border-radius: 8px;">
            <strong style="color: #2c3e50;">You:</strong> 
            <span style="color: #2c3e50;">${question}</span>
        </div>`;

    try {
        const response = await fetch(`${pythonURI}/api/ai/help`, {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify({ question: question })
        });

        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }

        const data = await response.json();

        chatBox.innerHTML += `
            <div style="margin-bottom: 15px; background: #3498db; padding: 10px; border-radius: 8px; color: white;">
                <strong>byte bot:</strong> ${data.response || "No response received"}
            </div>`;
    } catch (error) {
        console.error('Error:', error);
        chatBox.innerHTML += `
            <div style="margin-bottom: 15px; background: #e74c3c; padding: 10px; border-radius: 8px; color: white;">
                <strong>Error:</strong> ${error.message}
            </div>`;
    }

    // Clear input and scroll to bottom
    document.getElementById("question").value = "";
    chatBox.scrollTop = chatBox.scrollHeight;
}

// Add event listeners for byte bot when the document is loaded
document.addEventListener('DOMContentLoaded', function() {
    const questionInput = document.getElementById("question");
    const sendButton = document.getElementById("sendButton");

    if (questionInput && sendButton) {
        // Enter key event listener
        questionInput.addEventListener("keypress", function(event) {
            if (event.key === "Enter") {
                event.preventDefault();
                sendQuestion(this.value);
            }
        });

        // Button click event listener
        sendButton.addEventListener("click", function() {
            const question = questionInput.value;
            sendQuestion(question);
        });
    }
});
</script>
</body>
</html>