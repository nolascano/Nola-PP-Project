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
        }
        h1 {
            color: #ff6347; /* Tomato red color */
            text-align: center; /* Center-align text */
        }
        button {
            background-color: #4caf50; /* Green background */
            color: white; /* White text */
            border: none;
            padding: 10px 20px;
            text-align: center;
            font-size: 16px;
            cursor: pointer;
        }
        button:hover {
            background-color: #45a049; /* Darker green on hover */
        }
        #message {
            text-align: center;
            margin-top: 20px;
            font-size: 18px;
            color: #333;
        }
    </style>
</head>
<body>
    <h1>Welcome to My Quiz Website</h1>
    <button id="myButton">Click Me!</button>
    <p id="message"></p>

    <!-- JavaScript to handle button click -->
    <script>
        document.getElementById('myButton').addEventListener('click', function() {
            document.getElementById('message').textContent = 'Button clicked!';
        });
    </script>
</body>
</html>
