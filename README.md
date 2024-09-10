# Simple-Calculator
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Simple Calculator</title>
  <link rel="stylesheet" href="style.css"> <!-- Link to the CSS file -->
</head>
<body>
  <div class="calculator">
    <div id="display" class="display">0</div> <!-- Display screen -->
    <div class="buttons">
      <!-- Calculator buttons -->
      <button onclick="clearDisplay()">C</button>
      <button onclick="deleteLast()">DEL</button>
      <button onclick="appendOperator('/')">/</button>
      <button onclick="appendNumber(7)">7</button>
      <button onclick="appendNumber(8)">8</button>
      <button onclick="appendNumber(9)">9</button>
      <button onclick="appendOperator('*')">*</button>
      <button onclick="appendNumber(4)">4</button>
      <button onclick="appendNumber(5)">5</button>
      <button onclick="appendNumber(6)">6</button>
      <button onclick="appendOperator('-')">-</button>
      <button onclick="appendNumber(1)">1</button>
      <button onclick="appendNumber(2)">2</button>
      <button onclick="appendNumber(3)">3</button>
      <button onclick="appendOperator('+')">+</button>
      <button onclick="appendNumber(0)">0</button>
      <button onclick="appendOperator('.')">.</button>
      <button onclick="calculateResult()">=</button>
    </div>
  </div>

  <script src="script.js"></script> <!-- Link to the JavaScript file -->
</body>
</html>
/* style.css */
body {
  font-family: Arial, sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #f4f4f4;
}

.calculator {
  width: 260px;
  background-color: #333;
  border-radius: 10px;
  padding: 20px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
}

.display {
  background-color: #222;
  color: white;
  font-size: 32px;
  text-align: right;
  padding: 10px;
  border-radius: 5px;
  margin-bottom: 20px;
  height: 50px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-gap: 10px;
}

button {
  background-color: #444;
  color: white;
  font-size: 20px;
  padding: 15px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #555;
}

button:active {
  background-color: #666;
}
// script.js
let currentInput = '';
let previousInput = '';
let operator = null;
const display = document.getElementById('display');

// Function to append numbers to the display
function appendNumber(number) {
  if (currentInput.length < 16) { // Limit input length
    currentInput += number;
    updateDisplay();
  }
}

// Function to append operators (+, -, *, /)
function appendOperator(op) {
  if (currentInput !== '') {
    if (operator === null) {
      previousInput = currentInput;
      currentInput = '';
    }
    operator = op;
    updateDisplay();
  }
}

// Function to calculate the result
function calculateResult() {
  if (operator !== null && currentInput !== '') {
    let result;
    const prev = parseFloat(previousInput);
    const curr = parseFloat(currentInput);

    switch (operator) {
      case '+':
        result = prev + curr;
        break;
      case '-':
        result = prev - curr;
        break;
      case '*':
        result = prev * curr;
        break;
      case '/':
        result = prev / curr;
        break;
      default:
        return;
    }

    currentInput = result.toString();
    operator = null;
    previousInput = '';
    updateDisplay();
  }
}

// Function to update the display
function updateDisplay() {
  if (currentInput === '') {
    display.textContent = '0';
  } else {
    display.textContent = currentInput;
  }
}

// Function to clear the display
function clearDisplay() {
  currentInput = '';
  previousInput = '';
  operator = null;
  updateDisplay();
}

// Function to delete the last digit
function deleteLast() {
  currentInput = currentInput.slice(0, -1);
  updateDisplay();
}
