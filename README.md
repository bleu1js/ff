<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>XO Game</title>
<style>
  .container {
    display: flex;
    flex-wrap: wrap;
    width: 300px;
  }
  .box {
    width: 100px;
    height: 100px;
    border: 1px solid black;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 24px;
    cursor: pointer;
  }
</style>
</head>
<body>

<div class="container" id="container">
</div>

<script>
  // Initialize the game state
  let currentPlayer = 'X';
  let gameBoard = ['', '', '', '', '', '', '', '', ''];

  // Function to handle the click event on boxes
  function boxClicked(index) {
    if (gameBoard[index] === '') {
      gameBoard[index] = currentPlayer;
      render();
      // Check for a winner
      if (checkWinner(currentPlayer)) {
        alert(currentPlayer + ' wins!');
        resetGame();
        return;
      }
      // Check for a tie
      if (!gameBoard.includes('')) {
        alert('It\'s a tie!');
        resetGame();
        return;
      }
      // Switch players
      currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
    }
  }

  // Function to check for a winner
  function checkWinner(player) {
    const winConditions = [
      [0, 1, 2], [3, 4, 5], [6, 7, 8], // Rows
      [0, 3, 6], [1, 4, 7], [2, 5, 8], // Columns
      [0, 4, 8], [2, 4, 6] // Diagonals
    ];

    return winConditions.some((condition) => {
      return condition.every((index) => {
        return gameBoard[index] === player;
      });
    });
  }

  // Function to reset the game
  function resetGame() {
    currentPlayer = 'X';
    gameBoard = ['', '', '', '', '', '', '', '', ''];
    render();
  }

  // Function to render the game board
  function render() {
    const container = document.getElementById('container');
    container.innerHTML = '';
    gameBoard.forEach((value, index) => {
      const box = document.createElement('div');
      box.classList.add('box');
      box.textContent = value;
      box.onclick = () => boxClicked(index);
      container.appendChild(box);
    });
  }

  // Initial render
  render();
</script>

</body>
</html>
