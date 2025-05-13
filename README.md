# PRODIGY_WD_03
<html>
<head>
  <meta charset="UTF-8" />
  <title>Tic Tac Toe</title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      background: #1e1e2f;
      color: white;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      margin: 0;
    }

    h1 {
      margin-bottom: 20px;
    }

    .board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-template-rows: repeat(3, 100px);
      gap: 5px;
    }

    .cell {
      width: 100px;
      height: 100px;
      font-size: 36px;
      color: #fff;
      background-color: #4e54c8;
      display: flex;
      align-items: center;
      justify-content: center;
      cursor: pointer;
      border-radius: 8px;
    }

    .cell:hover {
      background-color: #3d42a6;
    }

    .status {
      margin-top: 20px;
      font-size: 20px;
    }

    button {
      margin-top: 15px;
      padding: 10px 20px;
      font-size: 16px;
      background-color: #4e54c8;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    button:hover {
      background-color: #3d42a6;
    }
  </style>
</head>
<body>

  <h1>Tic Tac Toe</h1>
  <div class="board" id="board"></div>
  <div class="status" id="status">Current Turn: X</div>
  <button onclick="resetGame()">Restart</button>

  <script>
    const board = document.getElementById("board");
    const statusText = document.getElementById("status");
    let currentPlayer = "X";
    let gameActive = true;
    let gameState = ["", "", "", "", "", "", "", "", ""];

    const winningConditions = [
      [0,1,2], [3,4,5], [6,7,8],
      [0,3,6], [1,4,7], [2,5,8],
      [0,4,8], [2,4,6]
    ];

    function handleClick(index) {
      if (!gameActive || gameState[index] !== "") return;
      gameState[index] = currentPlayer;
      renderBoard();
      if (checkWin()) {
        statusText.innerText = `${currentPlayer} wins!`;
        gameActive = false;
        return;
      }
      if (!gameState.includes("")) {
        statusText.innerText = "It's a draw!";
        gameActive = false;
        return;
      }
      currentPlayer = currentPlayer === "X" ? "O" : "X";
      statusText.innerText = `Current Turn: ${currentPlayer}`;
    }

    function renderBoard() {
      board.innerHTML = "";
      gameState.forEach((cell, index) => {
        const cellElement = document.createElement("div");
        cellElement.classList.add("cell");
        cellElement.innerText = cell;
        cellElement.onclick = () => handleClick(index);
        board.appendChild(cellElement);
      });
    }

    function checkWin() {
      return winningConditions.some(condition => {
        const [a, b, c] = condition;
        return gameState[a] && gameState[a] === gameState[b] && gameState[b] === gameState[c];
      });
    }

    function resetGame() {
      currentPlayer = "X";
      gameState = ["", "", "", "", "", "", "", "", ""];
      gameActive = true;
      statusText.innerText = `Current Turn: ${currentPlayer}`;
      renderBoard();
    }

    // Initial render
    renderBoard();
  </script>

</body>
</html>
