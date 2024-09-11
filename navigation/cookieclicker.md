---
layout: page
title: cookieclicker
permalink: /cookieclicker/
---

<h1>
    Welcome to Cookie Clicker!
</h1>
<h2>
Click this button to access the instructions!
</h2>
<button id="instructionsButton" style="color: white;">Instructions</button>
<br>
<img id="cookieImage" src="{{site.baseurl}}/images/cookieclicker/cookie.png" height="150 px">
<br>

Cookies: <span id="cookieDisplay">0</span>

<script>
    
///count number of cookies
function countCookies() {
    let count = 0;
    return function () {
        count++;
        return count;
    }
}
const cookieCounter = countCookies();
const button = document.getElementById("cookieImage");
const disp = document.getElementById("cookieDisplay");
button.addEventListener("click", () => {
    disp.innerHTML = cookieCounter();
});


//open instructions
function openInstructions() {
    let count = 0;
    return function () {
        count++;
        return count;
    }
}
//const cookieCounter = countCookies();
//const button = document.getElementById("cookieImage");
//const disp = document.getElementById("cookieDisplay");
//button.addEventListener("click", () => {
//    disp.innerHTML = <a>;
//});    
</script>