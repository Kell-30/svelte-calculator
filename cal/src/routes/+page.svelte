<script>
    let displayValue = "0";
    let history = "";
    let isOperatorClicked = false;
  
    function handleButtonClick(value) {
      if (value === "C") {
        clearDisplay();
      } else if (value === "=") {
        calculateResult();
      } else {
        if (isOperator(value)) {
          handleOperator(value);
        } else {
          handleNumber(value);
        }
      }
    }
  
    function handleNumber(number) {
      if (displayValue === "0" || isOperatorClicked) {
        displayValue = number;
        isOperatorClicked = false;
      } else {
        displayValue += number;
      }
    }
  
    function handleOperator(operator) {
      if (!isOperatorClicked) {
        history += displayValue + " " + operator + " ";
        displayValue = "0";
        isOperatorClicked = true;
      }
    }
  
    function calculateResult() {
      if (!isOperatorClicked) {
        history += displayValue;
        displayValue = evalInSafeContext(history);
        history = "";
      }
    }
  
    function clearDisplay() {
      displayValue = "0";
      history = "";
      isOperatorClicked = false;
    }
  
    function isOperator(value) {
      return ["+", "-", "*", "/"].includes(value);
    }
  
    function evalInSafeContext(code) {
      return new Function(`return ${code}`)();
    }
  </script>
  
  <main>
    <div class="calculator">
      <div class="display">{displayValue}</div>
      <div class="history">{history}</div>
      <div class="buttons">
        <button on:click={() => handleButtonClick("7")}>7</button>
        <button on:click={() => handleButtonClick("8")}>8</button>
        <button on:click={() => handleButtonClick("9")}>9</button>
        <button on:click={() => handleButtonClick("/")}>/</button>
        <button on:click={() => handleButtonClick("4")}>4</button>
        <button on:click={() => handleButtonClick("5")}>5</button>
        <button on:click={() => handleButtonClick("6")}>6</button>
        <button on:click={() => handleButtonClick("*")}>*</button>
        <button on:click={() => handleButtonClick("1")}>1</button>
        <button on:click={() => handleButtonClick("2")}>2</button>
        <button on:click={() => handleButtonClick("3")}>3</button>
        <button on:click={() => handleButtonClick("-")}>-</button>
        <button on:click={() => handleButtonClick("0")}>0</button>
        <button on:click={() => handleButtonClick(".")}>.</button>
        <button on:click={() => handleButtonClick("+")}>+</button>
        <button on:click={() => handleButtonClick("=")}>=</button>
        <button on:click={() => handleButtonClick("C")}>C</button>
      </div>
    </div>
  </main>
  
  <style>
    main {
      text-align: center;
      margin-top: 50px;
    }
  
    .calculator {
      width: 300px;
      margin: 0 auto;
      border: 1px solid #ccc;
      border-radius: 5px;
      padding: 10px;
    }
  
    .display {
      font-size: 24px;
      margin-bottom: 10px;
      border: 1px solid #ccc;
      padding: 5px;
      background-color: #f8f8f8;
    }
  
    .history {
      font-size: 16px;
      color: #777;
      margin-bottom: 5px;
    }
  
    .buttons {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 5px;
    }
  
    button {
      font-size: 20px;
      padding: 10px;
      border: none;
      background-color: #f0f0f0;
      cursor: pointer;
    }
  
    button:hover {
      background-color: #ddd;
    }
  </style>