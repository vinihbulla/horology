<!-- quotes.html -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      text-align: center;
      font-size: 20px;
      margin: 50px;
      font-family: "DIN Next", sans-serif;
    }

    #quote-background {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: -1;
      background: url('https://placekitten.com/1200/800') center/cover no-repeat; /* Substitua o URL pela imagem desejada */
      opacity: 0.2; /* Ajuste a opacidade conforme necessário */
    }

    #phrase-container {
      position: relative;
      z-index: 1;
      margin-bottom: 20px;
      overflow: hidden;
    }

    #phrase {
      transition: transform 0.5s ease-in-out;
    }

    .button-container {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-top: 20px;
    }

    .button {
      background-color: #f0f0f0; /* Cinza Claro */
      color: #333;
      border: none;
      border-radius: 50%;
      width: 40px;
      height: 40px;
      font-size: 16px;
      line-height: 40px; /* Centralizar texto verticalmente */
      cursor: pointer;
      transition: background-color 0.3s ease-in-out;
    }

    .button:hover {
      background-color: #ddd;
    }

    #dots {
      font-size: 16px;
      font-weight: normal;
      margin: 0 10px; /* Espaço entre os pontos e os botões */
    }

    .dot {
      display: inline-block;
      width: 10px;
      height: 10px;
      border-radius: 50%;
      background-color: #f0f0f0; /* Cinza Claro */
      margin: 0 3px; /* Reduzir a distância entre as bolinhas */
      transition: background-color 0.3s ease-in-out;
    }

    .dot:hover {
      background-color: #ddd;
    }

    .dot.active {
      background-color: #555;
      color: white;
    }
  </style>
</head>
<body>
  <div id="quote-background"></div>
  <div id="phrase-container">
    <p id="phrase">Frase 1</p>
  </div>
  <div class="button-container">
    <button class="button" onclick="previousPhrase()">‹</button>
    <span id="dots"></span>
    <button class="button" onclick="nextPhrase()">›</button>
  </div>

  <script>
    const phrases = ["Frase 1", "Frase 2", "Frase 3"];
    let currentPhraseIndex = 0;
    const phraseElement = document.getElementById('phrase');
    const dotsElement = document.getElementById('dots');

    function updatePhrase() {
      phraseElement.style.transform = 'translateY(-20px)';
      setTimeout(() => {
        phraseElement.textContent = phrases[currentPhraseIndex];
        phraseElement.style.transform = 'translateY(0)';
      }, 500);

      updateDots();
    }

    function updateDots() {
      dotsElement.innerHTML = '';
      for (let i = 0; i < phrases.length; i++) {
        const dot = document.createElement('span');
        dot.classList.add('dot');
        dot.addEventListener('click', () => goToPhrase(i));
        dotsElement.appendChild(dot);
      }

      dotsElement.childNodes[currentPhraseIndex].classList.add('active');
    }

    function nextPhrase() {
      currentPhraseIndex = (currentPhraseIndex + 1) % phrases.length;
      updatePhrase();
    }

    function previousPhrase() {
      currentPhraseIndex = (currentPhraseIndex - 1 + phrases.length) % phrases.length;
      updatePhrase();
    }

    function goToPhrase(index) {
      currentPhraseIndex = index;
      updatePhrase();
    }

    updateDots();
  </script>
</body>
</html>
