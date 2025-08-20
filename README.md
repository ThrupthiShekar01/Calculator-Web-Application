# Calculator-Web-Application
A fully functional calculator to practice DOM manipulation 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Calculator</title>
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: Arial, sans-serif;
    }

    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: linear-gradient(135deg, #1e3c72, #2a5298);
    }

    .calculator {
      background: #222;
      padding: 20px;
      border-radius: 15px;
      box-shadow: 0 8px 20px rgba(0,0,0,0.5);
      width: 320px;
    }

    .display {
      background: #111;
      color: #0f0;
      font-size: 2rem;
      text-align: right;
      padding: 15px;
      border-radius: 10px;
      margin-bottom: 15px;
      overflow-x: auto;
    }

    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 10px;
    }

    button {
      padding: 20px;
      font-size: 1.2rem;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      transition: 0.3s;
    }

    button:hover {
      opacity: 0.8;
    }

    .btn-operator {
      background: #ff9500;
      color: white;
    }

    .btn-equal {
      background: #28a745;
      color: white;
      grid-column: span 2;
    }

    .btn-clear {
      background: #dc3545;
      color: white;
      grid-column: span 2;
    }

    .btn-number {
      background: #444;
      color: white;
    }
  </style>
</head>
<body>

  <div class="calculator">
    <div class="display" id="display">0</div>
    <div class="buttons">
      <button class="btn-clear" id="clear">C</button>
      <button class="btn-operator" data-value="/">÷</button>
      <button class="btn-operator" data-value="*">×</button>

      <button class="btn-number" data-value="7">7</button>
      <button class="btn-number" data-value="8">8</button>
      <button class="btn-number" data-value="9">9</button>
      <button class="btn-operator" data-value="-">−</button>

      <button class="btn-number" data-value="4">4</button>
      <button class="btn-number" data-value="5">5</button>
      <button class="btn-number" data-value="6">6</button>
      <button class="btn-operator" data-value="+">+</button>

      <button class="btn-number" data-value="1">1</button>
      <button class="btn-number" data-value="2">2</button>
      <button class="btn-number" data-value="3">3</button>
      <button class="btn-number" data-value="0">0</button>

      <button class="btn-number" data-value=".">.</button>
      <button class="btn-equal" id="equal">=</button>
    </div>
  </div>

  <script>
    const display = document.getElementById("display");
    const buttons = document.querySelectorAll("button");
    let currentInput = "";

    function updateDisplay() {
      display.textContent = currentInput || "0";
    }

    buttons.forEach(button => {
      button.addEventListener("click", () => {
        const value = button.getAttribute("data-value");

        if (button.id === "clear") {
          currentInput = "";
        } else if (button.id === "equal") {
          try {
            currentInput = eval(currentInput).toString();
          } catch {
            currentInput = "Error";
          }
        } else {
          currentInput += value;
        }

        updateDisplay();
      });
    });

    // Handle keyboard input
    document.addEventListener("keydown", (e) => {
      if ((e.key >= 0 && e.key <= 9) || "+-*/.".includes(e.key)) {
        currentInput += e.key;
      } else if (e.key === "Enter") {
        try {
          currentInput = eval(currentInput).toString();
        } catch {
          currentInput = "Error";
        }
      } else if (e.key === "Backspace") {
        currentInput = currentInput.slice(0, -1);
      } else if (e.key === "Escape") {
        currentInput = "";
      }
      updateDisplay();
    });

    updateDisplay();
  </script>

</body>
</html>

