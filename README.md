<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pure Math Practice Game</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            align-items: center;
            background-color: #f0f0f0;
            margin: 0;
            padding: 20px;
        }
        #game-container {
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
            text-align: center;
            max-width: 600px;
            width: 100%;
        }
        #question {
            font-size: 1.5em;
            margin-bottom: 20px;
        }
        .option {
            display: block;
            margin: 10px auto;
            padding: 10px;
            width: 80%;
            background-color: #007bff;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1em;
        }
        .option:hover {
            background-color: #0056b3;
        }
        #feedback {
            margin-top: 20px;
            font-size: 1.2em;
        }
        #score {
            margin-top: 10px;
            font-size: 1.2em;
        }
        #next-btn {
            margin-top: 20px;
            padding: 10px 20px;
            background-color: #28a745;
            color: white;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        #next-btn:hover {
            background-color: #218838;
        }
    </style>
</head>
<body>
    <div id="game-container">
        <h1>Pure Math Practice Game</h1>
        <div id="score">Score: 0</div>
        <div id="question"></div>
        <div id="options"></div>
        <div id="feedback"></div>
        <button id="next-btn" style="display: none;">Next Question</button>
    </div>

    <script>
        let score = 0;
        let currentQuestion = null;

        const questions = [
            {
                question: "Solve for x: 2x + 3 = 11",
                options: ["4", "5", "6", "7"],
                correct: "4"
            },
            {
                question: "What is the area of a circle with radius 5? (Use π ≈ 3.14)",
                options: ["78.5", "31.4", "15.7", "25"],
                correct: "78.5"
            },
            {
                question: "Find the derivative of f(x) = 3x²",
                options: ["6x", "3x", "x²", "6x²"],
                correct: "6x"
            },
            {
                question: "Solve for y: y/3 - 2 = 4",
                options: ["6", "12", "18", "9"],
                correct: "18"
            },
            {
                question: "What is the slope of the line y = 2x + 3?",
                options: ["2", "3", "1", "-2"],
                correct: "2"
            }
        ];

        function getRandomQuestion() {
            const index = Math.floor(Math.random() * questions.length);
            return questions[index];
        }

        function displayQuestion() {
            currentQuestion = getRandomQuestion();
            document.getElementById("question").textContent = currentQuestion.question;
            const optionsDiv = document.getElementById("options");
            optionsDiv.innerHTML = "";
            currentQuestion.options.forEach(option => {
                const button = document.createElement("button");
                button.textContent = option;
                button.className = "option";
                button.onclick = () => checkAnswer(option);
                optionsDiv.appendChild(button);
            });
            document.getElementById("feedback").textContent = "";
            document.getElementById("next-btn").style.display = "none";
        }

        function checkAnswer(selected) {
            const feedback = document.getElementById("feedback");
            if (selected === currentQuestion.correct) {
                score += 10;
                feedback.textContent = "Correct! Well done!";
                feedback.style.color = "green";
            } else {
                feedback.textContent = `Incorrect. The correct answer is ${currentQuestion.correct}.`;
                feedback.style.color = "red";
            }
            document.getElementById("score").textContent = `Score: ${score}`;
            document.querySelectorAll(".option").forEach(button => button.disabled = true);
            document.getElementById("next-btn").style.display = "block";
        }

        document.getElementById("next-btn").onclick = displayQuestion;

        // Start the game
        displayQuestion();
    </script>
</body>
</html>
