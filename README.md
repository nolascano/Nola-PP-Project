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
    <h1>Welcome to My Memory Psychology Quiz Website</h1>
    <div class="container">
        <button onclick="showCategory('short-term-memory')">Short Term Memory Quizzes</button>
        <button onclick="showCategory('working-memory')">Working Memory Quizzes</button>
        <button onclick="showCategory('long-term-memory')">Long Term Memory Quizzes</button>
        <button onclick="showCategory('sensory-memory')">Sensory Memory Quizzes</button>
    </div>

    <div id="short-term-memory" class="hidden">
        <h2>Short Term Memory Quizzes</h2>
        <div class="level-buttons">
            <button onclick="startQuiz()">Level 1</button>
            <!-- Add Level 2 and Level 3 buttons here if needed -->
        </div>
    </div>

    <div id="question-container" class="hidden">
        <div id="timer" class="timer">20</div>
        <div id="imageContainer"></div>
        <p id="questionText"></p>
        <div id="options"></div>
    </div>

    <script>
        function showCategory(category) {
            document.querySelectorAll('.container > button').forEach(button => {
                button.classList.toggle('hidden', button.textContent.toLowerCase() !== category.replace('-', ' '));
            });
        }

        function startQuiz() {
            const images = [
                'images/dog.jpg',
                'images/cat.jpg',
                'images/hat.jpg',
                'images/house.jpg',
                'images/tennis_ball.jpg',
                'images/basketball.jpg',
                'images/pencil.jpg'
            ];

            const imageContainer = document.getElementById('imageContainer');
            imageContainer.innerHTML = ''; // Clear previous images

            images.forEach(src => {
                const img = document.createElement('img');
                img.src = src;
                img.className = 'quiz-image';
                img.id = src;
                imageContainer.appendChild(img);
            });

            // Start the timer
            startTimer();

            // Choose a random image to hide after 20 seconds
            setTimeout(() => {
                hideRandomImage(images);
            }, 20000);

            // Hide other memory quiz options
            document.querySelectorAll('.container > button').forEach(button => {
                button.classList.add('hidden');
            });

            document.getElementById('short-term-memory').classList.add('hidden');
            document.getElementById('question-container').classList.remove('hidden');
        }

        function startTimer() {
            let time = 20;
            document.getElementById('timer').textContent = time;

            const timerInterval = setInterval(() => {
                time--;
                document.getElementById('timer').textContent = time;
                if (time <= 0) {
                    clearInterval(timerInterval);
                    document.getElementById('questionText').textContent = 'Time is up!';
                }
            }, 1000);
        }

        function hideRandomImage(images) {
            const randomIndex = Math.floor(Math.random() * images.length);
            const imageToHide = images[randomIndex];
            document.querySelector(`#imageContainer img[src="${imageToHide}"]`).style.display = 'none';

            // Set the question text
            document.getElementById('questionText').textContent = 'Which image is missing?';

            // Create answer options
            let optionsHtml = '';
            images.forEach(src => {
                const option = src.split('/').pop().split('.')[0];
                optionsHtml += `<button onclick="checkAnswer('${option}', '${imageToHide.split('/').pop().split('.')[0]}')">${option}</button>`;
            });
            document.getElementById('options').innerHTML = optionsHtml;
        }

        function checkAnswer(selectedAnswer, missingImage) {
            const correctAnswer = missingImage;
            if (selectedAnswer === correctAnswer) {
                alert('Correct answer!');
            } else {
                alert('Incorrect answer!');
            }

            // Show the quiz options again
            document.querySelectorAll('.container > button').forEach(button => {
                button.classList.remove('hidden');
            });
            document.getElementById('short-term-memory').classList.remove('hidden');
            document.getElementById('question-container').classList.add('hidden');
        }
    </script>
</body>
</html>
