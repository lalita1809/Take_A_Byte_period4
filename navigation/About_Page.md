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
            padding: 10px 15px;
            font-size: 16px;
            margin: 5px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .edit-btn {
            background-color: #ffc107;
        }
        .delete-btn {
            background-color: #dc3545;
            color: white;
        }
        #chef-list {
            margin-top: 20px;
            width: 300px;
        }
        .chef-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            margin: 5px 0;
        }
        #delete-confirmation {
            display: none;
            position: fixed;
            background: white;
            padding: 20px;
            border: 2px solid black;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            text-align: center;
        }
    </style>
</head>
<body>
    <h1>Chef Management</h1>
    
    <form id="chef-form">
        <h2 id="form-title">Add a New Chef</h2>
        <input type="hidden" id="edit-mode" value="">
        <label for="name">Name:</label>
        <input type="text" id="name" required>
        <label for="age">Age:</label>
        <input type="number" id="age" required>
        <label for="grade">Grade:</label>
        <input type="text" id="grade" required>
        <label for="favorite_color">Favorite Color:</label>
        <input type="text" id="favorite_color" required>
        <button type="button" onclick="addOrUpdateChef()">Submit</button>
    </form>
    
    <div id="chef-list"></div>
    
    <div id="delete-confirmation">
        <p>Are you sure? Type "delete" to confirm:</p>
        <input type="text" id="delete-input">
        <button onclick="confirmDelete()">Confirm</button>
        <button onclick="closeDeletePopup()">Cancel</button>
    </div>
    
    <script>
        let chefs = [];
        let chefToDelete = null;

        function addOrUpdateChef() {
            const name = document.getElementById('name').value;
            const age = document.getElementById('age').value;
            const grade = document.getElementById('grade').value;
            const favoriteColor = document.getElementById('favorite_color').value;
            const editMode = document.getElementById('edit-mode').value;

            if (editMode) {
                const chef = chefs.find(c => c.name === editMode);
                chef.age = age;
                chef.grade = grade;
                chef.favoriteColor = favoriteColor;
                document.getElementById('form-title').textContent = 'Add a New Chef';
                document.getElementById('edit-mode').value = '';
            } else {
                chefs.push({ name, age, grade, favoriteColor });
            }

            document.getElementById('chef-form').reset();
            renderChefs();
        }

        function renderChefs() {
            const list = document.getElementById('chef-list');
            list.innerHTML = '';
            chefs.forEach(chef => {
                const div = document.createElement('div');
                div.classList.add('chef-item');
                div.innerHTML = `
                    <span>${chef.name}</span>
                    <button class="edit-btn" onclick="editChef('${chef.name}')">✏️</button>
                    <button class="delete-btn" onclick="showDeletePopup('${chef.name}')">🗑️</button>
                `;
                list.appendChild(div);
            });
        }

        function editChef(name) {
            const chef = chefs.find(c => c.name === name);
            document.getElementById('name').value = chef.name;
            document.getElementById('age').value = chef.age;
            document.getElementById('grade').value = chef.grade;
            document.getElementById('favorite_color').value = chef.favoriteColor;
            document.getElementById('form-title').textContent = 'Edit a Chef';
            document.getElementById('edit-mode').value = chef.name;
        }

        function showDeletePopup(name) {
            chefToDelete = name;
            document.getElementById('delete-confirmation').style.display = 'block';
        }

        function confirmDelete() {
            const input = document.getElementById('delete-input').value;
            if (input.toLowerCase() === 'delete') {
                chefs = chefs.filter(c => c.name !== chefToDelete);
                chefToDelete = null;
                document.getElementById('delete-confirmation').style.display = 'none';
                document.getElementById('delete-input').value = '';
                renderChefs();
            } else {
                alert('Incorrect input. Type "delete" to confirm.');
            }
        }

        function closeDeletePopup() {
            document.getElementById('delete-confirmation').style.display = 'none';
            chefToDelete = null;
        }
    </script>
</body>
</html>
