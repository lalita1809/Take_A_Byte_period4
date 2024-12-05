---
layout: post
title: Dishpire
search_exclude: true
hide: true
menu: nav/home.html
---

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Random Cuisine Spinner</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f4f4f9;
        }
        .wheel-container {
            position: relative;
            width: 300px;
            height: 300px;
            border-radius: 50%;
            border: 5px solid #000;
            overflow: hidden;
        }
        .wheel {
            width: 100%;
            height: 100%;
            position: absolute;
            transform-origin: center;
            transition: transform 5s cubic-bezier(0.33, 1, 0.68, 1);
        }
        .slice {
            position: absolute;
            width: 50%;
            height: 50%;
            background-color: #eee;
            border: 2px solid #ccc;
            box-sizing: border-box;
            clip-path: polygon(0% 0%, 100% 0%, 50% 100%);
            transform-origin: 100% 100%;
        }
        .slice:nth-child(1) { background: #f94144; transform: rotate(0deg); }
        .slice:nth-child(2) { background: #f3722c; transform: rotate(60deg); }
        .slice:nth-child(3) { background: #f8961e; transform: rotate(120deg); }
        .slice:nth-child(4) { background: #f9c74f; transform: rotate(180deg); }
        .slice:nth-child(5) { background: #90be6d; transform: rotate(240deg); }
        .slice:nth-child(6) { background: #43aa8b; transform: rotate(300deg); }
        .pointer {
            position: absolute;
            top: -15px;
            left: 50%;
            width: 0;
            height: 0;
            border-left: 15px solid transparent;
            border-right: 15px solid transparent;
            border-bottom: 30px solid #000;
            transform: translateX(-50%);
            z-index: 1;
        }
        button {
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            background-color: #4caf50;
            color: white;
            border: none;
            border-radius: 5px;
        }
        button:disabled {
            background-color: #aaa;
            cursor: not-allowed;
        }
        #result {
            margin-top: 20px;
            font-size: 20px;
            font-weight: bold;
            color: #333;
        }
    </style>
</head>
<body>
    <div class="wheel-container">
        <div class="pointer"></div>
        <div class="wheel" id="wheel">
            <div class="slice">Cuisine 1</div>
            <div class="slice">Cuisine 2</div>
            <div class="slice">Cuisine 3</div>
            <div class="slice">Cuisine 4</div>
            <div class="slice">Cuisine 5</div>
            <div class="slice">Cuisine 6</div>
        </div>
    </div>
    <button id="spinButton" onclick="spinWheel()">Spin the Wheel</button>
    <div id="result"></div>

    <script>
        let currentRotation = 0; // Track the current rotation of the wheel
        const spinButton = document.getElementById('spinButton');
        const resultDiv = document.getElementById('result');

        function spinWheel() {
            // Disable the spin button
            spinButton.disabled = true;

            const wheel = document.getElementById('wheel');
            const randomRotations = Math.floor(Math.random() * 4) + 5; // Random number of rotations (5 to 8)
            const randomSlice = Math.floor(Math.random() * 360); // Random degree for the final position
            const totalRotation = randomRotations * 360 + randomSlice; // Total rotation amount

            currentRotation += totalRotation; // Increment the total rotation
            wheel.style.transform = `rotate(${currentRotation}deg)`;

            // Determine which slice is selected after the spin
            setTimeout(() => {
                spinButton.disabled = false;

                // Calculate the final rotation position
                const normalizedRotation = currentRotation % 360;
                const sliceIndex = Math.floor((360 - normalizedRotation) / 60) % 6;

                // Get the selected cuisine
                const cuisines = ["Cuisine 1", "Cuisine 2", "Cuisine 3", "Cuisine 4", "Cuisine 5", "Cuisine 6"];
                const selectedCuisine = cuisines[sliceIndex];

                // Display the result
                resultDiv.textContent = `The Spinner Chose: ${selectedCuisine}`;
            }, 5000); // Matches the transition duration (5s)
        }
    </script>
</body>
</html>

