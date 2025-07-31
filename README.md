<!DOCTYPE html>
<html>
<head>
  <title>Tic Tac Toe</title>
  <style>
    #board {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      grid-gap: 10px;
    }
    .cell {
      width: 100px;
      height: 100px;
      background-color: #f0f0f0;
      border: 1px solid #ccc;
      font-size: 36px;
      text-align: center;
      line-height: 100px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div id="board">
    <div class="cell" id="cell-0"></div>
    <div class="cell" id="cell-1"></div>
    <div class="cell" id="cell-2"></div>
    <div class="cell" id="cell-3"></div>
    <div class="cell" id="cell-4"></div>
    <div class="cell" id="cell-5"></div>
    <div class="cell" id="cell-6"></div>
    <div class="cell" id="cell-7"></div>
    <div class="cell" id="cell-8"></div>
  </div>
  <script>
    let currentPlayer = "X";
    let board = ["", "", "", "", "", "", "", "", ""];
    let gameOver = false;

    // Fungsi untuk menangani klik pada cell
    function handleClick(index) {
      if (gameOver) return;
      if (board[index] !== "") return;
      board[index] = currentPlayer;
      document.getElementById(`cell-${index}`).innerText = currentPlayer;
      checkWinner();
      currentPlayer = currentPlayer === "X" ? "O" : "X";
    }

    // Fungsi untuk memeriksa pemenang
    function checkWinner() {
      const winningCombinations = [
        [0, 1, 2],
        [3, 4, 5],
        [6, 7, 8],
        [0, 3, 6],
        [1, 4, 7],
        [2, 5, 8],
        [0, 4, 8],
        [2, 4, 6],
      ];
      for (let combination of winningCombinations) {
        if (
          board[combination[0]] === board[combination[1]] &&
          board[combination[1]] === board[combination[2]] &&
          board[combination[0]] !== ""
        ) {
          gameOver = true;
          alert(`Player ${board[combination[0]]} wins!`);
          return;
        }
      }
      if (!board.includes("")) {
        gameOver = true;
        alert("It's a draw!");
      }
    }

    // Menambahkan event listener pada setiap cell
    for (let i = 0; i < 9; i++) {
      document.getElementById(`cell-${i}`).addEventListener("click", () => handleClick(i));
    }
  </script>
</body>
</html>
