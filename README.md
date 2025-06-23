# immersiononlinequizmaker
HTML CODE

<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Improved Quiz with Admin Panel</title>
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(135deg, #81ecec, #74b9ff);
      margin: 0;
      padding: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    
    .quiz-container {
      background: #fff;
      border-radius: 15px;
      box-shadow: 0 8px 10px rgba(0, 0, 0, 0.1);
      width: 90%;
      max-width: 700px;
      padding: 30px;
      text-align: center;
      transition: transform 0.3s ease-in-out;
      box-sizing: border-box;
    }
    
    .quiz-container:hover {
      transform: scale(1.02);
    }
    
    .question {
      font-size: 1.4em;
      margin-bottom: 25px;
      color: #2d3436;
    }
    
    .options {
      display: flex;
      flex-direction: column;
      gap: 15px;
      margin-bottom: 20px;
    }
    
    .option {
      padding: 12px;
      border: 2px solid #dfe6e9;
      border-radius: 10px;
      background-color: #f1f2f6;
      cursor: pointer;
      transition: background-color 0.3s, color 0.3s, transform 0.2s;
      font-size: 1.1em;
    }
    
    .option:hover {
      background-color: #0984e3;
      color: #fff;
      transform: scale(1.01);
    }
    
    .timer-container {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 20px;
    }
    
    .timer-text {
      font-size: 1.2em;
      color: #e17055;
    }
    
    .timer {
      font-size: 1.2em;
      color: #e17055;
    }
    
    .progress-bar {
      width: 100%;
      background: #dfe6e9;
      border-radius: 10px;
      overflow: hidden;
      margin-bottom: 20px;
      height: 10px;
    }
    
    .progress {
      height: 10px;
      background: #00b894;
      width: 0;
      transition: width 0.3s ease-in-out;
    }
    
    .result {
      font-size: 1.8em;
      color: #00b894;
      display: none;
      margin-top: 20px;
    }
    
    .restart-btn {
      background-color: #0984e3;
      color: #fff;
      border: none;
      padding: 12px 25px;
      font-size: 1.1em;
      border-radius: 10px;
      cursor: pointer;
      margin-top: 25px;
      display: none;
      transition: background-color 0.3s;
    }
    
    .restart-btn:hover {
      background-color: #065a9e;
    }
    
    /* Summary Styles */
    .summary {
      margin-top: 30px;
      text-align: left;
    }
    
    .summary h2 {
      font-size: 1.5em;
      margin-bottom: 10px;
      color: #333;
    }
    
    .summary-item {
      margin-bottom: 10px;
      padding: 10px;
      background: #f9f9f9;
      border-radius: 8px;
      border-left: 4px solid #00b894;
    }
    
    .summary-item.incorrect {
      border-left-color: #e17055;
    }
    
    .summary-item strong {
      display: inline-block;
      width: 120px;
    }
    
    /* Admin Panel Styles */
    #toggleAdminBtn {
      margin: 20px;
      padding: 10px 20px;
      background-color: #6c5ce7;
      color: #fff;
      border: none;
      border-radius: 10px;
      cursor: pointer;
    }
    
    #adminPanel {
      display: none;
      max-width: 700px;
      width: 90%;
      margin: 0 auto 20px auto;
      padding: 20px;
      background: #fff;
      border-radius: 12px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.1);
    }
    
    #adminPanel h2 {
      margin-bottom: 15px;
      color: #333;
    }
    
    #adminPanel form div {
      margin-bottom: 10px;
    }
    
    #adminPanel label {
      font-weight: bold;
    }
    
    #adminPanel input, #adminPanel textarea {
      width: 100%;
      padding: 8px;
      margin-top: 4px;
      border: 1px solid #ccc;
      border-radius: 4px;
      box-sizing: border-box;
    }
    
    #adminPanel button {
      padding: 10px 20px;
      background-color: #0984e3;
      color: #fff;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }
    
    #adminPanel button:hover {
      background-color: #065a9e;
    }
  </style>
</head>
<body>
  <div class="quiz-container">
    <div class="timer-container">
      <div class="timer-text">Time Left:</div>
      <div class="timer"><span id="time">30</span>s</div>
    </div>
    <div class="progress-bar">
      <div class="progress" id="progress"></div>
    </div>
    <div class="question">Question will appear here</div>
    <div class="options"></div>
    <div class="result">Your score: <span id="score">0</span></div>
    <button class="restart-btn">Restart Quiz</button>
  </div>

  <!-- Toggle Button for Admin Panel -->
  <button id="toggleAdminBtn">Show Admin Panel</button>
  
  <!-- Admin Panel -->
  <div id="adminPanel">
    <h2>Admin Panel: Add a New Question</h2>
    <form id="adminForm">
      <div>
        <label for="adminQuestion">Question:</label><br>
        <textarea id="adminQuestion" rows="2"></textarea>
      </div>
      <div>
        <label for="adminOption1">Option 1:</label><br>
        <input type="text" id="adminOption1" />
      </div>
      <div>
        <label for="adminOption2">Option 2:</label><br>
        <input type="text" id="adminOption2" />
      </div>
      <div>
        <label for="adminOption3">Option 3:</label><br>
        <input type="text" id="adminOption3" />
      </div>
      <div>
        <label for="adminOption4">Option 4:</label><br>
        <input type="text" id="adminOption4" />
      </div>
      <div>
        <label for="adminCorrect">Correct Answer:</label><br>
        <input type="text" id="adminCorrect" />
      </div>
      <button type="submit">Add Question</button>
    </form>
  </div>
  
  <script>
    // Initialize quiz data using let so new questions can be added dynamically
    let quizData = [
      {
        question: "What is the capital of France?",
        options: ["Berlin", "Madrid", "Paris", "Lisbon"],
        answer: "Paris"
      },
      {
        question: "Which language is used for web development?",
        options: ["Python", "HTML", "Java", "C++"],
        answer: "HTML"
      },
      {
        question: "Who wrote 'Hamlet'?",
        options: ["Charles Dickens", "William Shakespeare", "Mark Twain", "Jane Austen"],
        answer: "William Shakespeare"
      },
      {
        question: "What is the largest planet in our solar system?",
        options: ["Earth", "Mars", "Jupiter", "Saturn"],
        answer: "Jupiter"
      },
      {
        question: "Which country is known as the Land of the Rising Sun?",
        options: ["China", "Japan", "South Korea", "India"],
        answer: "Japan"
      },
      {
        question: "Which element has the chemical symbol 'O'?",
        options: ["Gold", "Oxygen", "Silver", "Carbon"],
        answer: "Oxygen"
      },
      {
        question: "What is the square root of 64?",
        options: ["6", "7", "8", "9"],
        answer: "8"
      },
      {
        question: "Who painted the 'Mona Lisa'?",
        options: ["Pablo Picasso", "Leonardo da Vinci", "Vincent van Gogh", "Claude Monet"],
        answer: "Leonardo da Vinci"
      },
      {
        question: "What is the boiling point of water at sea level?",
        options: ["90°C", "100°C", "110°C", "120°C"],
        answer: "100°C"
      },
      {
        question: "Which planet is known as the Red Planet?",
        options: ["Venus", "Mars", "Mercury", "Saturn"],
        answer: "Mars"
      }
    ];

    let currentQuestion = 0;
    let score = 0;
    let timeLeft = 30;
    let timerInterval;
    let userAnswers = [];

    const timerEl = document.getElementById('time');
    const questionEl = document.querySelector('.question');
    const optionsEl = document.querySelector('.options');
    const resultEl = document.querySelector('.result');
    const scoreEl = document.getElementById('score');
    const restartBtn = document.querySelector('.restart-btn');
    const progressEl = document.getElementById('progress');
    const quizContainer = document.querySelector('.quiz-container');

    // Load question and update progress bar
    function loadQuestion() {
      if (currentQuestion >= quizData.length) {
        endQuiz();
        return;
      }
      clearInterval(timerInterval);
      timeLeft = 30;
      timerEl.textContent = timeLeft;
      updateProgress();
      startTimer();

      const currentQuiz = quizData[currentQuestion];
      questionEl.textContent = currentQuiz.question;
      optionsEl.innerHTML = '';
      currentQuiz.options.forEach(option => {
        const button = document.createElement('button');
        button.classList.add('option');
        button.textContent = option;
        button.onclick = () => checkAnswer(option);
        optionsEl.appendChild(button);
      });
    }
    
    // Update progress bar based on current question index
    function updateProgress() {
      const progressPercent = (currentQuestion / quizData.length) * 100;
      progressEl.style.width = progressPercent + '%';
    }
    
    // Check answer and record it
    function checkAnswer(selectedOption) {
      clearInterval(timerInterval);
      userAnswers.push(selectedOption);
      if (selectedOption === quizData[currentQuestion].answer) {
        score++;
      }
      currentQuestion++;
      loadQuestion();
    }
    
    // Start question timer
    function startTimer() {
      timerInterval = setInterval(() => {
        timeLeft--;
        timerEl.textContent = timeLeft;
        if (timeLeft <= 0) {
          clearInterval(timerInterval);
          userAnswers.push("No answer");
          currentQuestion++;
          loadQuestion();
        }
      }, 1000);
    }
    
    // End quiz: hide quiz, display results and summary with correct/user answers.
    function endQuiz() {
      clearInterval(timerInterval);
      questionEl.style.display = 'none';
      optionsEl.style.display = 'none';
      progressEl.style.width = '100%';
      resultEl.style.display = 'block';
      scoreEl.textContent = score;
      restartBtn.style.display = 'inline-block';

      // Create the summary container
      const summaryContainer = document.createElement('div');
      summaryContainer.classList.add('summary');
      const summaryTitle = document.createElement('h2');
      summaryTitle.textContent = "Quiz Summary";
      summaryContainer.appendChild(summaryTitle);
      
      quizData.forEach((item, index) => {
        const summaryItem = document.createElement('div');
        summaryItem.classList.add('summary-item');
        const userAnswer = userAnswers[index] || "No answer";
        if (userAnswer !== item.answer) {
          summaryItem.classList.add('incorrect');
        }
        summaryItem.innerHTML = `<strong>Question:</strong> ${item.question}<br>
                                 <strong>Your answer:</strong> ${userAnswer}<br>
                                 <strong>Correct answer:</strong> ${item.answer}`;
        summaryContainer.appendChild(summaryItem);
      });
      
      quizContainer.appendChild(summaryContainer);
    }
    
    // Restart the quiz and remove the summary display if present
    restartBtn.addEventListener('click', () => {
      const summaryEl = document.querySelector('.summary');
      if (summaryEl) {
        summaryEl.remove();
      }
      currentQuestion = 0;
      score = 0;
      userAnswers = [];
      timeLeft = 30;
      timerEl.textContent = timeLeft;
      resultEl.style.display = 'none';
      restartBtn.style.display = 'none';
      questionEl.style.display = 'block';
      optionsEl.style.display = 'flex';
      loadQuestion();
    });
    
    // Initialize quiz
    loadQuestion();
    
    // Admin panel toggle logic
    document.getElementById('toggleAdminBtn').addEventListener('click', function() {
      const panel = document.getElementById('adminPanel');
      if (panel.style.display === 'none' || panel.style.display === '') {
        panel.style.display = 'block';
        this.textContent = 'Hide Admin Panel';
      } else {
        panel.style.display = 'none';
        this.textContent = 'Show Admin Panel';
      }
    });
    
    // Admin form: add new question on submit
    document.getElementById('adminForm').addEventListener('submit', function(e) {
      e.preventDefault();
      const question = document.getElementById('adminQuestion').value.trim();
      const option1 = document.getElementById('adminOption1').value.trim();
      const option2 = document.getElementById('adminOption2').value.trim();
      const option3 = document.getElementById('adminOption3').value.trim();
      const option4 = document.getElementById('adminOption4').value.trim();
      const correct = document.getElementById('adminCorrect').value.trim();
      
      if (!question || !option1 || !option2 || !option3 || !option4 || !correct) {
        alert("Please fill out all fields.");
        return;
      }
      
      const optionsArray = [option1, option2, option3, option4];
      if (!optionsArray.includes(correct)) {
        alert("Correct answer must be one of the provided options.");
        return;
      }
      
      // Add new question to quizData
      quizData.push({
        question: question,
        options: optionsArray,
        answer: correct
      });
      alert("Question added successfully!");
      this.reset();
      // No extra update is needed as quizData.length is used directly.
    });
  </script>
</body>
</html>
