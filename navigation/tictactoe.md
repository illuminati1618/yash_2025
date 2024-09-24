---
layout: post 
title: Tic Tac Toe 
type: tangibles
courses: { compsci: {week: 0} }
comments: true
---

  <style>
    .game-board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-template-rows: repeat(3, 100px);
      gap: 5px;
      justify-content: center;
      margin-top: 50px;
    }
    .cell {
      width: 100px;
      height: 100px;
      background-color: #f2f2f2;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 2em;
      cursor: pointer;
      border: 2px solid #333;
    }
    .message {
      text-align: center;
      font-size: 1.5em;
      margin-top: 20px;
    }
    .play-again {
    display: none;
    margin-top: 20px;
    padding: 20px 40px;
    font-size: 1.5em;
    cursor: pointer;
    background-color: transparent; /* Initial transparent */
    color: white;
    border: none;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    border-radius: 10px;
    box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.2);
    }
  </style>

  <div class="game-board">
    <div class="cell" data-index="0"></div>
    <div class="cell" data-index="1"></div>
    <div class="cell" data-index="2"></div>
    <div class="cell" data-index="3"></div>
    <div class="cell" data-index="4"></div>
    <div class="cell" data-index="5"></div>
    <div class="cell" data-index="6"></div>
    <div class="cell" data-index="7"></div>
    <div class="cell" data-index="8"></div>
  </div>

  <div class="message"></div>
  <button class="play-again">Play Again</button>

  <script>
    const cells = document.querySelectorAll('.cell');
    const message = document.querySelector('.message');
    const playAgainButton = document.querySelector('.play-again');
    let currentPlayer = 'X';
    let board = Array(9).fill(null);
    let isGameActive = true;

    const winningConditions = [
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],
      [0, 3, 6],
      [1, 4, 7],
      [2, 5, 8],
      [0, 4, 8],
      [2, 4, 6],
    ];

    function checkWinner() {
      for (const condition of winningConditions) {
        const [a, b, c] = condition;
        if (board[a] && board[a] === board[b] && board[a] === board[c]) {
          isGameActive = false;
          return board[a];
        }
      }
      if (!board.includes(null)) return 'Draw';
      return null;
    }

    function handleClick(e) {
      const index = e.target.dataset.index;
      if (!isGameActive || board[index]) return;

      board[index] = currentPlayer;
      e.target.textContent = currentPlayer;

      if (currentPlayer === 'X') {
        e.target.style.color = 'red';
      } else {
        e.target.style.color = 'blue';
      }

      const winner = checkWinner();
      if (winner) {
        message.textContent = winner === 'Draw' ? "It's a draw!" : `${winner} wins!`;
        isGameActive = false;
        playAgainButton.style.display = 'block';
      } else {
        currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
      }
    }

    function resetGame() {
      board = Array(9).fill(null);
      isGameActive = true;
      currentPlayer = 'X';
      cells.forEach(cell => {
        cell.textContent = '';
        cell.style.color = '';
      });
      message.textContent = '';
      playAgainButton.style.display = 'none';
    }

    cells.forEach(cell => cell.addEventListener('click', handleClick));
    playAgainButton.addEventListener('click', resetGame);
  </script>