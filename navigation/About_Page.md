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
  <img src="{{site.baseurl}}/images/about/about_cuisine.png" alt="food food food"/>


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

<!DOCTYPE html>
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
            margin-top: 20px;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            background: #f9f9f9;
            max-width: 400px;
            text-align: center;
        }
    </style>
</head>
<body>
    <h1>About The Chefs</h1>
    <button onclick="fetchStudentData('lalita')">Lalita</button>
    <button onclick="fetchStudentData('bailey')">Bailey</button>
    <button onclick="fetchStudentData('yuva')">Yuva</button>
    <button onclick="fetchStudentData('joanna')">Joanna</button>
    <button onclick="fetchStudentData('ahmad')">Ahmad</button>
    <button onclick="fetchStudentData('nathan')">Nathan</button>

    <div id="student-data">
      Click a button to learn about each of us.
    </div>

    <script>
        async function fetchStudentData(studentName) {
            const apiUrl = `http://127.0.0.1:8887/api/student/${studentName}`;

            try {
                const response = await fetch(apiUrl);

                if (response.ok) {
                    const data = await response.json();

                    // Display data on the page
                    document.getElementById('student-data').innerHTML = `
                        <h2>${data.name}</h2>
                        <p><strong>Age:</strong> ${data.age}</p>
                        <p><strong>Grade:</strong> ${data.grade}</p>
                        <p><strong>Favorite Color:</strong> ${data.favorite_color}</p>
                    `;
                } else {
                    document.getElementById('student-data').innerText = `Error: Could not fetch data for ${studentName}`;
                }
            } catch (error) {
                document.getElementById('student-data').innerText = `Error: ${error.message}`;
            }
        }
    </script>
</body>
</html>

