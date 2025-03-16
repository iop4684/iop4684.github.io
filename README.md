# iop4684.github.io
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Career Choices Visual Novel</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            background-color: #f3f4f6;
        }
        .container {
            background: white;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
            width: 90%;
            max-width: 500px;
            text-align: center;
        }
        h1 {
            font-size: 1.5rem;
            margin-bottom: 20px;
            color: #333;
        }
        .question {
            margin-bottom: 20px;
        }
        .options button {
            background-color: #007bff;
            color: white;
            border: none;
            padding: 10px 20px;
            margin: 5px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 1rem;
        }
        .options button:hover {
            background-color: #0056b3;
        }
        .result {
            font-size: 1.25rem;
            margin-top: 20px;
            color: #444;
        }
        .restart {
            margin-top: 20px;
            background-color: #28a745;
            color: white;
            padding: 10px 20px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        .restart:hover {
            background-color: #1e7e34;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Career Choices</h1>
        <div id="game">
            <div class="question" id="question"></div>
            <div class="options" id="options"></div>
        </div>
        <div class="result" id="result" style="display: none;"></div>
        <button class="restart" id="restart" style="display: none;">Restart</button>
    </div>

    <script>
        const stages = [
            {
                question: "At 5-6 years old, what excites you the most?",
                options: [
                    { text: "Drawing and creating art", value: "A" },
                    { text: "Building things and solving puzzles", value: "B" },
                    { text: "Playing pretend or storytelling", value: "C" },
                ],
            },
            {
                question: "As a teenager, what do you enjoy the most?",
                options: [
                    { text: "Exploring science and technology", value: "1" },
                    { text: "Helping and connecting with people", value: "2" },
                    { text: "Performing or expressing yourself creatively", value: "3" },
                ],
            },
        ];

        const careerPaths = {
            "A1": "Graphic Designer",
            "A2": "Art Therapist",
            "A3": "Actor",
            "B1": "Engineer",
            "B2": "Teacher",
            "B3": "Architect",
            "C1": "Scientist",
            "C2": "Counselor",
            "C3": "Writer",
        };

        let stageIndex = 0;
        let answerCombination = "";

        const questionElement = document.getElementById("question");
        const optionsElement = document.getElementById("options");
        const resultElement = document.getElementById("result");
        const restartButton = document.getElementById("restart");

        function renderStage() {
            const stage = stages[stageIndex];
            questionElement.textContent = stage.question;
            optionsElement.innerHTML = "";
            stage.options.forEach((option) => {
                const button = document.createElement("button");
                button.textContent = option.text;
                button.onclick = () => {
                    answerCombination += option.value;
                    stageIndex++;
                    if (stageIndex < stages.length) {
                        renderStage();
                    } else {
                        showResult();
                    }
                };
                optionsElement.appendChild(button);
            });
        }

        function showResult() {
            const career = careerPaths[answerCombination];
            resultElement.textContent = `Your career choice is: ${career}`;
            resultElement.style.display = "block";
            optionsElement.style.display = "none";
            questionElement.style.display = "none";
            restartButton.style.display = "block";
        }

        restartButton.onclick = () => {
            stageIndex = 0;
            answerCombination = "";
            resultElement.style.display = "none";
            optionsElement.style.display = "flex";
            questionElement.style.display = "block";
            restartButton.style.display = "none";
            renderStage();
        };

        renderStage();
    </script>
</body>
</html>
