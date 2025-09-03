<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Do you love me?</title>

  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Quicksand:wght@300..700&display=swap" rel="stylesheet" />

  <!-- Styles -->
  <link rel="stylesheet" href="do_you_love_me.css" />
</head>
<body>
  <!-- Question Section -->
  <div class="question-container container">
    <video class="local-gif" src="Reply me love.mp4" autoplay muted loop></video>
    <h2 class="question">Do you love me?</h2>
    <div class="button-container">
      <button class="yes-btn btn js-yes-btn">Yes</button>
      <button class="no-btn btn js-no-btn">No</button>
    </div>
  </div>

  <!-- Result Section -->
  <div class="result-container container">
    <video class="gif-result" src="Love me.mp4" autoplay loop></video>
    <h2>I knew it😍!</h2>
  </div>

  <!-- Heart Loader -->
  <div class="cssload-main">
    <div class="cssload-heart">
      <span class="cssload-heartL"></span>
      <span class="cssload-heartR"></span>
      <span class="cssload-square"></span>
    </div>
    <div class="cssload-shadow"></div>
  </div>

  <!-- Scripts -->
  <script src="do_you_love_me.js"></script>
</body>
</html>

/* Reset */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* Base styles */
body {
  display: grid;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #ffe6e9;
  font-family: "Quicksand", sans-serif;
}

/* Container positioning */
.container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  transition: 0.2s;
}

/* Question container */
.question-container {
  top: 40%;
}

.local-gif {
  width: 100%;
  max-width: 300px;
  border-radius: 10px;
  display: block;
  margin: 0 auto 3rem;
  pointer-events: none;
}

.question {
  font-size: 3.5rem;
  margin-bottom: 1rem;
  text-align: center;
}

.button-container {
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  position: relative;
}

.btn {
  border: none;
  border-radius: 50px;
  padding: 10px 20px;
  font-size: 18px;
  cursor: pointer;
  transition: all 0.3s ease;
  background-color: #ff6b81;
  color: white;
  font-family: "Poppins", sans-serif;
  box-shadow: 0px 4px 15px rgba(255, 107, 129, 0.5);
  position: absolute;
}

.btn:hover {
  background-color: #ffa4b1;
  transform: scale(1.1);
  box-shadow: 0px 6px 20px rgba(255, 107, 129, 0.7);
  text-shadow: 1px 1px 5px rgba(255, 182, 193, 0.8);
}

.yes-btn {
  right: 54%;
}

.no-btn {
  left: 54%;
}

/* Result container */
.result-container {
  display: none;
  top: 40%;
  text-align: center;
}

.gif-result {
  border-radius: 10px;
  margin-bottom: 2rem;
}

.result-container h2 {
  font-size: 3.2rem;
}

/* Heart loader */
.cssload-main {
  display: none;
  position: absolute;
  top: 17%;
  left: 50%;
  transform: translate(-100%, -240%);
}

.cssload-heart {
  position: absolute;
  animation: cssload-heart 2.88s cubic-bezier(0.75, 0, 0.5, 1) infinite;
}

.cssload-heartL,
.cssload-heartR {
  width: 1em;
  height: 1em;
  background-color: #ff0000;
  border-radius: 50%;
  position: absolute;
}

.cssload-heartL {
  transform: translate(-28px, -27px);
  animation: cssload-heartL 2.88s infinite;
}

.cssload-heartR {
  transform: translate(28px, -27px);
  animation: cssload-heartR 2.88s infinite;
}

.cssload-square {
  width: 1em;
  height: 1em;
  background-color: #ff0000;
  transform: scale(1) rotate(-45deg);
  animation: cssload-square 2.88s infinite;
}

.cssload-shadow {
  position: relative;
  width: 1em;
  height: 0.24em;
  background-color: rgb(215, 215, 215);
  border-radius: 50%;
  animation: cssload-shadow 2.88s infinite;
  top: 97px;
  left: 50%;
}

/* Animations */
@keyframes cssload-heart {
  50% { transform: rotate(360deg); }
  100% { transform: rotate(720deg); }
}

@keyframes cssload-heartL {
  60% { transform: scale(0.4); }
}

@keyframes cssload-heartR {
  40% { transform: scale(0.4); }
}

@keyframes cssload-square {
  50% {
    border-radius: 100%;
    transform: scale(0.5) rotate(-45deg);
  }
  100% {
    transform: scale(1) rotate(-45deg);
  }
}

@keyframes cssload-shadow {
  50% {
    transform: scale(0.5);
    background-color: rgb(228, 228, 228);
  }
}
const questionContainer = document.querySelector(".question-container");
const resultContainer = document.querySelector(".result-container");
const gifResult = document.querySelector(".gif-result");
const heartLoader = document.querySelector(".cssload-main");
const yesBtn = document.querySelector(".js-yes-btn");
const noBtn = document.querySelector(".js-no-btn");

// Move "No" button on hover
noBtn.addEventListener("mouseover", () => {
  const containerWidth = questionContainer.offsetWidth;
  const containerHeight = questionContainer.offsetHeight;

  const newX = Math.floor(Math.random() * (containerWidth - noBtn.offsetWidth));
  const newY = Math.floor(Math.random() * (containerHeight - noBtn.offsetHeight));

  noBtn.style.left = `${newX}px`;
  noBtn.style.top = `${newY}px`;
});

// "Yes" button click
yesBtn.addEventListener("click", () => {
  questionContainer.style.display = "none";
  heartLoader.style.display = "block";

  setTimeout(() => {
    heartLoader.style.display = "none";
    resultContainer.style.display = "block";
    gifResult.play();
  }, 3000);
});
