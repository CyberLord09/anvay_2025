---
layout: post
title: Cookie Clicker
description: Cookie Clicker
type: hacks
---


<html>
    <head>
        <title>Shark Bait's Cookie Clicker Game!</title>
    </head>

    <body>
        <div class="container">
            <h1 id="space"></h1>
            <div id="cookie" onclick="cookieClick()">
                <img src="https://media.giphy.com/media/l0u0eiVkW4x0Y/200.gif" width="200px"/>
            </div>
            <p class="cookie-text">Number of Cookies:</p>
            <div id="numbers">0</div>
            <div id="upgradeLevel"></div>

            <p class="instructions">Click the cookie - this makes more cookies. You will automatically upgrade according to the following table of upgrade costs!</p>

            <div class="table-container">
                <table>
                    <tr>
                        <th>Name</th>
                        <th>How many cookies can it make?</th>
                        <th>Cost</th>
                    </tr>
                    <tr>
                        <td>Granny</td>
                        <td>Granny makes 2x as much!</td>
                        <td>30 cookies!</td>
                    </tr>
                    <tr>
                        <td>Factory</td>
                        <td>Factory makes 10x as much!</td>
                        <td>500 cookies!</td>
                    </tr>
                    <tr>
                        <td>Plant</td>
                        <td>Plant makes 30x as much!</td>
                        <td>1,000 cookies!</td>
                    </tr>
                    <tr>
                        <td>SuperPlant</td>
                        <td>SuperPlant makes 1000x as much!</td>
                        <td>100,000 cookies!</td>
                    </tr>
                </table>
            </div>

            <!-- Shop section -->
            <div class="shop-container">
                <h2>Cookie Shop</h2>
                <button id="buyPassive" onclick="buyPassiveCookies()">Buy Passive Cookies (10,000 cookies)</button>
                <p id="passiveInfo">Generates 100 cookies per second.</p>
            </div>
            
            <!-- Invisible button for 10,000 cookies -->
            <button id="hiddenCookie" onclick="getSecretCookies()">Hidden Button</button>
        </div>
    </body>
</html>


<script>
var num = 0;
var passiveCookies = false; // Track if the player has bought passive cookies
var cookiesPerSecond = 0;   // Passive cookies generated per second
var passivePrice = 10000;   // Cost for passive cookies

window.onload = function () {
    var name = prompt("What is your name?");
    var space = document.getElementById("space");
    space.innerHTML = name + "'s Bakery";
    setInterval(generatePassiveCookies, 1000); // Call function every second to add passive cookies
}

function cookieClick() {
    num += 1;

    var numbers = document.getElementById("numbers");
    var upgradeLevel = document.getElementById("upgradeLevel");

    numbers.innerHTML = num;

    if (num >= 30 && num < 500) {
        num += 1;
        upgradeLevel.innerHTML = "Granny Level";
    } else if (num >= 500 && num < 1000) {
        num += 9;
        upgradeLevel.innerHTML = "Factory Level";
    } else if (num >= 1000 && num < 100000) {
        num += 29;
        upgradeLevel.innerHTML = "Plant Level";
    } else if (num >= 100000) {
        num += 999;
        upgradeLevel.innerHTML = "SuperPlant Level";
    }
}

function buyPassiveCookies() {
    if (num >= passivePrice) {
        num -= passivePrice;
        passiveCookies = true;
        cookiesPerSecond = 100; // Set passive cookies per second to 100
        document.getElementById('buyPassive').disabled = true; // Disable the button after purchase
        document.getElementById('buyPassive').innerHTML = "Passive Cookies Purchased!";
    }
}

function generatePassiveCookies() {
    if (passiveCookies) {
        num += cookiesPerSecond;
        document.getElementById("numbers").innerHTML = num;
    }
}

// Function for secret hidden button
function getSecretCookies() {
    num += 10000;
    document.getElementById("numbers").innerHTML = num;
}

</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, sans-serif;
    background: linear-gradient(45deg, #6dd5fa, #2980b9);
    animation: gradient 5s ease infinite;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    text-align: center;
    color: #fff;
}

@keyframes gradient {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
}

.container {
    background-color: rgba(255, 255, 255, 0.1);
    padding: 20px;
    border-radius: 20px;
    box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
    backdrop-filter: blur(10px);
    width: 90%;
    max-width: 600px;
}

h1 {
    font-size: 2em;
    margin-bottom: 20px;
}

#cookie {
    cursor: pointer;
    transition: transform 0.1s;
}

#cookie:hover {
    transform: scale(1.1);
}

.cookie-text, .instructions {
    font-size: 1.2em;
    margin: 15px 0;
}

#numbers, #upgradeLevel {
    font-size: 2em;
    margin: 20px auto;
    padding: 20px;
    background-color: #fff;
    color: #000;
    width: 200px;
    border-radius: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

#upgradeLevel {
    background-color: #f39c12;
}

table {
    width: 100%;
    margin-top: 20px;
    border-collapse: collapse;
}

th, td {
    padding: 10px;
    border: 1px solid #fff;
}

th {
    background-color: #f39c12;
}

td {
    background-color: rgba(255, 255, 255, 0.1);
}

.table-container {
    overflow-x: auto;
    margin-top: 20px;
}

/* Shop Styles */
.shop-container {
    margin-top: 30px;
}

#buyPassive {
    font-size: 1.2em;
    padding: 10px 20px;
    background-color: #3498db;
    border: none;
    color: #fff;
    cursor: pointer;
    border-radius: 10px;
}

#buyPassive:hover {
    background-color: #2980b9;
}

#passiveInfo {
    margin-top: 10px;
    font-size: 1.1em;
}

/* Hidden button */
#hiddenCookie {
    position: absolute;
    top: 380px;
    left: 20px;
    opacity: 0; /* Make it invisible */
    cursor: pointer;
    width: 200px;
    height: 50px;
}

</style>
