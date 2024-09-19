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

<!-- Oven status bar (initially hidden) -->
<div style="margin-top: 20px;">
    <div id="ovenBarContainer" style="width: 300px; height: 30px; background-color: gray; display: none; float: left;">
        <div id="ovenProgress" style="height: 100%; width: 0%; background-color: yellow;"></div>
    </div>
    <div style="margin-left: 10px; float: left;">
        Oven Level: <span id="ovenLevel">0</span>
    </div>
</div>

<!-- Clear floats -->
<div style="clear: both;"></div>

<!-- Permanent Frenzy Message (initially hidden) -->
<div id="permanentFrenzyMessage" style="text-align: center; color: red; font-weight: bold; font-size: 18px; display: none;">
    Permanent Frenzy Activated!
</div>

<script>
// Count number of cookies
let cookies = 0;
let autoclickers = 0;
let grandmas = 0;
let cookiePerClick = 1;
let baseCookiePerClick = 1; // New variable to store base cookie per click
let ovenActive = false;
let ovenCooldown = 0;
let ovenDuration = 3000; // Oven frenzy duration (3 seconds)
let ovenCooldownPeriod = 20000; // Time between oven frenzies (20 seconds)
let ovenPurchases = 0; // Track how many ovens have been bought
let ovenFrenzyRemaining = 0; // Time remaining for the oven frenzy
let ovenCooldownRemaining = 0; // Time remaining for the cooldown
let permanentFrenzyActive = false; // Track if permanent frenzy is active

// Shop items prices
const ovenPrice = 200;
const grandmaPrice = 25;
const autoclickerPrice = 10;

// Function to update the cookie display
function updateDisplay() {
    document.getElementById("cookieDisplay").innerHTML = Math.floor(cookies);

    // Show the shop once you reach 50 cookies
    if (cookies >= 50) {
        document.getElementById("shop").style.display = "block";
    }

    // Update oven button color if permanent frenzy is reached
    if (permanentFrenzyActive) {
        document.getElementById("buyOven").style.color = "red";
        document.getElementById("buyOven").disabled = true; // Disable the button
    }
}

// Function for manual cookie clicks
document.getElementById("cookieImage").addEventListener("click", () => {
    cookies += cookiePerClick;
    updateDisplay();
});

// Function to update the oven bar (frenzy or cooldown)
function updateOvenBar() {
    let ovenProgressBar = document.getElementById("ovenProgress");

    if (ovenPurchases >= 1) {
        document.getElementById("ovenBarContainer").style.display = "block"; // Show bar after first oven purchase
    }

    if (permanentFrenzyActive) {
        ovenProgressBar.style.width = "100%";
        ovenProgressBar.style.backgroundColor = "red"; // Bar stays red in permanent frenzy
    } else if (ovenActive) {
        let percentage = (ovenFrenzyRemaining / ovenDuration) * 100;
        ovenProgressBar.style.width = percentage + "%";
        ovenProgressBar.style.backgroundColor = "yellow"; // Yellow when oven is active
    } else if (!ovenActive && ovenCooldownRemaining > 0) {
        let percentage = ((ovenCooldownPeriod - ovenCooldownRemaining) / ovenCooldownPeriod) * 100;
        ovenProgressBar.style.width = percentage + "%";
        ovenProgressBar.style.backgroundColor = "blue"; // Blue when in cooldown
    } else {
        ovenProgressBar.style.width = "0%";
    }
}

// Function to display permanent frenzy message with fade-in
function displayPermanentFrenzyMessage() {
    let message = document.getElementById("permanentFrenzyMessage");
    message.style.display = "block";
    message.style.opacity = 0;
    let fadeDuration = 2000; // 2 seconds fade-in

    // Fade-in effect
    let start = null;
    function fadeIn(timestamp) {
        if (!start) start = timestamp;
        let progress = timestamp - start;
        let opacity = Math.min(progress / fadeDuration, 1);
        message.style.opacity = opacity;

        if (progress < fadeDuration) {
            window.requestAnimationFrame(fadeIn);
        }
    }
    window.requestAnimationFrame(fadeIn);
}

// Game loop that updates autoclickers, grandmas, and the oven every 100ms
function gameLoop() {
    // Autoclickers: Increment cookies every 10 seconds (100ms * 100)
    if (autoclickers > 0) {
        cookies += (autoclickers / 100);
    }

    // Grandmas: Increment cookies every 5 seconds (100ms * 50)
    if (grandmas > 0) {
        cookies += (grandmas / 50);
    }

    // Oven logic: Trigger frenzy mode based on cooldown
    if (ovenActive) {
        ovenFrenzyRemaining -= 100; // Reduce frenzy time remaining
        if (ovenFrenzyRemaining <= 0) {
            ovenActive = false;
            cookiePerClick = baseCookiePerClick; // Reset cookies per click to base value
            document.getElementById("ovenStatus").style.display = "none"; // Hide frenzy status
            ovenCooldownRemaining = ovenCooldownPeriod; // Start the cooldown
        }
    } else if (ovenCooldownRemaining > 0) {
        ovenCooldownRemaining -= 100; // Reduce cooldown remaining
    } else if (!ovenActive && ovenCooldownRemaining <= 0 && ovenPurchases > 0 && !permanentFrenzyActive) {
        // Activate oven frenzy
        ovenActive = true;
        ovenFrenzyRemaining = ovenDuration; // Set the oven frenzy time
        cookiePerClick = baseCookiePerClick * 2; // Double cookies per click
        document.getElementById("ovenStatus").style.display = "block"; // Show frenzy status
    }

    // Update the progress bar
    updateOvenBar();

    // Update the cookie display
    updateDisplay();
}

// Buy Autoclicker
document.getElementById("buyAutoclicker").addEventListener("click", () => {
    if (cookies >= autoclickerPrice) {
        cookies -= autoclickerPrice;
        autoclickers++;
        updateDisplay();
    } else {
        alert("Not enough cookies!");
    }
});

// Buy Oven
document.getElementById("buyOven").addEventListener("click", () => {
    if (cookies >= ovenPrice) {
        cookies -= ovenPrice;
        ovenPurchases++;
        updateDisplay();

        // Increase oven level display
        document.getElementById("ovenLevel").innerHTML = ovenPurchases;

        // Reduce cooldown with each purchase, until it's a permanent frenzy
        if (ovenPurchases < 12) {
            ovenCooldownPeriod = Math.max(1000, 20000 - ovenPurchases * 2000); // Reduce by 2 seconds per purchase, down to 1 second
        } else {
            permanentFrenzyActive = true; // Permanent frenzy
            ovenActive = true; // Set oven to be always active
            cookiePerClick = baseCookiePerClick * 2; // Permanent double cookies
            document.getElementById("ovenStatus").style.display = "block"; // Show permanent frenzy status

            // Change bar to red and show permanent frenzy message
            updateOvenBar();
            displayPermanentFrenzyMessage(); // Show fade-in message
        }
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
    } else {
        alert("Not enough cookies!");
    }
});

// Start the game loop, running every 100 milliseconds (0.1 seconds)
setInterval(gameLoop, 100);

</script>