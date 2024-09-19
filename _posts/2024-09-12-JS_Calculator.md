---
layout: post
title: JS Calculator
description: Grab Calculator Code and place in IPYNB
type: hacks
---

<style>
  .calculator-output {
    /* calulator output 
      top bar shows the results of the calculator;
      result to take up the entirety of the first row;
      span defines 4 columns and 1 row
    */
    grid-column: span 4;
    grid-row: span 1;

    padding: 0.25em;
    font-size: 20px;
    background-color: #2c3e50;
    color: #ecf0f1;
    box-shadow: 0 0 100px rgba(1, 94, 131, 5000000000);

    display: flex;
    align-items: center;
  }
  #history-container {
    margin-top: 20px;
    background-color: #34495e;
    padding: 10px;
    color: #ecf0f1;
    max-height: 200px;
    overflow-y: auto;
    font-size: 18px;
  }

  #history-list {
    list-style-type: none;
    padding: 0;
  }

  #history-list li {
    margin-bottom: 10px;
  }
</style>

<!-- Add a container for the animation -->
<div id="animation">
  <div class="calculator-container">
      <!--result-->
      <div class="calculator-output" id="output">0</div>
      <!--row 1-->
      <div class="calculator-number">1</div>
      <div class="calculator-number">2</div>
      <div class="calculator-number">3</div>
      <div class="calculator-operation">+</div>
      <!--row 2-->
      <div class="calculator-number">4</div>
      <div class="calculator-number">5</div>
      <div class="calculator-number">6</div>
      <div class="calculator-operation">-</div>
      <!--row 3-->
      <div class="calculator-number">7</div>
      <div class="calculator-number">8</div>
      <div class="calculator-number">9</div>
      <div class="calculator-operation">*</div>
      <!--row 4-->
      <div class="calculator-operation">^</div>
      <div class="calculator-operation">Factors</div>
      <div class="calculator-operation">√</div>
      <div class="calculator-operation">÷</div>
      <!--row 5-->
      <div class="calculator-operation">BTC</div>
      <div class="calculator-operation">ETH</div>
      <div class="calculator-operation">DOGE</div>
      <div class="calculator-operation">
        <span class="currency-dropdown">
          <select id="currency-dropdown" onclick="event.stopPropagation();" onchange="updateCurrency(this.value);">
            <option value="USD">USD</option>
            <option value="EUR">EUR</option>
            <option value="JPY">JPY</option>
            <option value="GBP">GBP</option>
            <option value="AUD">AUD</option>
            <option value="CAD">CAD</option>
            <option value="MXN">MXN</option>
            <option value="INR">INR</option>
            <option value="CNH">CNH</option>
            <option value="HKD">HKD</option>
          </select>
        </span>
      </div>
      <!--row 6-->
      <div class="calculator-clear">A/C</div>
      <div class="calculator-number">0</div>
      <div class="calculator-number">.</div>
      <div class="calculator-equals">=</div>
  </div>
</div>

<br>
<button id="clear-history-button">Clear History</button>
<br>

<div id="history-container">
  <h3>Calculation History</h3>
  <ul id="history-list"></ul>
</div>

<!-- JavaScript (JS) implementation of the calculator. -->
<script>
  // initialize important variables to manage calculations
  var firstNumber = null;
  var operator = null;
  var nextReady = true;
  // build objects containing key elements
  const output = document.getElementById("output");
  const numbers = document.querySelectorAll(".calculator-number");
  const operations = document.querySelectorAll(".calculator-operation");
  const clear = document.querySelectorAll(".calculator-clear");
  const equals = document.querySelectorAll(".calculator-equals");
  const historyList = document.getElementById("history-list");

  // Number buttons listener
  numbers.forEach(button => {
    button.addEventListener("click", function() {
      number(button.textContent);
    });
  });

  // Number action
  function number (value) { // function to input numbers into the calculator
      if (value != ".") {
          if (nextReady == true) { // nextReady is used to tell the computer when the user is going to input a completely new number
              output.innerHTML = value;
              if (value != "0") { // if statement to ensure that there are no multiple leading zeroes
                  nextReady = false;
              }
          } else {
              output.innerHTML = output.innerHTML + value; // concatenation is used to add the numbers to the end of the input
          }
      } else { // special case for adding a decimal; can't have two decimals
          if (output.innerHTML.indexOf(".") == -1) {
              output.innerHTML = output.innerHTML + value;
              nextReady = false;
          }
      }
  }

  // Operation buttons listener
  operations.forEach(button => {
    button.addEventListener("click", function() {
      operation(button.textContent);
    });
  });

  // Operator action
  function operation(choice) {
    if (choice === "Currency") {
      handleCurrencyConversion();
    } else {
      if (firstNumber == null) {
        firstNumber = parseFloat(output.innerHTML);
        nextReady = true;
      } else {
        firstNumber = calculate(firstNumber, parseFloat(output.innerHTML));
      }
      operator = choice;
      output.innerHTML = firstNumber.toString();
      nextReady = true;
    }
  }

  // Handle Currency Conversion
  function handleCurrencyConversion() {
    const selectedCurrency = document.getElementById("currency-dropdown").value;
    const currentOutput = parseFloat(output.innerHTML);
    const convertedAmount = convertCurrency(currentOutput, selectedCurrency);
    output.innerHTML = convertedAmount.toString();
    firstNumber = convertedAmount;
    operator = null; // Reset operator after currency conversion
    nextReady = true;
  }

  // Update Currency Button
  function updateCurrency(currency) {
    handleCurrencyConversion();
  }
  // Convert Currency
  function convertCurrency(amount, targetCurrency) {
    const exchangeRates = {
      'USD': 1,
      'EUR': 0.92,
      'JPY': 144.74,
      'GBP': 0.79,
      'AUD': 1.49,
      'CAD': 1.34,
      'MXN': 16.97,
      'INR': 83.11,
      'CNH': 7.16,
      'HKD': 7.82,
    };
    return amount * exchangeRates[targetCurrency];
  }

  // Calculator
  function calculate (first, second) { // function to calculate the result of the equation
      let result = 0;
      switch (operator) {
          case "+":
              result = first + second;
              break;
          case "-":
              result = first - second;
              break;
          case "*":
              result = first * second;
              break;
          case "÷":
              result = first / second;
              break;
          case "^":
              result = first ** second;
              break;
          case "√":
              result = Math.sqrt(first);
              break;
          case "Factors":
              function findFactors(number) {
                  let factors = [];
                  for (let i = 1; i <= number; i++) {
                      if (number % i === 0) {
                          factors.push(i);
                      }
                  }
                  return factors.join(', ');
              }
              
              result = findFactors(first);
              break;
          case "BTC":
              result = first * 46859.2;
              break;
          case "ETH":
              result = first * 2265.17;
              break;
          case "DOGE":
              result = first * 0.079;
              break;
          case "Currency":
              break;
          default: 
              break;
      }
      if (operator !== "Currency") {
        output.innerHTML = result.toString();
        // firstNumber = result;
      }

      return result;
  }

  // Equals button listener
  equals.forEach(button => {
    button.addEventListener("click", function() {
      equal();
    });
  });

// Equal action
function equal () {
  let secondNumber = parseFloat(output.innerHTML); 
  let result = calculate(firstNumber, secondNumber); // Calculate the result
  addToHistory(firstNumber, operator, secondNumber, result); // Add correct calculation to history
  output.innerHTML = result.toString(); // Display the result
  nextReady = true;
}


  // Clear button listener
  clear.forEach(button => {
    button.addEventListener("click", function() {
      clearCalc();
    });
  });

  // A/C action
  function clearCalc () { // clears calculator
      firstNumber = null;
      output.innerHTML = "0";
      nextReady = true;
  }
    // Add event listener to the window to capture keyboard input
  window.addEventListener("keydown", function(event) {
    handleKeyPress(event.key);
  });

  // Function to handle keyboard input
  function handleKeyPress(key) {
    // Check if the pressed key is a number or a dot
    if (/^[0-9.]$/.test(key)) {
      number(key);
    } else if (key === "+" || key === "-" || key === "*" || key === "/" || key === "^" || key === "√" || key === "Enter") {
      operation(key);
    } else if (key === "Escape") {
      clearCalc();
    }
  }

    // Add to history function
  function addToHistory(first, operator, second, result) {
    const historyEntry = `${first} ${operator} ${second} = ${result}`;
    const li = document.createElement("li");
    li.textContent = historyEntry;
    historyList.appendChild(li);
  }

  // Clear history button listener
document.getElementById("clear-history-button").addEventListener("click", function() {
  clearHistory();
});

// Function to clear the history
function clearHistory() {
  const historyList = document.getElementById("history-list");
  historyList.innerHTML = ""; // Clear the history list by setting its HTML to an empty string
}

</script>