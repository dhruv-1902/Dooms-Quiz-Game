<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Marvel and Cricket Quiz</title>
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background: linear-gradient(to right, #74ebd5, #ACB6E5);
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      min-height: 100vh;
      margin: 0;
      padding: 1rem;
    }

    .quiz-container {
      background: #fff;
      padding: 2rem;
      border-radius: 15px;
      box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
      width: 90%;
      max-width: 500px;
      text-align: center;
      animation: fadeIn 1s ease;
    }

    .project-members {
      position: absolute;
      top: 10px;
      right: 10px;
      background-color: #ffffffcc;
      padding: 1rem 1.5rem;
      border-radius: 12px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
      max-width: 250px;
      text-align: left;
      font-size: 0.9rem;
      z-index: 1000;
    }

    .project-members h3 {
      margin-top: 0;
      font-size: 1rem;
      color: #333;
      text-align: center;
    }

    .project-members ul {
      list-style: none;
      padding: 0;
      margin: 0;
    }

    .project-members li {
      margin: 0.4rem 0;
    }

    .project-members a {
      text-decoration: none;
      color: #1a73e8;
    }

    .project-members a:hover {
      text-decoration: underline;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(-20px); }
      to { opacity: 1; transform: translateY(0); }
    }

    @keyframes resultFadeIn {
      0% {
        transform: scale(0.8) translateY(30px);
        opacity: 0;
      }
      100% {
        transform: scale(1) translateY(0);
        opacity: 1;
      }
    }

    #result-screen.animated {
      animation: resultFadeIn 1s ease-out forwards;
    }

    .hidden {
      display: none;
    }

    h1, h2 {
      color: #333;
    }

    #timer {
      font-size: 1.2rem;
      color: #00796b;
      margin-bottom: 1rem;
      font-weight: bold;
    }

    #question {
      font-size: 1.3rem;
      margin: 1rem 0;
    }

    #answers button {
      background: #ffffff;
      border: 2px solid #64b5f6;
      border-radius: 12px;
      padding: 1rem;
      margin: 0.6rem 0;
      width: 100%;
      font-size: 1.1rem;
      font-weight: 600;
      color: #333;
      cursor: pointer;
      transition: all 0.25s ease-in-out;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.05);
    }

    #answers button:hover {
      transform: scale(1.03);
      background-color: #e3f2fd;
      box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
    }

    #next-btn, #start-btn {
      margin-top: 1rem;
      padding: 0.6rem 1.2rem;
      font-size: 1rem;
      background-color: #64b5f6;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }

    #next-btn:hover, #start-btn:hover {
      background-color: #42a5f5;
    }

    button:disabled {
      opacity: 0.6;
      cursor: not-allowed;
    }
  </style>
</head>
<body>

  <div class="project-members">
    <h3>👥 Project Members</h3>
    <ul>
      <li><a href="my portfolio2.html" target="_blank"><strong>Bikash Kumar Yadav.H</strong></a> – 🧠 Team Leader</li>
      <li><a href="pandi1.html" target="_blank"><strong>Arul Pandi.K</strong></a> – 👨‍💻 Developer</li>
      <li><a href="https://example.com/sanjay" target="_blank"><strong>Sanjay Ganesh.B</strong></a> – 👨‍💻 Developer</li>
      <li><a href="https://example.com/abhinav" target="_blank"><strong>Abhinav Siddharth.E.K</strong></a> – ✍ Content Creator</li>
      <li><a href="https://example.com/chandru" target="_blank"><strong>Chandru.K</strong></a> – 🧪 Tester</li>
    </ul>
  </div>

  <!-- 🔹 Main Quiz Container -->
  <div class="quiz-container">
    <div id="start-screen">
      <h1>🏏🦸 Marvel and Cricket Quiz!</h1>
      <button id="start-btn">Start Quiz</button>
    </div>

    <div id="quiz-screen" class="hidden">
      <div id="timer">⏱ Time: <span id="time">15</span>s</div>
      <div id="question">Quiz text</div>
      <div id="answers"></div>
      <button id="next-btn" class="hidden">Next</button>
    </div>

    <div id="result-screen" class="hidden">
      <h2>🎉 Your Quiz Score: <span id="score"></span></h2>
      <p>🏆 High Score: <span id="high-score"></span></p>
      <p style="font-size: 1.5rem;">👏 Congratulations! 🎊</p>
      <button onclick="startQuiz()">Play Again</button>
    </div>
  </div>

  <audio id="correct-sound" src="https://www.soundjay.com/buttons/sounds/button-09.mp3"></audio>
  <audio id="wrong-sound" src="https://www.soundjay.com/buttons/sounds/button-10.mp3"></audio>

  <script>
    const questionBank = [
      { question: "What is the real name of the Scarlet Witch?", answers: ["Natasha Romanoff", "Wanda Maximoff", "Carol Danvers", "Jean Grey"], correct: 1 },
      { question: "What metal is used to make Captain America's shield?", answers: ["Adamantium", "Titanium", "Vibranium", "Uru"], correct: 2 },
      { question: "Which Infinity Stone was located on Vormir?", answers: ["Time Stone", "Soul Stone", "Reality Stone", "Mind Stone"], correct: 1 },
      { question: "Who is the director of S.H.I.E.L.D. before it was disbanded?", answers: ["Nick Fury", "Phil Coulson", "Maria Hill", "Alexander Pierce"], correct: 0 },
      { question: "Which movie introduced Spider-Man into the MCU?", answers: ["Spider-Man: Homecoming", "Avengers: Age of Ultron", "Captain America: Civil War", "Iron Man 3"], correct: 2 },
      { question: "Who killed Tony Stark’s parents?", answers: ["Thanos", "Baron Zemo", "Winter Soldier", "Red Skull"], correct: 2 },
      { question: "What is Doctor Strange’s Sanctum called?", answers: ["The Watchtower", "Sanctum Sanctorum", "X-Mansion", "Darkhold Keep"], correct: 1 },
      { question: "What species is Loki biologically?", answers: ["Human", "Frost Giant", "Asgardian", "Elf"], correct: 1 },
      { question: "Which Guardian of the Galaxy said, 'I’m Mary Poppins, y’all!'?", answers: ["Rocket", "Peter Quill", "Yondu", "Drax"], correct: 2 },
      { question: "What is the name of the AI that replaces J.A.R.V.I.S. in Tony Stark’s suit?", answers: ["Friday", "Karen", "Veronica", "Siri"], correct: 0 },
      { question: "Who has scored the most international centuries in cricket?", answers: ["Ricky Ponting", "Sachin Tendulkar", "Virat Kohli", "Brian Lara"], correct: 1 },
      { question: "Which country won the first Cricket World Cup in 1975?", answers: ["India", "Australia", "England", "West Indies"], correct: 3 },
      { question: "Who bowled the fastest delivery in international cricket history?", answers: ["Shoaib Akhtar", "Brett Lee", "Dale Steyn", "Jeff Thomson"], correct: 0 },
      { question: "Which Indian cricketer is known as the 'Hitman'?", answers: ["Virat Kohli", "Rohit Sharma", "KL Rahul", "MS Dhoni"], correct: 1 },
      { question: "In which year did India win its first ICC T20 World Cup?", answers: ["2007", "2011", "2003", "2015"], correct: 0 }
    ];

    let questions = questionBank;
    const startBtn = document.getElementById('start-btn');
    const quizScreen = document.getElementById('quiz-screen');
    const startScreen = document.getElementById('start-screen');
    const resultScreen = document.getElementById('result-screen');
    const questionEl = document.getElementById('question');
    const answersEl = document.getElementById('answers');
    const nextBtn = document.getElementById('next-btn');
    const timeEl = document.getElementById('time');
    const scoreEl = document.getElementById('score');
    const highScoreEl = document.getElementById('high-score');
    const correctSound = document.getElementById('correct-sound');
    const wrongSound = document.getElementById('wrong-sound');

    let currentQuestion = 0;
    let score = 0;
    let timer;
    let timeLeft = 15;

    startBtn.addEventListener('click', startQuiz);
    nextBtn.addEventListener('click', () => {
      currentQuestion++;
      if (currentQuestion < questions.length) {
        showQuestion();
      } else {
        showResult();
      }
    });

    function startQuiz() {
      startScreen.classList.add('hidden');
      resultScreen.classList.add('hidden');
      resultScreen.classList.remove('animated');
      quizScreen.classList.remove('hidden');
      score = 0;
      currentQuestion = 0;
      questions = shuffleArray(questionBank);
      showQuestion();
    }

    function showQuestion() {
      resetState();
      startTimer();
      let q = questions[currentQuestion];
      questionEl.textContent = Question ${currentQuestion + 1}: ${q.question};
      q.answers.forEach((answer, index) => {
        let btn = document.createElement('button');
        btn.textContent = answer;
        btn.addEventListener('click', () => selectAnswer(index === q.correct));
        answersEl.appendChild(btn);
      });
    }

    function resetState() {
      clearInterval(timer);
      timeLeft = 15;
      timeEl.textContent = timeLeft;
      answersEl.innerHTML = '';
      nextBtn.classList.add('hidden');
    }

    function startTimer() {
      timer = setInterval(() => {
        timeLeft--;
        timeEl.textContent = timeLeft;
        if (timeLeft <= 0) {
          clearInterval(timer);
          selectAnswer(false);
        }
      }, 1000);
    }

    function selectAnswer(isCorrect) {
      clearInterval(timer);
      if (isCorrect) {
        score++;
        correctSound.play();
      } else {
        wrongSound.play();
      }
      nextBtn.classList.remove('hidden');
    }

    function showResult() {
      quizScreen.classList.add('hidden');
      resultScreen.classList.remove('hidden');
      resultScreen.classList.add('animated');
      scoreEl.textContent = ${score} / ${questions.length};
      let highScore = localStorage.getItem('highScore') || 0;
      if (score > highScore) {
        localStorage.setItem('highScore', score);
        highScore = score;
      }
      highScoreEl.textContent = highScore;
    }

    function shuffleArray(array) {
      let copy = array.slice();
      for (let i = copy.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [copy[i], copy[j]] = [copy[j], copy[i]];
      }
      return copy;
    }
  </script>
</body>
</html># Dooms-Quiz-Game
This Marvel and Cricket combined quiz webpage brings together the thrill of superheroes and the excitement of the sport. Test your knowledge on iconic Marvel characters and legendary cricket moments in one fun-packed quiz experience!
