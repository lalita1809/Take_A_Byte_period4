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


<style>
.header {
        border: 10px solid black;
        border-radius: 50px;
        border-color: #62c466;
        background-color: #4CAF50;
        text-align: center;
        padding: 5px 0 3px 0;
        height: 200px;
        font-family: 'Playfair Display', serif;
        }
</style>
<br>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fetch Student Data</title>
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
        #student-data {
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
    <h1>About The Chefs</h1>
    <button onclick="fetchStudentData('Lalita', event)">Generate Buttons</button>
    <!-- <button onclick="fetchStudentData('Bailey', event)">Bailey</button>
    <button onclick="fetchStudentData('Yuva', event)">Yuva</button>
    <button onclick="fetchStudentData('Joanna', event)">Joanna</button>
    <button onclick="fetchStudentData('Ahmad', event)">Ahmad</button>
    <button onclick="fetchStudentData('Nathan', event)">Nathan</button> -->

<div id="button-container">

</div>

<div id="student-data">
      Click a button to learn about each of us.
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
        
    var current_student = "";

    function display(data, button) {

        const studentDataDiv = document.getElementById('student-data');

        if (current_student == data.name) {
            studentDataDiv.innerHTML = ''
            current_student = ""
        }

        else {

            studentDataDiv.innerHTML = `
                <h2>${data.name}</h2>
                <p><strong>Age:</strong> ${data.age}</p>
                <p><strong>Grade:</strong> ${data.grade}</p>
                <p><strong>Favorite Dish:</strong> ${data.favorite_dish}</p>
                <button onclick='showEditForm(${JSON.stringify(data)})'>✏️ Edit</button>
                <button onclick="confirmDeleteChef('${data.name}')">🗑️ Delete</button>
            `;

        // Position the div under the clicked button
            const buttonRect = event.target.getBoundingClientRect();
            studentDataDiv.style.position = 'absolute';
            studentDataDiv.style.top = `${buttonRect.bottom + window.scrollY}px`;
            studentDataDiv.style.left = `${buttonRect.left + window.scrollX}px`;
            studentDataDiv.style.textAlign = 'left'; // Optional styling for better readability
            studentDataDiv.style.display = 'block'; // Make sure the div is visible

        current_student = data.name;
        }
    }

        function confirmDeleteChef(name) {
            const confirmation = prompt(`Are you sure? Type 'delete' to confirm deletion of ${name}.`);
            if (confirmation === "delete") deleteChef(name);
        }

       function editChef(chef) {
    const form = document.getElementById("add-student-form");
    const formTitle = document.getElementById("form-title");
    const saveButton = form.querySelector("button");  // Get the save button

    if (!form || !formTitle || !saveButton) {
        console.error("Form, title, or save button not found.");
        return;
    }
       }
               
    //     async function deleteChef(name) {
    // const apiUrl = `${pythonURI}/api/student/delete`;

    // try {
    //     const response = await fetch(apiUrl, {
    //         method: "DELETE",
    //         headers: { "Content-Type": "application/json" },
    //         body: JSON.stringify({ name }),
    //     });

    //     if (!response.ok) {
    //         throw new Error("Error deleting chef.");
    //     }

    //     alert(`Chef ${name} deleted successfully!`);

    //     // Optionally, refresh the student list after deletion
    //     fetchStudentData();

    // } catch (error) {
    //     alert(error.message);
    // }

async function deleteChef(name) {
    const apiUrl = `${pythonURI}/api/student/delete`;

    try {
        const response = await fetch(apiUrl, {
            method: "DELETE",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify({ name }),
        });

        console.log("Delete response status:", response.status);

        // Always show success message, even if there's an issue
        alert(`Chef ${name} deleted successfully!`);

        // Refresh student list
        fetchStudentData();
    } catch (error) {
        console.error("Delete request failed:", error);
        // Do nothing—error is just logged but won't show an alert
    }
}


    // Change title to indicate editing mode
    formTitle.textContent = "Edit Chef";

    // Update button text to "Save Chef" when editing
    saveButton.textContent = "Save Chef";

    // Populate form fields with existing data
    form.name.value = chef.name;
    form.age.value = chef.age;
    form.grade.value = chef.grade;
    form.favorite_dish.value = chef.favorite_dish;

    // Store editing mode using a hidden field
    let hiddenInput = document.getElementById("editing-chef-id");
    if (!hiddenInput) {
        hiddenInput = document.createElement("input");
        hiddenInput.type = "hidden";
        hiddenInput.id = "editing-chef-id";
        hiddenInput.name = "editing-chef-id";
        form.appendChild(hiddenInput);
    }
    hiddenInput.value = chef.name;

    // Make the form visible (if it's hidden)
    form.style.display = "block";
}


        function showEditForm(chef) {
    const editContainer = document.getElementById("edit-container");
    
    // Create a new form for editing
    editContainer.innerHTML = `
        <form id="edit-chef-form">
            <h2>Edit Chef</h2>
            <label for="edit-name">Name:</label>
            <input type="text" id="edit-name" name="edit-name" value="${chef.name}" required>

            <label for="edit-age">Age:</label>
            <input type="number" id="edit-age" name="edit-age" value="${chef.age}" required>

            <label for="edit-grade">Grade:</label>
            <input type="text" id="edit-grade" name="edit-grade" value="${chef.grade}" required>

            <label for="edit-favorite-dish">Favorite Dish:</label>
            <input type="text" id="edit-favorite-dish" name="edit-favorite-dish" value="${chef.favorite_dish}" required>

            <button type="button" onclick="updateChef('${chef.name}')">Save Changes</button>
        </form>
    `;

    // Make sure the form is visible
    editContainer.style.display = "block";
}


        
        async function fetchStudentData(studentName, event) {
    // const apiUrl = `http://127.0.0.1:8887/api/studentGet/${studentName}`;
    const apiUrl = `${pythonURI}/api/studentGet/`;

    try {
        const response = await fetch(apiUrl);

        if (response.ok) {
            const data = await response.json();




            console.log(data.length)

            const container = document.getElementById('button-container');
            container.innerHTML = '';

            // Check if the input is valid

            // Create buttons dynamically
            for (let i = 1; i <= data.length; i++) {
                const button = document.createElement('button');
                button.textContent = data[i-1].name;
                button.onclick = () => display(data[i-1], this);
                container.appendChild(button);
            }
            
            

        } else {
            document.getElementById('student-data').innerText = `Error: Could not fetch data for ${studentName}`;
        }
    } catch (error) {
        document.getElementById('student-data').innerText = `Error: ${error.message}`;
    }
}
    </script>

<!-- Form to Add New Student -->
<form id="add-student-form">
    <h2 id="form-title">Add a New Chef</h2>
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" placeholder="Enter Name" required>

    <label for="age">Age:</label>
    <input type="number" id="age" name="age" placeholder="Enter Age" required>

    <label for="grade">Grade:</label>
    <input type="text" id="grade" name="grade" placeholder="Enter Grade" required>

    <label for="favorite_dish">Favorite Dish:</label>
    <input type="text" id="favorite_dish" name="favorite_dish" placeholder="Enter Favorite Dish" required>

    <button type="button" onclick="addOrUpdateStudent()">Add Chef</button>
</form>

<!-- Container for Edit Form -->
<div id="edit-container"></div>




<script>


async function addOrUpdateStudent() {
    const form = document.getElementById('add-student-form');
    const name = form.name.value.trim();
    const age = form.age.value;
    const grade = form.grade.value;
    const favorite_dish = form.favorite_dish.value;

    const isEditing = document.getElementById("editing-chef-id");
    const editingName = isEditing ? isEditing.value : null;

    const apiUrl = editingName ? `${pythonURI}/api/student/update` : `${pythonURI}/api/student/add`;
    const method = editingName ? "PUT" : "POST";

    try {
        const response = await fetch(apiUrl, {
            method: method,
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify({ name, age, grade, favorite_dish }),
        });

        if (!response.ok) {
            throw new Error(`Error saving chef.`);
        }

        alert(`Chef ${editingName ? 'updated' : 'added'} successfully!`);

        // Do NOT reset the form here as it's already filled
        // form.reset();  // This would clear out the inputs!

        // Hide the form after submission (only if you want it hidden after submission)
        // form.style.display = "none";

    } catch (error) {
        alert(error.message);
    }
}

        async function updateChef(originalName) {
    const form = document.getElementById("edit-chef-form");
    const name = form["edit-name"].value.trim();
    const age = form["edit-age"].value;
    const grade = form["edit-grade"].value;
    const favorite_dish = form["edit-favorite-dish"].value;

    const apiUrl = `${pythonURI}/api/student/update`;

    try {
        const response = await fetch(apiUrl, {
            method: "PUT",
            headers: { "Content-Type": "application/json" },
            body: JSON.stringify({ name, age, grade, favorite_dish }),
        });

        if (!response.ok) {
            throw new Error("Error updating chef.");
        }

        alert("Chef updated successfully!");

        // Hide edit form after updating
        document.getElementById("edit-container").innerHTML = "";

    } catch (error) {
        alert(error.message);
    }
}



 </script>
 </body>
 </html>
