
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Квіз на 20 питань</title>
<style>
    body {
        font-family: Arial, sans-serif;
        background-color: #f0f0f0;
        text-align: center;
    }
    .quiz-container {
        max-width: 600px;
        margin: 0 auto;
        padding: 20px;
        background-color: #fff;
        border-radius: 8px;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    }
    .question {
        font-size: 18px;
        font-weight: bold;
        margin-bottom: 20px;
    }
    .options {
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
    }
    .option-btn {
        background-color: #4CAF50;
        color: white;
        border: none;
        padding: 10px 20px;
        margin: 10px;
        cursor: pointer;
        border-radius: 5px;
        font-size: 16px;
        transition: background-color 0.3s ease;
    }
    .option-btn:hover {
        background-color: #45a049;
    }
    .next-btn {
        background-color: #007BFF;
        color: white;
        border: none;
        padding: 10px 20px;
        margin-top: 20px;
        cursor: pointer;
        border-radius: 5px;
        font-size: 16px;
        transition: background-color 0.3s ease;
    }
    .next-btn:hover {
        background-color: #0056b3;
    }
    .start-btn {
        background-color: #28a745;
        color: white;
        border: none;
        padding: 15px 30px;
        cursor: pointer;
        border-radius: 5px;
        font-size: 18px;
        transition: background-color 0.3s ease;
        margin-top: 20px;
    }
    .start-btn:hover {
        background-color: #218838;
    }
    .title-container img {
        max-width: 100%;
        height: auto;
        border-radius: 8px;
    }
    .correct {
        background-color: #4CAF50;
    }
    .incorrect {
        background-color: #f44336;
    }
</style>
</head>
<body>
<div class="quiz-container" id="titleContainer">
    <h1>Ласкаво просимо до квізу!</h1>
    <img src="https://th.bing.com/th/id/OIP.tRLXleKq9eFGroobtBDMyQHaE8?rs=1&pid=ImgDetMain" alt="Картинка для квізу">
    <p>Натисніть кнопку нижче, щоб почати квіз.</p>
    <button class="start-btn" onclick="startQuiz()">Почати квіз</button>
</div>
<div class="quiz-container" id="quizContainer" style="display: none;">
    <div class="question" id="question"></div>
    <div class="options">
        <button class="option-btn" id="option1" onclick="checkAnswer(this)">Option 1</button>
        <button class="option-btn" id="option2" onclick="checkAnswer(this)">Option 2</button>
        <button class="option-btn" id="option3" onclick="checkAnswer(this)">Option 3</button>
    </div>
    <button class="next-btn" id="nextBtn" style="display: none;" onclick="nextQuestion()">Наступне питання</button>
</div>

<script>
    const questions = [
        {
            question: "Яка італійська марка відома своїми спортивними автомобілями з тельняшкою на логотипі?",
            options: ["Maserati", "Lamborghini", "Ferrari"],
            answer: "Ferrari"
        },
        {
            question: "Яка марка автомобілів вважається 'автомобілем народу'?",
            options: ["Volkswagen", "Toyota", "Ford"],
            answer: "Volkswagen"
        },
        {
            question: "Яка італійська марка відома своїми спортивними автомобілями з тельняшкою на логотипі?",
            options: ["Lamborgini", "Ferrari", "Maserati"],
            answer: "Ferrari"
        },
        {
            question: "Яка марка виготовляє автомобілі з характерними плаваючими 'крилами' на передньому бампері?",
            options: ["Audi", "BMW", "Mercedes-Benz"],
            answer: "Mercedes-Benz"
        },
        {
            question: "Яка марка відома своїми електричними автомобілями, такими як Model S і Model 3?",
            options: ["Ferrari", "Tesla", "Chevrolet"],
            answer: "Tesla"
        },
        {
            question: "Яка німецька марка виробляє автомобілі з характерною решіткою радіатора у формі 'нісового паперового кліпа'?",
            options: ["Volkswagen", "Audi", ""],
            answer: "BMW"
        },
        {
            question: "Яка японська марка відома своїми моделями Accord і Civic?",
            options: ["Subaru", "Toyota", "Honda"],
            answer: "Honda"
        },
        {
            question: "Яка марка відома своїми автомобілями з емблемою з півмісяцем і зіркою на радіаторі?",
            options: ["Audi", "BMW", "Mercedes-Benz"],
            answer: "Mercedes-Benz"
        },
        {
            question: "Яка американська марка випускає спортивні автомобілі з моделями Mustang і F-150?",
            options: ["Ford", "Mercedes-Benz", "Dodge"],
            answer: "Ford"
        },
        {
            question: "Яка марка відома своїми автомобілями з високою прохідністю, такими як Discovery і Range Rover?",
            options: ["Land Rover", "Jeep", "Toyota"],
            answer: "Land Rover"
        },
        {
            question: "Яка марка виготовляє розкішні автомобілі Phantom і Ghost?",
            options: ["Rolls-Royce", "Bentley", "Aston Martin"],
            answer: "Rolls-Royce"
        },
        {
            question: "Хто є власником марки Bugatti?",
            options: ["BMW", "Volkswagen Group", "Mercedes-Benz"],
            answer: "Volkswagen Group"
        },
        {
            question: "Яка італійська марка відома своїми спортивними автомобілями з моделями 488 і F8 Tributo?",
            options: ["BMW", "Lamborghini", "Ferrari"],
            answer: "Ferrari"
        },
        {
            question: "Яка марка виробляє легендарні спортивні автомобілі з моделями 911 і Cayman?",
            options: ["Jaguar", "Audi", "Porsche"],
            answer: "Porsche"
        },
        {
            question: "Яка японська марка відома своїми позашляховиками Outback і Forester?",
            options: ["Subaru", "Porsche", "Nissan"],
            answer: "Subaru"
        },
        {
            question: "Яка марка відома своїми спортивними автомобілями з моделями Giulia і Stelvio?",
            options: ["Alfa Romeo", "Fiat", "Lancia"],
            answer: "Alfa Romeo"
        },
        {
            question: "Яка англійська марка відома своїми розкішними автомобілями з моделями Phantom і Wraith?",
            options: ["Rolls-Royce", "Bentley", "Aston Martin"],
            answer: "Rolls-Royce"
        },
        {
            question: "Яка німецька марка відома своїми автомобілями з моделями A4 і Q7?",
            options: ["Audi", "BMW", "Mercedes-Benz"],
            answer: "Audi"
        },
        {
            question: "Яка марка випускає легендарний спортивний автомобіль з іменем GT-R?",
            options: ["Audi", "Subaru", "Nissan"],
            answer: "Nissan"
        },
        {
            question: "Яка італійська марка відома своїми спортивними автомобілями з моделями Huracan і Aventador?",
            options: ["Pagani", "Ferrari", "Lamborghini"],
            answer: "Lamborghini"
        },
        {
            question: "Яка американська марка випускає позашляховики з моделями Wrangler і Grand Cherokee?",
            options: ["Ford", "Jeep", "Chevrolet"],
            answer: "Jeep"
        }
    ];

    let currentQuestion = 0;
    const totalQuestions = questions.length;
    let score = 0;

    function startQuiz() {
        document.getElementById('titleContainer').style.display = 'none';
        document.getElementById('quizContainer').style.display = 'block';
        shuffleQuestions();
        displayQuestion();
    }

    function shuffleQuestions() {
        for (let i = questions.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1));
            [questions[i], questions[j]] = [questions[j], questions[i]];
        }
    }

    function displayQuestion() {
        if (currentQuestion >= totalQuestions) {
            showResults();
            return;
        }
        const questionElement = document.getElementById('question');
        const optionButtons = document.getElementsByClassName('option-btn');
        questionElement.textContent = `${currentQuestion + 1}. ${questions[currentQuestion].question}`;
        for (let i = 0; i < optionButtons.length; i++) {
            optionButtons[i].textContent = questions[currentQuestion].options[i];
            optionButtons[i].classList.remove('correct', 'incorrect'); // Видаляємо класи
            optionButtons[i].disabled = false;
        }
        document.getElementById('nextBtn').style.display = 'none';
    }

    function checkAnswer(button) {
        const selectedAnswer = button.textContent;
        const correctAnswer = questions[currentQuestion].answer;
        const optionButtons = document.getElementsByClassName('option-btn');
        for (let i = 0; i < optionButtons.length; i++) {
            if (optionButtons[i].textContent === correctAnswer) {
                optionButtons[i].classList.add('correct');
            } else {
                optionButtons[i].classList.add('incorrect');
            }
        }
        if (selectedAnswer === correctAnswer) {
            score++;
        }
        disableOptions();
        document.getElementById('nextBtn').style.display = 'block';
    }

    function disableOptions() {
        const optionButtons = document.getElementsByClassName('option-btn');
        for (let i = 0; i < optionButtons.length; i++) {
            optionButtons[i].disabled = true;
        }
    }

    function nextQuestion() {
        currentQuestion++;
        displayQuestion();
    }

    function showResults() {
        const quizContainer = document.getElementById('quizContainer');
        quizContainer.innerHTML = `<h2>Ваш результат: ${score} з ${totalQuestions}</h2>`;
    }
</script>
</body>
</html>
