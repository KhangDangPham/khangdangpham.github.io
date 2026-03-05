---
layout: page
title: TI-84 Calculator
permalink: /ti84-calculator
---

## TI-84 Simple Calculator
A simple calculator app version of the TI-84 calculator

```html
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>TI-84 Simple Calculator</title>
    <link href="style.css" rel="stylesheet" />
</head>
<body>
    <div class="calculator">
        <div class="top">
            <h1 class="title">TI-84</h1>
            <input type="text" id="display" disabled/>
        </div>
        <div class="bottom">
            <button class="btn hidden"></button>
            <button class="btn hidden"></button>
            <button class="btn hidden"></button>
            <button id="clear" class="btn dark">CLEAR</button>
            <button class="btn light math">7</button>
            <button class="btn light math">8</button>
            <button class="btn light math">9</button>
            <button class="btn gray math">÷</button>
            <button class="btn light math">4</button>
            <button class="btn light math">5</button>
            <button class="btn light math">6</button>
            <button class="btn gray math">x</button>
            <button class="btn light math">1</button>
            <button class="btn light math">2</button>
            <button class="btn light math">3</button>
            <button class="btn gray math">-</button>
            <button class="btn light math">0</button>
            <button class="btn light math">.</button>
            <button class="btn hidden"></button>
            <button class="btn gray math">+</button>
            <button id="enter" class="btn gray">ENTER</button>
        </div>
    </div>
    <script src="script.js"></script>
</body>
```

```css
body {
  font-family: Arial, sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: auto;
  height: 100vh;
}

.top {
  display: flex;
  flex-direction: column;
  background: lightgray;
  padding: 0 20px;
}

.title {
  color: gray;
  margin: 0;
  text-align: center;
  font-size: 1.5rem;
  padding: 10px 0;
}

.calculator {
  background: #000;
  padding: 0 10px 20px;
  border-radius: 0 0 3rem 3rem;
  box-shadow: 0 30px 15px rgba(0, 0, 0, 0.1);
  width: auto;
  display: flex;
  flex-direction: column;
}

#display {
  font-size: 1rem;
  text-align: left;
  margin-bottom: 1.25rem;
  padding: 10px;
  background: whitesmoke;
  color: black;
  font-weight: bold;
}

.bottom {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 0.625rem;
  padding: 1.25rem 1.25rem 1.375rem;
}

.btn {
  border: 1px solid white;
  cursor: pointer;
  transition: background 0.3s ease;
}

.btn:hover {
  background: #ddd;
}

.light {
  background: white;
  border-radius: 0.25rem 0.25rem 0.75rem 0.75rem;
  color: black;
  font-weight: bolder;
  font-size: 1.5rem;
  padding: 0.3125rem;
}

.dark {
  background: black;
  border-radius: 0.25rem 0.25rem 0.75rem 0.75rem;
  color: white;
  font-size: 0.75rem;
}

#clear {
  padding: 0.3126rem 0;
}

.gray {
  background: gray;
  border-radius: 0.25rem 0.25rem 0.75rem 0.75rem;
  color: white;
  font-size: 1.5rem;
}

.hidden {
  visibility: hidden;
}

#enter {
  grid-column: span 4;
}
```

```javascript
// Reference to the display
const display = document.getElementById('display');
const buttons = document.querySelectorAll('.math');
const clearButton = document.getElementById('clear');
const enterButton = document.getElementById('enter');

// Function to calculate the result
function calculateResult(value) {
    const calculatedValue = eval(value || null);
    if (isNaN(calculatedValue)) {
        display.value = "Error: Cannot divide 0 by 0";
        setTimeout(() => {
            display.value = "";
        }, 1500);
    } else {
        display.value = calculatedValue;
    }
}

// Function to update the display
function updateDisplay(inputValue) {
    if (!display.value) {
        display.value = "";
    }

    display.value += inputValue;
}

// Function to handle number and decimal button clicks
buttons.forEach(button => {
    button.addEventListener('click', () => {
        let value = button.textContent;

        if (value === '÷') {
            value = '/';
        } else if (value === 'x') {
            value = '*';
        }

        updateDisplay(value);
    });
});

// Function to handle clear button
clearButton.addEventListener('click', () => {
    display.value = "";
});

// Function to handle enter button
enterButton.addEventListener('click', () => {
    calculateResult(display.value)
});

// Adding event handler on document for keyboard inputs
document.addEventListener('keydown', keyboardHandler);

// Function to handle keyboard inputs
function keyboardHandler(e) {
    e.preventDefault();

    // integers
    if (e.key === "0") {
        display.value += "0";
    } else if (e.key === "1") {
        display.value += "1";
    } else if (e.key === "2") {
        display.value += "2";
    } else if (e.key === "3") {
        display.value += "3";
    } else if (e.key === "4") {
        display.value += "4";
    } else if (e.key === "5") {
        display.value += "5";
    } else if (e.key === "6") {
        display.value += "6";
    } else if (e.key === "7") {
        display.value += "7";
    } else if (e.key === "8") {
        display.value += "8";
    } else if (e.key === "9") {
        display.value += "9";
    }

    // operators
    if (e.key === "/") {
        display.value += "/";
    } else if (e.key === "*") {
        display.value += "*";
    } else if (e.key === "-") {
        display.value += "-";
    } else if (e.key === "+") {
        display.value += "+";
    }

    // decimal
    if (e.key === ".") {
        display.value += ".";
    }

    // enter
    if (e.key === "Enter") {
        calculateResult(display.value);
    }

    // backspace
    if (e.key === "Backspace") {
        const currentInput = display.value;
        display.value = currentInput.substring(0, display.value.length - 1);
    }
}
```
