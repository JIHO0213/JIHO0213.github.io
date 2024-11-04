<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>딥페이크 구별 퀴즈</title>
  <style>
    body { font-family: Arial, sans-serif; text-align: center; padding: 20px; }
    .quiz-container, .result { display: none; }
    .feedback { font-weight: bold; margin: 10px; }
    .quiz-image { width: 300px; height: auto; }
  </style>
</head>
<body>

  <h1>딥페이크 구별 퀴즈</h1>
  <p>아래 이미지가 진짜인지, 딥페이크인지 맞춰보세요!</p>

  <div id="quiz-container" class="quiz-container">
    <img id="quiz-image" class="quiz-image" src="" alt="Quiz Image">
    <div>
      <button onclick="checkAnswer(true)">진짜</button>
      <button onclick="checkAnswer(false)">딥페이크</button>
    </div>
    <p id="feedback" class="feedback"></p>
  </div>

  <div id="result" class="result">
    <h2>딥페이크의 문제점</h2>
    <p>딥페이크는 가짜 정보를 퍼뜨리거나 악의적으로 사용될 수 있어 사회적 문제가 됩니다...</p>
    <p>딥페이크 피해 상담 전화: 02-1234-5678</p>
  </div>

  <button id="start-quiz" onclick="startQuiz()">퀴즈 시작</button>

  <script>
    // Quiz data: images, correct answers, and explanations
    const quizData = [
      {
        image: "image1.jpg",  // 첫 번째 이미지 파일 경로
        isReal: true,
        explanation: "이 이미지는 자연스러운 눈 깜박임과 피부 질감을 보여줍니다."
      },
      {
        image: "image2.jpg",  // 두 번째 이미지 파일 경로
        isReal: false,
        explanation: "딥페이크 이미지로, 눈 주위와 얼굴 윤곽이 부자연스럽습니다."
      },
      {
        image: "image3.jpg",  // 세 번째 이미지 파일 경로
        isReal: false,
        explanation: "이 이미지의 빛 반사와 눈 깜박임이 어색합니다."
      }
    ];

    let currentQuiz = 0; // 현재 퀴즈 번호
    let correctAnswers = 0;

    function startQuiz() {
      document.getElementById("start-quiz").style.display = "none";
      document.getElementById("quiz-container").style.display = "block";
      loadQuiz();
    }

    function loadQuiz() {
      if (currentQuiz < quizData.length) {
        const quiz = quizData[currentQuiz];
        document.getElementById("quiz-image").src = quiz.image;
        document.getElementById("feedback").innerText = "";
      } else {
        showResult();
      }
    }

    function checkAnswer(isReal) {
      const quiz = quizData[currentQuiz];
      const feedback = document.getElementById("feedback");

      if (isReal === quiz.isReal) {
        feedback.innerText = "정답입니다! " + quiz.explanation;
        feedback.style.color = "green";
        correctAnswers++;
      } else {
        feedback.innerText = "오답입니다! " + quiz.explanation;
        feedback.style.color = "red";
      }

      currentQuiz++;
      setTimeout(loadQuiz, 2000); // 2초 후 다음 퀴즈로 이동
    }

    function showResult() {
      document.getElementById("quiz-container").style.display = "none";
      document.getElementById("result").style.display = "block";
      document.getElementById("result").innerHTML += `<p>맞춘 개수: ${correctAnswers}/${quizData.length}</p>`;
    }
  </script>
</body>
</html>
