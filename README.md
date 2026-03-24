# task-33
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Advanced Web App</title>

<style>
/* ===== GLOBAL STYLES ===== */
body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: #0f172a;
    color: white;
}

.container {
    padding: 20px;
}

/* ===== NAVBAR ===== */
nav {
    display: flex;
    justify-content: space-between;
    background: #1e293b;
    padding: 15px;
}

/* ===== CAROUSEL ===== */
.carousel {
    position: relative;
    max-width: 100%;
    height: 300px;
    overflow: hidden;
    margin: 20px 0;
}

.carousel img {
    width: 100%;
    height: 300px;
    object-fit: cover;
}

/* ===== QUIZ ===== */
.quiz-box {
    background: #1e293b;
    padding: 20px;
    border-radius: 10px;
}

button {
    padding: 10px;
    margin: 5px;
    border: none;
    background: #22c55e;
    color: white;
    cursor: pointer;
}

button:hover {
    background: #16a34a;
}

/* ===== API BOX ===== */
.api-box {
    margin-top: 20px;
    padding: 15px;
    background: #1e293b;
    border-radius: 10px;
}

/* ===== RESPONSIVE ===== */
@media (max-width: 768px) {
    nav {
        flex-direction: column;
        text-align: center;
    }

    .carousel {
        height: 200px;
    }
}
</style>
</head>

<body>

<nav>
    <h2>Advanced App</h2>
    <p>Task 3 - ApexPlanet</p>
</nav>

<div class="container">

    <!-- CAROUSEL -->
    <div class="carousel">
        <img id="carouselImage" src="https://picsum.photos/800/300?1">
    </div>

    <!-- QUIZ -->
    <div class="quiz-box">
        <h3 id="question">Question here</h3>
        <div id="answers"></div>
        <p id="score"></p>
    </div>

    <!-- API -->
    <div class="api-box">
        <h3>Random Joke (API)</h3>
        <p id="joke">Click button to load joke</p>
        <button onclick="getJoke()">Get Joke</button>
    </div>

</div>

<script>
/* ===== IMAGE CAROUSEL ===== */
const images = [
    "https://picsum.photos/800/300?1",
    "https://picsum.photos/800/300?2",
    "https://picsum.photos/800/300?3"
];

let index = 0;

setInterval(() => {
    index = (index + 1) % images.length;
    document.getElementById("carouselImage").src = images[index];
}, 3000);


/* ===== QUIZ APP ===== */
const quizData = [
    {
        question: "What is HTML?",
        options: ["Programming Language", "Markup Language", "Database"],
        answer: "Markup Language"
    },
    {
        question: "What is CSS used for?",
        options: ["Styling", "Logic", "Database"],
        answer: "Styling"
    }
];

let current = 0;
let score = 0;

function loadQuestion() {
    let q = quizData[current];
    document.getElementById("question").innerText = q.question;

    let answersHTML = "";
    q.options.forEach(option => {
        answersHTML += `<button onclick="checkAnswer('${option}')">${option}</button>`;
    });

    document.getElementById("answers").innerHTML = answersHTML;
}

function checkAnswer(selected) {
    if (selected === quizData[current].answer) {
        score++;
    }

    current++;

    if (current < quizData.length) {
        loadQuestion();
    } else {
        document.getElementById("question").innerText = "Quiz Finished!";
        document.getElementById("answers").innerHTML = "";
        document.getElementById("score").innerText = "Score: " + score;
    }
}

loadQuestion();


/* ===== API FETCH ===== */
async function getJoke() {
    let response = await fetch("https://official-joke-api.appspot.com/random_joke");
    let data = await response.json();
    document.getElementById("joke").innerText = data.setup + " - " + data.punchline;
}
</script>

</body>
</html>
