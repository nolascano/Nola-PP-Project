<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Memory Psychology Quiz Website</title>
    <style>
        body {
            background-color: #f0f8ff; /* Light blue background */
            font-family: Arial, sans-serif; /* Font style */
            text-align: center;
        }
        h1 {
            color: #ff6347; /* Tomato red color */
            margin-top: 20px;
        }
        .container {
            margin: 20px auto;
            width: 80%;
        }
        button {
            background-color: #4caf50; /* Green background */
            color: white; /* White text */
            border: none;
            padding: 10px 20px;
            text-align: center;
            font-size: 16px;
            cursor: pointer;
            margin: 10px;
        }
        button:hover {
            background-color: #45a049; /* Darker green on hover */
        }
        .hidden {
            display: none;
        }
        .level-buttons {
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Welcome to My Quiz Website</h1>

    <div class="container">
        <!-- Main category buttons -->
        <button onclick="showLevels('sensory')">Sensory Memory Quizzes</button>
        <button onclick="showLevels('working')">Working Memory Quizzes</button>
        <button onclick="showLevels('longterm')">Long Term Memory Quizzes</button>
        <button onclick="showLevels('shortterm')">Short Term Memory Quizzes</button>
    </div>

    <!-- Level buttons for each category -->
    <div id="sensory" class="level-buttons hidden">
        <h2>Sensory Memory Quizzes</h2>
        <button onclick="showMessage('sensory', 1)">Level 1</button>
        <button onclick="showMessage('sensory', 2)">Level 2</button>
        <button onclick="showMessage('sensory', 3)">Level 3</button>
    </div>
    <div id="working" class="level-buttons hidden">
        <h2>Working Memory Quizzes</h2>
        <button onclick="showMessage('working', 1)">Level 1</button>
        <button onclick="showMessage('working', 2)">Level 2</button>
        <button onclick="showMessage('working', 3)">Level 3</button>
    </div>
    <div id="longterm" class="level-buttons hidden">
        <h2>Long Term Memory Quizzes</h2>
        <button onclick="showMessage('longterm', 1)">Level 1</button>
        <button onclick="showMessage('longterm', 2)">Level 2</button>
        <button onclick="showMessage('longterm', 3)">Level 3</button>
    </div>
    <div id="shortterm" class="level-buttons hidden">
        <h2>Short Term Memory Quizzes</h2>
        <button onclick="showMessage('shortterm', 1)">Level 1</button>
        <button onclick="showMessage('shortterm', 2)">Level 2</button>
        <button onclick="showMessage('shortterm', 3)">Level 3</button>
    </div>

    <p id="message"></p>

    <!-- JavaScript to handle button clicks -->
    <script>
        function showLevels(category) {
            // Hide all level buttons
            var levels = document.querySelectorAll('.level-buttons');
            levels.forEach(function(level) {
                level.classList.add('hidden');
            });

            // Show the selected category's level buttons
            document.getElementById(category).classList.remove('hidden');
        }

        function showMessage(category, level) {
            document.getElementById('message').textContent = 'You selected ' + category + ' Quiz Level ' + level + '!';
        }
    </script>
</body>
</html>
