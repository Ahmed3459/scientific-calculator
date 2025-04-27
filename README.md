<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Scientific Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background: #f0f0f0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .calculator {
            background: #fff;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
            width: 320px;
            padding: 20px;
        }
        .display {
            width: 100%;
            height: 60px;
            margin-bottom: 15px;
            font-size: 28px;
            text-align: right;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            background: #f9f9f9;
        }
        .buttons {
            display: grid;
            grid-template-columns: repeat(5, 1fr);
            gap: 10px;
        }
        button {
            padding: 15px;
            font-size: 18px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            background: #007bff;
            color: white;
        }
        button:hover {
            opacity: 0.8;
        }
        .function {
            background: #ff9500;
        }
        .clear {
            background: #dc3545;
        }
        .delete {
            background: #6c757d;
        }
        .equals {
            background: #28a745;
            grid-column: span 2;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <input type="text" class="display" id="display" readonly>
        <div class="buttons">
            <button onclick="clearDisplay()">C</button>
            <button onclick="deleteLastChar()" class="delete">⌫</button>
            <button onclick="appendToDisplay('(')">(</button>
            <button onclick="appendToDisplay(')')">)</button>
            <button onclick="appendToDisplay('^')">^</button>
            
            <button onclick="appendToDisplay('√(')">√</button>
            <button onclick="appendToDisplay('sin(')">sin</button>
            <button onclick="appendToDisplay('cos(')">cos</button>
            <button onclick="appendToDisplay('tan(')">tan</button>
            <button onclick="appendToDisplay('π')">π</button>
            
            <button onclick="appendToDisplay('7')">7</button>
            <button onclick="appendToDisplay('8')">8</button>
            <button onclick="appendToDisplay('9')">9</button>
            <button onclick="appendToDisplay('/')">÷</button>
            <button onclick="appendToDisplay('log(')">log</button>
            
            <button onclick="appendToDisplay('4')">4</button>
            <button onclick="appendToDisplay('5')">5</button>
            <button onclick="appendToDisplay('6')">6</button>
            <button onclick="appendToDisplay('*')">×</button>
            <button onclick="appendToDisplay('ln(')">ln</button>
            
            <button onclick="appendToDisplay('1')">1</button>
            <button onclick="appendToDisplay('2')">2</button>
            <button onclick="appendToDisplay('3')">3</button>
            <button onclick="appendToDisplay('-')">-</button>
            <button onclick="memoryOperation('M+')">M+</button>
            
            <button onclick="appendToDisplay('0')">0</button>
            <button onclick="appendToDisplay('.')">.</button>
            <button class="equals" onclick="calculate()">=</button>
            <button onclick="appendToDisplay('+')">+</button>
            <button onclick="memoryOperation('MR')">MR</button>
        </div>
    </div>

    <script>
        let memory = 0;
        
        function appendToDisplay(value) {
            document.getElementById('display').value += value;
        }
        
        function clearDisplay() {
            document.getElementById('display').value = '';
        }
        
        function deleteLastChar() {
            let currentValue = document.getElementById('display').value;
            document.getElementById('display').value = currentValue.slice(0, -1);
        }
        
        function memoryOperation(op) {
            const display = document.getElementById('display');
            if (op === 'M+') {
                memory += parseFloat(display.value) || 0;
            } else if (op === 'M-') {
                memory -= parseFloat(display.value) || 0;
            } else if (op === 'MC') {
                memory = 0;
            } else if (op === 'MR') {
                display.value = memory;
            }
        }
        
        function calculate() {
            try {
                let expr = document.getElementById('display').value;
                expr = expr.replace(/\^/g, '**');
                expr = expr.replace(/√\(/g, 'Math.sqrt(');
                expr = expr.replace(/sin\(/g, 'Math.sin(');
                expr = expr.replace(/cos\(/g, 'Math.cos(');
                expr = expr.replace(/tan\(/g, 'Math.tan(');
                expr = expr.replace(/log\(/g, 'Math.log10(');
                expr = expr.replace(/ln\(/g, 'Math.log(');
                expr = expr.replace(/π/g, 'Math.PI');
                expr = expr.replace(/e/g, 'Math.E');
                
                const result = eval(expr);
                document.getElementById('display').value = result;
            } catch (error) {
                document.getElementById('display').value = 'Error';
            }
        }
    </script>
</body>
</html>
