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
        .question-container {
            margin: 20px auto;
            text-align: center;
        }
        .timer {
            font-size: 20px;
            color: #333;
            margin-bottom: 10px;
        }
        .quiz-image {
            width: 100px;
            height: auto;
            margin: 10px;
            display: inline-block;
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
        <button onclick="startQuiz('sensory', 1)">Level 1</button>
        <button onclick="startQuiz('sensory', 2)">Level 2</button>
        <button onclick="startQuiz('sensory', 3)">Level 3</button>
    </div>
    <div id="working" class="level-buttons hidden">
        <h2>Working Memory Quizzes</h2>
        <button onclick="startQuiz('working', 1)">Level 1</button>
        <button onclick="startQuiz('working', 2)">Level 2</button>
        <button onclick="startQuiz('working', 3)">Level 3</button>
    </div>
    <div id="longterm" class="level-buttons hidden">
        <h2>Long Term Memory Quizzes</h2>
        <button onclick="startQuiz('longterm', 1)">Level 1</button>
        <button onclick="startQuiz('longterm', 2)">Level 2</button>
        <button onclick="startQuiz('longterm', 3)">Level 3</button>
    </div>
    <div id="shortterm" class="level-buttons hidden">
        <h2>Short Term Memory Quizzes</h2>
        <button onclick="startQuiz('shortterm', 1)">Level 1</button>
        <button onclick="startQuiz('shortterm', 2)">Level 2</button>
        <button onclick="startQuiz('shortterm', 3)">Level 3</button>
    </div>

    <div id="quiz" class="hidden">
        <div class="question-container">
            <div class="timer" id="timer">20</div>
            <div id="imageContainer"></div>
            <p id="questionText"></p>
            <div id="options"></div>
        </div>
    </div>

    <p id="message"></p>

    <!-- JavaScript to handle button clicks and quiz functionality -->
    <script>
        var score = 0;
        var timerInterval;

        function showLevels(category) {
            // Hide all level buttons
            var levels = document.querySelectorAll('.level-buttons');
            levels.forEach(function(level) {
                level.classList.add('hidden');
            });

            // Show the selected category's level buttons
            document.getElementById(category).classList.remove('hidden');
        }

        function startQuiz(category, level) {
            // Hide all level buttons
            var levels = document.querySelectorAll('.level-buttons');
            levels.forEach(function(level) {
                level.classList.add('hidden');
            });

            // Show quiz container
            document.getElementById('quiz').classList.remove('hidden');

            // Load specific quiz based on category and level
            if (category === 'shortterm' && level === 1) {
                loadShortTermMemoryQuiz();
            }
        }

        function loadShortTermMemoryQuiz() {
            const images = [
                'cat.jpg', 'dog.jpg', 'pencil.jpg', 'house.jpg', 
                'rose.jpg', 'bike.jpg', 'basketball.jpg', 'tennis.jpg'
            ];

            const imageContainer = document.getElementById('imageContainer');
            imageContainer.innerHTML = ''; // Clear previous images

            images.forEach(image => {
                const img = document.createElement('img');
                img.src = 'images/' + image; // Assuming images are in the 'images' folder
                img.className = 'quiz-image';
                img.id = image;
                imageContainer.appendChild(img);
            });

            // Start the timer
            startTimer();

            // Choose a random image to hide after 20 seconds
            setTimeout(() => {
                hideRandomImage(images);
            }, 20000);
        }

        function startTimer() {
            let time = 20; // Timer duration in seconds
            document.getElementById('timer').textContent = time;

            timerInterval = setInterval(() => {
                time--;
                document.getElementById('timer').textContent = time;
                if (time <= 0) {
                    clearInterval(timerInterval);
                    document.getElementById('message').textContent = 'Time is up!';
                    // Handle time up scenario (e.g., reveal the answer)
                }
            }, 1000);
        }

        function hideRandomImage(images) {
            const randomIndex = Math.floor(Math.random() * images.length);
            const imageToHide = images[randomIndex];
            document.getElementById(imageToHide).style.display = 'none';

            // Set the question text
            document.getElementById('questionText').textContent = 'Which image is missing?';

            // Create answer options
            let optionsHtml = '';
            images.forEach(image => {
                const option = image.replace('.jpg', '').replace(/_/g, ' ');
                optionsHtml += `<button onclick="checkAnswer('${image}', '${imageToHide}')">${option}</button>`;
            });
            document.getElementById('options').innerHTML = optionsHtml;
        }

        function checkAnswer(selectedAnswer, missingImage) {
            clearInterval(timerInterval); // Stop the timer
            const correctAnswer = missingImage.replace('.jpg', '').replace(/_/g, ' ');
            if (selectedAnswer === correctAnswer) {
                score++;
                document.getElementById('message').textContent = 'Correct answer!';
            } else {
                document.getElementById('message').textContent = 'Incorrect answer!';
            }
            // Load next question or finish quiz
        }
    </script>
</body>
</html>
