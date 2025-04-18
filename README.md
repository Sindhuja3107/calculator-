# calculator-

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Basic Calculator</title>
  <link rel="stylesheet" href="style.css" />
</head>
<body>
  <div class="calculator">
    <div class="display" id="display">0</div>
    <div class="buttons">
      <button class="btn" onclick="clearDisplay()">C</button>
      <button class="btn" onclick="deleteLast()">⌫</button>
      <button class="btn" onclick="appendOperator('/')">÷</button>
      <button class="btn" onclick="appendOperator('*')">×</button>

      <button class="btn" onclick="appendNumber('7')">7</button>
      <button class="btn" onclick="appendNumber('8')">8</button>
      <button class="btn" onclick="appendNumber('9')">9</button>
      <button class="btn" onclick="appendOperator('-')">−</button>

      <button class="btn" onclick="appendNumber('4')">4</button>
      <button class="btn" onclick="appendNumber('5')">5</button>
      <button class="btn" onclick="appendNumber('6')">6</button>
      <button class="btn" onclick="appendOperator('+')">+</button>

      <button class="btn" onclick="appendNumber('1')">1</button>
      <button class="btn" onclick="appendNumber('2')">2</button>
      <button class="btn" onclick="appendNumber('3')">3</button>
      <button class="btn equal" onclick="calculate()">=</button>

      <button class="btn zero" onclick="appendNumber('0')">0</button>
      <button class="btn" onclick="appendNumber('.')">.</button>
    </div>
  </div>
  <script src="script.js"></script>
</body>
</html>

**css**

body {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background: #f4f4f4;
    font-family: Arial, sans-serif;
  }
  
  .calculator {
    width: 320px;
    background: #fff;
    border-radius: 12px;
    box-shadow: 0 8px 20px rgba(0,0,0,0.2);
    overflow: hidden;
  }
  
  .display {
    background: #222;
    color: #fff;
    text-align: right;
    padding: 20px;
    font-size: 2rem;
  }
  
  .buttons {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-gap: 1px;
    background: #ccc;
  }
  
  .btn {
    padding: 20px;
    font-size: 1.2rem;
    background: #eee;
    border: none;
    cursor: pointer;
    transition: background 0.2s;
  }
  
  .btn:hover {
    background: #ddd;
  }
  
  .equal {
    background: #c72525;
    color: white;
    grid-row: span 2;
  }
  
  .zero {
    grid-column: span 2;
  }

  **java script**

  let display = document.getElementById('display');
let currentInput = '';

function appendNumber(number) {
  if (currentInput === '0' && number !== '.') {
    currentInput = number;
  } else {
    currentInput += number;
  }
  updateDisplay();
}

function appendOperator(operator) {
  if (currentInput === '') return;
  if (isOperator(currentInput.slice(-1))) {
    currentInput = currentInput.slice(0, -1);
  }
  currentInput += operator;
  updateDisplay();
}

function clearDisplay() {
  currentInput = '';
  updateDisplay();
}

function deleteLast() {
  currentInput = currentInput.slice(0, -1);
  updateDisplay();
}

function calculate() {
  try {
    currentInput = eval(currentInput).toString();
  } catch {
    currentInput = 'Error';
  }
  updateDisplay();
}

function updateDisplay() {
  display.textContent = currentInput || '0';
}

function isOperator(char) {
  return ['+', '-', '*', '/'].includes(char);
}
