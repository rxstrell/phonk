---
comments: True
layout: post
title: Calculator
description: Calculator
type: hacks
courses: {'csse': {'week': 4}}
categories: ['C4.1']
---

<html>
<head>
    <title>Калькулятор</title>
    <style>
        .calculator {
            width: 250px;
            margin: 0 auto;
        }
        input[type="text"] {
            width: 100%;
            padding: 10px;
            font-size: 24px;
            text-align: right;
        }
        table {
            width: 100%;
            margin-top: 10px;
        }
        table td {
            padding: 5px;
            text-align: center;
            font-size: 20px;
            cursor: pointer;
        }
        #equals {
            background-color: #008CBA;
            color: #fff;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <input type="text" id="display" readonly>
        <table>
            <tr>
                <td onclick="appendToDisplay('7')">7</td>
                <td onclick="appendToDisplay('8')">8</td>
                <td onclick="appendToDisplay('9')">9</td>
                <td onclick="appendToDisplay('+')">+</td>
            </tr>
            <tr>
                <td onclick="appendToDisplay('4')">4</td>
                <td onclick="appendToDisplay('5')">5</td>
                <td onclick="appendToDisplay('6')">6</td>
                <td onclick="appendToDisplay('-')">-</td>
            </tr>
            <tr>
                <td onclick="appendToDisplay('1')">1</td>
                <td onclick="appendToDisplay('2')">2</td>
                <td onclick="appendToDisplay('3')">3</td>
                <td onclick="appendToDisplay('*')">*</td>
            </tr>
            <tr>
                <td onclick="appendToDisplay('0')">0</td>
                <td onclick="appendToDisplay('.')">.</td>
                <td onclick="clearDisplay()">C</td>
                <td onclick="appendToDisplay('/')">/</td>
            </tr>
            <tr>
                <td colspan="4" id="equals" onclick="calculate()">=</td>
            </tr>
        </table>
    </div>

    <script>
        function appendToDisplay(value) {
            document.getElementById('display').value += value;
        }

        function clearDisplay() {
            document.getElementById('display').value = '';
        }

        function calculate() {
            try {
                var result = eval(document.getElementById('display').value);
                document.getElementById('display').value = result;
            } catch (error) {
                document.getElementById('display').value = 'Error';
            }
        }
    </script>
</body>
</html>
