--- 
layout: page 
title: cookieclicker 
permalink: /cookieclicker/ 
---

<h1>Welcome to Cookie Clicker!</h1>
<h2>Click this button to access the instructions!</h2>
<button 
    id="instructionsButton"
    style="color: white;"
    onclick="window.open('https://youtube.com/', '_blank', 'noopener,noreferrer');">
    Instructions
</button>
<br>
<img id="cookieImage" src="{{site.baseurl}}/images/cookieclicker/cookie.png" height="150 px">
<br>

Cookies: <span id="cookieDisplay">0</span>

<!-- Shop (initially hidden) -->
<div id="shop" style="display:none; margin-top:20px;">
    <h2>Shop</h2>
    <button id="buyAutoclicker">Buy Autoclicker (10 cookies)</button><br>
    <button id="buyOven">Buy Oven (20 cookies)</button><br>
    <button id="buyGrandma">Buy Grandma (15 cookies)</button>
</div>

<script>
// Count number of cookies
let cookies = 0;
let autoclickers = 0;
let grandmas = 0;
let cookiePerClick = 1; // Multiplied by oven during frenzy

// Shop items
const ovenPrice = 20;
const grandmaPrice = 15;
const autoclickerPrice = 10;

// Function to increment cookie count
function countCookies() {
    return function () {
        cookies += cookiePerClick;
        updateDisplay();
    };
}
const cookieCounter = countCookies();
const button = document.getElementById("cookieImage");
const cookiedisp = document.getElementById("cookieDisplay");

// Display updated cookie count and check shop availability
function updateDisplay() {
    cookiedisp.innerHTML = cookies;
    if (cookies >= 50) {
        document.getElementById("shop").style.display = "block";
    }
}

// Add event listener for manual clicks
button.addEventListener("click", () => {
    cookieCounter();
});

// Autoclicker logic
function activateAutoclicker() {
    setInterval(() => {
        cookies += autoclickers;
        updateDisplay();
    }, 10000); // Autoclick every 10 seconds
}

// Oven logic (frenzy mode)
function activateOven() {
    setInterval(() => {
        cookiePerClick *= 2; // Double clicks
        setTimeout(() => {
            cookiePerClick /= 2; // Reset after 3 seconds
        }, 3000); // Frenzy duration 3 seconds
    }, 20000); // Oven triggers every 20 seconds
}

// Grandma logic
function activateGrandma() {
    setInterval(() => {
        cookies += grandmas; // Grandma autoclicks every 5 seconds
        updateDisplay();
    }, 5000);
}

// Buy Autoclicker
document.getElementById("buyAutoclicker").addEventListener("click", () => {
    if (cookies >= autoclickerPrice) {
        cookies -= autoclickerPrice;
        autoclickers++;
        updateDisplay();
        activateAutoclicker();
    } else {
        alert("Not enough cookies!");
    }
});

// Buy Oven
document.getElementById("buyOven").addEventListener("click", () => {
    if (cookies >= ovenPrice) {
        cookies -= ovenPrice;
        updateDisplay();
        activateOven();
    } else {
        alert("Not enough cookies!");
    }
});

// Buy Grandma
document.getElementById("buyGrandma").addEventListener("click", () => {
    if (cookies >= grandmaPrice) {
        cookies -= grandmaPrice;
        grandmas++;
        updateDisplay();
        activateGrandma();
    } else {
        alert("Not enough cookies!");
    }
});
</script>
