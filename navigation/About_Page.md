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
        border-color: #F5E1E7;
        background-color: pink;
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
            background-color: #007bff;
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
                <p><strong>Favorite Color:</strong> ${data.favorite_color}</p>
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
    <h2>Add a New Chef</h2>
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" placeholder="Enter Name" required>

    <label for="age">Age:</label>
    <input type="number" id="age" name="age" placeholder="Enter Age" required>

    <label for="grade">Grade:</label>
    <input type="text" id="grade" name="grade" placeholder="Enter Grade" required>

    <label for="favorite_color">Favorite Color:</label>
    <input type="text" id="favorite_color" name="favorite_color" placeholder="Enter Favorite Color" required>

    <button type="button" onclick="addOrUpdateStudent()">Add Chef</button>
</form>
<h2>Delete a Chef</h2>
<form id="delete-student-form">
  <label for="name">Name:</label>
  <input type="text" id="name" name="name" placeholder="Enter Name" required />

  <label for="age">Age:</label>
  <input type="number" id="age" name="age" placeholder="Enter Age" required />

  <label for="grade">Grade:</label>
  <input type="text" id="grade" name="grade" placeholder="Enter Grade" required />

  <label for="favorite_color">Favorite Color:</label>
  <input type="text" id="favorite_color" name="favorite_color" placeholder="Enter Favorite Color" required />

  <button type="button" onclick="deleteStudent()">Delete Student</button>
</form>


<script>

async function deleteStudent() {
  const form = document.getElementById('delete-student-form');
  const name = form.name.value.trim(); // Trim spaces to avoid mismatches
  const age = parseInt(form.age.value); // Convert age to number
  const grade = form.grade.value;
  const favorite_color = form.favorite_color.value;

  const getApiUrl = (pythonURI + `/api/studentGet/`); // API to fetch existing students
  const deleteApiUrl = (pythonURI + `/api/student/delete`); // API to delete a student

  try {
    // Fetch existing students
    const response = await fetch(getApiUrl);
    if (!response.ok) throw new Error('Failed to fetch student data.');

    const data = await response.json();

    // Find the student by name
    const student = data.find((student) => student.name.toLowerCase() === name.toLowerCase());

  //  if (!student) {
    //  alert(`Student with name "${name}" not found.`);
    //  return;
   // }

    // Check if the data matches
    if (student.age !== age || student.grade !== grade || student.favorite_color !== favorite_color) {
      alert(`Data mismatch. Please ensure the data matches the student information.`);
      return;
    }

    // Send DELETE request to delete the student
    const deleteResponse = await fetch(deleteApiUrl, {
      method: 'DELETE',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ name, age, grade, favorite_color }),
    });

    if (!deleteResponse.ok) {
      const errorData = await deleteResponse.json();
      throw new Error(`Error: ${errorData.message}`);
    }

    const responseData = await deleteResponse.json();
    alert(`Student ${responseData.name} deleted successfully!`);
    form.reset();

  } catch (error) {
    alert(`Error: ${error.message}`);
  }
}



async function addOrUpdateStudent() {
  const form = document.getElementById('add-student-form');
  const name = form.name.value.trim(); // Trim spaces to avoid mismatches
  const age = form.age.value;
  const grade = form.grade.value;
  const favorite_color = form.favorite_color.value;

  const getApiUrl = (pythonURI + `/api/studentGet/`); // API to fetch existing students
  const addApiUrl = (pythonURI + `/api/student/add`); // API to add a new student
  const updateApiUrl = (pythonURI + `/api/student/update`); // API to update an existing student

  try {
    // Fetch existing students
    const response = await fetch(getApiUrl);
    if (!response.ok) throw new Error('Failed to fetch student data.');

    const data = await response.json();

    // Check if the student already exists
    const existingStudent = data.find((student) => student.name.toLowerCase() === name.toLowerCase());

    const apiUrl = existingStudent ? updateApiUrl : addApiUrl; // Determine API endpoint
    const method = existingStudent ? 'PUT' : 'POST'; // Use PUT for updates, POST for new entries

    // Send request to add or update the student
    const saveResponse = await fetch(apiUrl, {
      method: method,
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ name, age, grade, favorite_color }),
    });

    if (!saveResponse.ok) {
      const errorData = await saveResponse.json();
      throw new Error(`Error: ${errorData.message}`);
    }

    const responseData = await saveResponse.json();
    alert(`Student ${responseData.name} ${existingStudent ? 'updated' : 'added'} successfully!`);
    form.reset();

  } catch (error) {
    alert(`Error: ${error.message}`);
  }
}


//   async function addStudent() {
//   const form = document.getElementById('add-student-form');
//   const name = form.name.value.trim(); // Trim spaces to avoid mismatches
//   const age = form.age.value;
//   const grade = form.grade.value;
//   const favorite_color = form.favorite_color.value;

//   const getApiUrl = `http://127.0.0.1:8887/api/studentGet/`; // API to fetch existing students
//   const addApiUrl = `http://127.0.0.1:8887/api/student/add`; // API to add a new student
//   const updateApiUrl = `http://127.0.0.1:8887/api/student/update`; // API to update an existing student

//   let data = [];

//   // Fetch existing students
//   try {
//     const response = await fetch(getApiUrl);
//     if (response.ok) {
//       data = await response.json(); // Assign the fetched data to the `data` variable
//     } else {
//       alert('Failed to fetch student data.');
//       return;
//     }
//   } catch (error) {
//     alert(`Error fetching student data: ${error.message}`);
//     return; // Exit early if fetching data fails
//   }

//   // Check if the student already exists
//   const existingStudent = data.find((student) => student.name.toLowerCase() === name.toLowerCase());

//   const apiUrl = existingStudent ? updateApiUrl : addApiUrl; // Determine the correct API URL
//   const method = existingStudent ? 'PUT' : 'POST'; // Use PUT for updates, POST for new entries

//   try {
//     const response = await fetch(apiUrl, {
//       method: method,
//       headers: {
//         'Content-Type': 'application/json',
//       },
//       body: JSON.stringify({ name, age, grade, favorite_color }),
//     });

//     if (response.ok) {
//       const responseData = await response.json();
//       alert(
//         `Student ${responseData.name} ${existingStudent ? 'updated' : 'added'} successfully!`
//       );
//       form.reset();
//     } else {
//       const errorData = await response.json();
//       alert(`Error: ${errorData.message}`);
//     }
//   } catch (error) {
//     alert(`Error: ${error.message}`);
//   }
// }

 </script>
 </body>
 </html>


