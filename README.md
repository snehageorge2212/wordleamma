<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Birthday Wordle for Mom</title>
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background-color: #fff7e6;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
    }
    h1 {
      color: #ff69b4;
    }
    #game {
      display: grid;
      grid-template-rows: repeat(6, 1fr);
      gap: 10px;
    }
    .row {
      display: flex;
      gap: 10px;
    }
    .tile {
      width: 60px;
      height: 60px;
      border: 2px solid #ccc;
      font-size: 2rem;
      text-transform: uppercase;
      text-align: center;
      line-height: 60px;
      background-color: white;
    }
    .correct {
      background-color: #6aaa64;
      color: white;
    }
    .present {
      background-color: #c9b458;
      color: white;
    }
    .absent {
      background-color: #787c7e;
      color: white;
    }
    input {
      margin-top: 20px;
      font-size: 1.2rem;
      padding: 10px;
      width: 200px;
      text-align: center;
      text-transform: uppercase;
    }
    button {
      margin-top: 10px;
      padding: 10px 20px;
      font-size: 1rem;
      background-color: #ff69b4;
      color: white;
      border: none;
      cursor: pointer;
    }
    #message {
      margin-top: 20px;
      font-size: 1.5rem;
      color: green;
    }
  </style>
</head>
<body>
  <h1>Happy Birthday, Mom! 🎉</h1>
  <div id="game"></div>
  <input type="text" id="guessInput" maxlength="5" autofocus />
  <button onclick="submitGuess()">Guess</button>
  <div id="message"></div>

  <script>
    const solution = "GAMMY";
    const game = document.getElementById("game");
    const input = document.getElementById("guessInput");
    const message = document.getElementById("message");
    let currentRow = 0;

    // Create empty game grid
    for (let i = 0; i < 6; i++) {
      const row = document.createElement("div");
      row.classList.add("row");
      for (let j = 0; j < 5; j++) {
        const tile = document.createElement("div");
        tile.classList.add("tile");
        row.appendChild(tile);
      }
      game.appendChild(row);
    }

    function submitGuess() {
      const guess = input.value.toUpperCase();
      if (guess.length !== 5) return;
      if (currentRow >= 6) return;

      const row = game.children[currentRow];
      const letters = row.children;

      for (let i = 0; i < 5; i++) {
        letters[i].textContent = guess[i];
        if (guess[i] === solution[i]) {
          letters[i].classList.add("correct");
        } else if (solution.includes(guess[i])) {
          letters[i].classList.add("present");
        } else {
          letters[i].classList.add("absent");
        }
      }

      if (guess === solution) {
        message.textContent = "You got it! 🎉 Love you, Mom! 💖";
        input.disabled = true;
      }

      currentRow++;
      input.value = "";

      if (currentRow === 6 && guess !== solution) {
        message.textContent = `The word was "${solution}". 💐`;
      }
    }
  </script>
</body>
</html>
