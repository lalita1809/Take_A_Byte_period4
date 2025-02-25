---
layout: post
title: Feedback
search_exclude: true
hide: true
permalink: /navigation/feedback
---
<div style="text-align: center;" class="header">
<h3>Give us your feedback! 💬 Share your thoughts about the recipes and post reviews! 🍴</h3>

<br>

<style>
.header {
        border: 10px solid black;
        border-radius: 50px;
        border-color: #F5E1E7;
        background-color: green;
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
    <title>Feedback Page</title>
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
        #feedback-container {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin-top: 20px;
        }
        #feedback-data {
            display: none;
            border: 1px solid #ddd;
            border-radius: 5px;
            background: #f9f9f9;
            padding: 10px;
            text-align: center;
            max-width: 400px;
        }
    </style>
</head>
<body>
    <h1>Feedback Page</h1>
    <button onclick="fetchFeedbackData(event)">Show Feedback</button>
    
<div id="feedback-container"></div>

<div id="feedback-data">
        Click on feedback to view details.
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

        async function fetchFeedbackData(event) {
          ;
            
            try {
                const apiUrl = (pythonURI + '/api/feedback/getAll')
                const response = await fetch(apiUrl, {
                    method: 'GET', 
                    headers: {
                        'Authorization': `Bearer ${localStorage.getItem('jwt')}`
                    }
                });

                if (response.ok) {
                    const data = await response.json();
                    const container = document.getElementById('feedback-container');
                    container.innerHTML = '';

                    // Create feedback buttons dynamically
                    data.forEach((feedback) => {
                        const button = document.createElement('button');
                        button.textContent = `${feedback.recipe}: ${feedback.written_feedback.substring(0, 30)}...`;
                        button.onclick = () => displayFeedbackDetails(feedback);
                        container.appendChild(button);
                    });
                } else {
                    alert('Failed to load feedback');
                }
            } catch (error) {
                alert(`Error: ${error.message}`);
            }
        }

        function displayFeedbackDetails(feedback) {
            const feedbackDataDiv = document.getElementById('feedback-data');
            feedbackDataDiv.style.display = 'block';
            feedbackDataDiv.innerHTML = `
                <h3>${feedback.recipe}</h3>
                <p><strong>Feedback:</strong> ${feedback.written_feedback}</p>
                <p><strong>Name:</strong> ${feedback.name}</p>
                <p><strong>Cuisine:</strong> ${feedback.cuisine}</p>
                <p><strong>Thumbs Up:</strong> ${feedback.thumbs_up}</p>
                <p><strong>Thumbs Down:</strong> ${feedback.thumbs_down}</p>
                <button onclick="deleteFeedback('${feedback.name}')">Delete Feedback</button>
                <button onclick="editFeedback('${feedback.name}', '${feedback.written_feedback}')">Edit Feedback</button>
            `;
        }

        async function deleteFeedback(feedbackId) {
            try {
                const response = await fetch(pythonURI + '/api/feedback/delete', {
                    method: 'DELETE',
                    headers: {
                        'Content-Type': 'application/json',
                        'Authorization': `Bearer ${localStorage.getItem('jwt')}`
                    },
                    body: JSON.stringify({ name: feedbackId })  // Changed to send name instead of id
                });

                if (response.ok) {
                    alert('Feedback deleted successfully!');
                    fetchFeedbackData();
                } else {
                    const errorMessage = await response.text();
                    alert(`Error deleting feedback: ${errorMessage}`);
                }
            } catch (error) {
                alert(`Error: ${error.message}`);
            }
        }

        async function editFeedback(feedbackId, oldContent) {
            const newContent = prompt('Edit your feedback:', oldContent);
            if (newContent) {
                try {
                    const response = await fetch(pythonURI + '/api/feedback/update', {
                        method: 'PUT',
                        headers: {
                            'Content-Type': 'application/json',
                            'Authorization': `Bearer ${localStorage.getItem('jwt')}`
                        },
                        body: JSON.stringify({ 
                            name: feedbackId,  // Changed to send name instead of id
                            written_feedback: newContent 
                        })
                    });

                    if (response.ok) {
                        alert('Feedback updated successfully!');
                        fetchFeedbackData();
                    } else {
                        alert('Error updating feedback');
                    }
                } catch (error) {
                    alert(`Error: ${error.message}`);
                }
            }
        }
</script>

 <!-- Form to Add New Feedback -->
<form id="add-feedback-form">
        <h2>Submit Your Feedback</h2>
        <label for="name">Your Name:</label>
        <input type="text" id="name" name="name" placeholder="Enter your name" required>

<label for="cuisine">Cuisine:</label>
        <input type="text" id="cuisine" name="cuisine" placeholder="Enter the cuisine" required>

<label for="recipe">Recipe Name:</label>
        <input type="text" id="recipe" name="recipe" placeholder="Enter the recipe name" required>

<label for="thumbs_up">Thumbs Up:</label>
        <input type="number" id="thumbs_up" name="thumbs_up" placeholder="Thumbs up" required>

<label for="thumbs_down">Thumbs Down:</label>
        <input type="number" id="thumbs_down" name="thumbs_down" placeholder="Thumbs down" required>

<label for="written_feedback">Written Feedback:</label>
        <textarea id="written_feedback" name="written_feedback" placeholder="Enter your feedback" required></textarea>

<button type="button" onclick="addFeedback()">Submit Feedback</button>
    </form>

<script>
    async function addFeedback() {
        const form = document.getElementById('add-feedback-form');
        const name = form.name.value.trim();
        const cuisine = form.cuisine.value.trim();
        const recipe = form.recipe.value.trim();
        const thumbs_up = parseInt(form.thumbs_up.value.trim());  // Convert to number
        const thumbs_down = parseInt(form.thumbs_down.value.trim());  // Convert to number
        const written_feedback = form.written_feedback.value.trim();

        if (!name || !cuisine || !recipe || isNaN(thumbs_up) || isNaN(thumbs_down) || !written_feedback) {
            alert('Please fill all fields correctly');
            return;
        }

        try {
            const apiUrl = pythonURI + '/api/feedback/addFeedback';
            const response = await fetch(apiUrl, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `Bearer ${localStorage.getItem('jwt')}`
                },
                body: JSON.stringify({
                    name: name,
                    cuisine: cuisine,
                    recipe: recipe,
                    thumbs_up: thumbs_up,
                    thumbs_down: thumbs_down,
                    written_feedback: written_feedback
                })
            });

            if (response.ok) {
                alert('Feedback submitted successfully!');
                form.reset();
                fetchFeedbackData(); // Refresh feedback list
            } else {
                const errorData = await response.text();
                alert(`Failed to submit feedback: ${errorData}`);
            }
        } catch (error) {
            alert(`Error: ${error.message}`);
        }
    }

    // Ensure function is available globally
    window.addEventListener("load", function() {
        window.addFeedback = addFeedback;
    });
</script>
</body>
</html>