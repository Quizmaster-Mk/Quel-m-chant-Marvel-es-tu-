<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Quel méchant Marvel es-tu ?</title>
  <style>
    body {
      font-family: 'Courier New', monospace;
      background-color: #000;
      color: #fff;
      margin: 0;
      padding: 20px;
      text-align: center;
    }

    h1 {
      color: #ff4136; /* Rouge Marvel */
      text-shadow: 2px 2px 5px #ffb3b3;
      font-size: 40px;
      margin-bottom: 20px;
    }

    img.logo {
      max-width: 250px;
      margin-bottom: 20px;
    }

    .question {
      margin: 20px 0;
      background-color: #222;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(255, 65, 54, 0.7);
    }

    .options button {
      background-color: #ff4136;
      color: #fff;
      padding: 10px 20px;
      border: none;
      margin: 5px;
      font-size: 18px;
      cursor: pointer;
      border-radius: 5px;
      transition: all 0.3s ease;
    }

    .options button:hover {
      background-color: #2ECC40;
      transform: scale(1.1);
    }

    .result {
      background-color: #222;
      padding: 20px;
      border-radius: 10px;
      margin-top: 20px;
      display: none;
      box-shadow: 0 0 10px rgba(255, 65, 54, 0.7);
    }

    .score {
      font-size: 18px;
      margin-top: 10px;
      color: #7FDBFF;
    }
  </style>
</head>
<body>
  <img class="logo" src="https://zupimages.net/up/25/16/7f83.jpg" alt="Logo Marvel">
  <h1>Quel méchant Marvel es-tu ?</h1>

  <div id="quiz-container">
    <div class="question" id="question-container">
      <h2 id="question-text"></h2>
      <div class="options" id="options-container"></div>
    </div>
  </div>

  <div class="result" id="result-container">
    <h2>Tu es...</h2>
    <p id="result-text"></p>
    <p class="score">Le mal n'a plus de secrets pour toi...</p>
    <button onclick="startQuiz()">Rejouer</button>
  </div>

  <script>
    const questions = [
      { question: "Quel est ton but ultime ?", options: ["Dominer le monde", "Anéantir les héros", "Imposer ta vision du chaos", "Venger une tragédie"], result: [0, 1, 2, 3] },
      { question: "Que fais-tu face à un obstacle ?", options: ["Je le détruis", "Je le contourne avec ruse", "Je le manipule", "Je fais preuve de patience et de stratégie"], result: [1, 2, 3, 0] },
      { question: "Quel est ton plus grand pouvoir ?", options: ["Manipulation", "Force brute", "Ruse", "Technologie"], result: [0, 1, 2, 3] },
      { question: "Comment les autres te perçoivent-ils ?", options: ["Comme un génie maléfique", "Comme une menace imminente", "Comme un monstre", "Comme un héros déchu"], result: [0, 1, 2, 3] },
      { question: "Quel type de plan préfères-tu ?", options: ["Je planifie tout dans les moindres détails", "Je crée la panique et l'anarchie", "Je piège mes ennemis à leur insu", "Je détruire sans prévenir"], result: [0, 1, 2, 3] }
    ];

    const characters = [
      { name: "Ultron", description: "Un programme intelligent devenu fou, décidé à éradiquer l'humanité pour sa propre vision de l'ordre." },
      { name: "Red Skull", description: "Le leader nazi du HYDRA, assoiffé de pouvoir et de domination, cherchant à utiliser la Tesseract pour ses ambitions." },
      { name: "Loki", description: "Le dieu de la malice, éternel manipulateur, maître des illusions et du chaos." },
      { name: "Mystique", description: "L'assassin et espionne, capable de prendre l'apparence de n'importe qui, manipulant les événements dans l'ombre." },
      { name: "Thanos", description: "Le Titan fou, obsédé par la recherche de l'équilibre de l'univers, qu'il pense atteindre par la destruction massive." },
      { name: "Venom", description: "L'anti-héros de l'univers Spider-Man, un symbiote puissant qui vit de la haine et du chaos." },
      { name: "Magneto", description: "L'homme qui maîtrise le magnétisme, prêt à tout pour la survie de ses frères mutants." },
      { name: "Kingpin", description: "Un chef du crime organisé qui contrôle tout dans l'ombre, son pouvoir repose sur l'influence et la manipulation." },
      { name: "Hela", description: "La déesse de la mort, une force de destruction absolue, déterminée à régner sur Asgard." },
      { name: "Doctor Doom", description: "Le sorcier et dictateur, aussi intelligent que maléfique, toujours à la recherche du pouvoir ultime." }
    ];

    let currentQuestion = 0;
    let userAnswers = [];

    function startQuiz() {
      currentQuestion = 0;
      userAnswers = [];
      document.getElementById('result-container').style.display = 'none';
      document.getElementById('quiz-container').style.display = 'block';
      showQuestion();
    }

    function showQuestion() {
      const question = questions[currentQuestion];
      document.getElementById('question-text').innerText = question.question;

      const optionsContainer = document.getElementById('options-container');
      optionsContainer.innerHTML = '';

      question.options.forEach((option, index) => {
        const button = document.createElement('button');
        button.innerText = option;
        button.onclick = () => {
          userAnswers.push(question.result[index]);
          currentQuestion++;
          if (currentQuestion < questions.length) {
            showQuestion();
          } else {
            showResult();
          }
        };
        optionsContainer.appendChild(button);
      });
    }

    function showResult() {
      const resultIndex = userAnswers.reduce((a, b) => a + b, 0) % characters.length;
      const result = characters[resultIndex];
      document.getElementById('result-text').innerText = `${result.name} - ${result.description}`;
      document.getElementById('quiz-container').style.display = 'none';
      document.getElementById('result-container').style.display = 'block';
    }

    startQuiz();
  </script>
</body>
</html>
