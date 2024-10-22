---
layout: page
title: Snake
description: snake game
permalink: /snake/
---

{% include nav/home.html %}

<style>

    body{
    }
    .wrap{
        margin-left: auto;
        margin-right: auto;
    }

    canvas{
        display: none;
        border-style: solid;
        border-width: 10px;
        border-color: #FFFFFF;
    }
    canvas:focus{
        outline: none;
    }

    /* All screens style */
    #gameover p, #setting p, #menu p{
        font-size: 20px;
    }

    #gameover a, #setting a, #menu a{
        font-size: 30px;
        display: block;
    }

    #gameover a:hover, #setting a:hover, #menu a:hover{
        cursor: pointer;
    }

    #gameover a:hover::before, #setting a:hover::before, #menu a:hover::before{
        content: ">";
        margin-right: 10px;
    }

    #menu{
        display: block;
    }

    #gameover{
        display: none;
    }

    #setting{
        display: none;
    }

    #setting input{
        display:none;
    }

    #setting label{
        cursor: pointer;
        display: inline-block; /* Add this to fix the issue */
        padding: 3px; /* Add padding for better readability */
        margin: 2px; /* Add margin for better spacing */
    }

    #setting input:checked + label{
        background-color: #fd5819;
        color: #000;
    }
    /*
    p {
    background: linear-gradient( 
      to right, #ffffff, #ffffff); 
    -webkit-text-fill-color: transparent; 
    -webkit-background-clip: text; 
    }
    */
    #setting p {
        background: none;
        color: #fff
    }

    #setting select {
        background: linear-gradient(to right, #fd5819, #e89b4f);
        color: #000000; /* Set text color to be visible on the background */
        border: 1px solid #ffffff; /* Optional: Add border for better visibility */
    }



    #score_value {
        font-size: 24px; /* Adjust the font size as needed */
        color: black; /* Set text color to black */
        background: linear-gradient(to bottom, #a17101, #dee880);; /* Set background color to orange */
        padding: 5px 10px; /* Add padding for better appearance */
        border-radius: 8px; /* Add border-radius for rounded corners */
        display: inline-block; /* Make it an inline-block to center with text-align */
    }

    .fs-4 {
        text-align: center; /* Center the text */
        color: black; /* Set text color to black */
    }
    

/*
    .highlight-text {
        background-color: rgba(27, 15, 64, 0.4); /* Adjust the color and opacity
        color: #fff;  Text color 
        padding: 1px 4px;
        border-radius: 3px;
         text-shadow: 0 0 4px rgba(255, 255, 255, 0.8);  Text shadow for visibility 
    } */

</style>


<div class="container">
    <header class="pb-3 mb-4 border-bottom border-primary text-dark">
        <p class="fs-4"><span style="color: lightblue; font-size: 24px;">Snake score:</span> <span id="score_value">0</span></p>
    </header>
    <div class="container bg-secondary" style="text-align:center;">
        <!-- Main Menu -->
        <div id="menu" class="py-4 text-light">
            <p>Welcome to Snake, press SPACE to begin</p>
            <a id="new_game" class="link-alert">new game</a>
            <a id="setting_menu" class="link-alert">settings</a>
        </div>
        <!-- Game Over -->
        <div id="gameover" class="py-4 text-light">
            <p>Game Over, press SPACE to try again</p>
            <a id="new_game1" class="link-alert">new game</a>
            <a id="setting_menu1" class="link-alert">settings</a>
        </div>
        <!-- Play Screen -->
        <canvas id="snake" class="wrap" width="220" height="220" tabindex="1"></canvas>
        <!-- Settings Screen -->
        <div id="setting" class="py-4 text-light">
            <p>Settings Screen, press SPACE to go back to playing</p>
            <a id="new_game2" class="link-alert">new game</a>
            <br>
            <p><span style="color: #3da5f5;">Speed:</span>
                <input id="speed1" type="radio" name="speed" value="150"/>
                <label for="speed1">Slow</label>
                <input id="speed2" type="radio" name="speed" value="75" checked/>
                <label for="speed2">Normal</label>
                <input id="speed3" type="radio" name="speed" value="35"/>
                <label for="speed3">Fast</label>
            </p>
            <p><span style="color:#3da5f5;">Wall:</span>
                <input id="wallon" type="radio" name="wall" value="1" checked/>
                <label for="wallon">On</label>
                <input id="walloff" type="radio" name="wall" value="0"/>
                <label for="walloff">Off</label>
            </p>
            <p><span style="color:#3da5f5;">Snake Style:</span>
                <input id="style_fill" type="radio" name="style" value="fill" checked/>
                <label for="style_fill">Block</label>
                <input id="style_stroke" type="radio" name="style" value="stroke"/>
                <label for="style_stroke">Skeleton</label>
            </p>
            <p><span style="color: #3da5f5;">Snake Shape:</span>
                <input id="dotStyle1" type="radio" name="dotStyle" value="square" checked/>
                <label for="dotStyle1">Sharp</label>
                <input id="dotStyle2" type="radio" name="dotStyle" value="rounded"/>
                <label for="dotStyle2">Rounded</label>
                <input id="dotStyle3" type="radio" name="dotStyle" value="circle"/>
                <label for="dotStyle3">Circle</label>
            </p>
            <label for="snakecolor" style="color: #3da5f5; font-size: 20px;">Choose a color for your snake:</label>
            <select name="snakecolor" id="snakecolor">
                <option value="#000000">Black</option>
                <option value="#ffffff">White</option>
                <option value="#f24e00">Red</option>
                <option value="#fc9803">Orange</option>
                <option value="#fcf003">Yellow</option>
                <option value="#03fc5a">Green</option>
                <option value="#180261">Blue</option>
                <option value="#4169e1">Invisible</option>
            </select>
            <!-- 
            <p>Board Size:
                <input id="boardsizesmall" type="radio" name="speed" value="320" checked/>
                <label for="boardsizesmall">Slow</label>
                <input id="boardsizemedium" type="radio" name="speed" value="75"/>
                <label for="boardsizemedium">Normal</label>
                <input id="boardsizelarge" type="radio" name="speed" value="35"/>
                <label for="boadsizelarge">Fast</label>
            </p>
            -->
        </div>
    </div>
</div>

<script>
    //disable arrow key scrolling
    window.addEventListener("keydown", function(e) { if(["Space","ArrowUp","ArrowDown","ArrowLeft","ArrowRight"].indexOf(e.code) > -1) { e.preventDefault(); } }, false);
    
    (function(){
        /* Attributes of Game */
        /////////////////////////////////////////////////////////////
        // Canvas & Context
        const canvas = document.getElementById("snake");
        const ctx = canvas.getContext("2d");
        // HTML Game IDs
        const SCREEN_SNAKE = 0;
        const screen_snake = document.getElementById("snake");
        const ele_score = document.getElementById("score_value");
        const speed_setting = document.getElementsByName("speed");
        const wall_setting = document.getElementsByName("wall");
        const style_setting = document.getElementsByName("style");
        const snakeColorSelect = document.getElementById('snakecolor');
        // HTML Screen IDs (div)
        const SCREEN_MENU = -1, SCREEN_GAME_OVER=1, SCREEN_SETTING=2;
        const screen_menu = document.getElementById("menu");
        const screen_game_over = document.getElementById("gameover");
        const screen_setting = document.getElementById("setting");
        // HTML Event IDs (a tags)
        const button_new_game = document.getElementById("new_game");
        const button_new_game1 = document.getElementById("new_game1");
        const button_new_game2 = document.getElementById("new_game2");
        const button_setting_menu = document.getElementById("setting_menu");
        const button_setting_menu1 = document.getElementById("setting_menu1");
        // Game Control
        const BLOCK = 10;   // size of block rendering
        let SCREEN = SCREEN_MENU;
        let snake;
        let snake_dir;
        let snake_next_dir;
        let snake_speed;
        let food = {x: 0, y: 0};
        let score;
        let wall;
        let snake_style = "fill";
        let dotStyle = "square";
        for (let i = 1; i <= 3; i++) {
            document.getElementById('dotStyle' + i).addEventListener("click", function () {
                dotStyle = this.value;
            });
        }
        let selectedColor = '#000000';
        /* Display Control */
        /////////////////////////////////////////////////////////////
        // 0 for the game
        // 1 for the main menu
        // 2 for the settings screen
        // 3 for the game over screen
        let showScreen = function(screen_opt){
            SCREEN = screen_opt;
            switch(screen_opt){
                case SCREEN_SNAKE:
                    screen_snake.style.display = "block";
                    screen_menu.style.display = "none";
                    screen_setting.style.display = "none";
                    screen_game_over.style.display = "none";
                    break;
                case SCREEN_GAME_OVER:
                    screen_snake.style.display = "block";
                    screen_menu.style.display = "none";
                    screen_setting.style.display = "none";
                    screen_game_over.style.display = "block";
                    break;
                case SCREEN_SETTING:
                    screen_snake.style.display = "none";
                    screen_menu.style.display = "none";
                    screen_setting.style.display = "block";
                    screen_game_over.style.display = "none";
                    break;
            }
        }
        /* Actions and Events  */
        /////////////////////////////////////////////////////////////
        window.onload = function(){
            // HTML Events to Functions
            button_new_game.onclick = function(){newGame();};
            button_new_game1.onclick = function(){newGame();};
            button_new_game2.onclick = function(){newGame();};
            button_setting_menu.onclick = function(){showScreen(SCREEN_SETTING);};
            button_setting_menu1.onclick = function(){showScreen(SCREEN_SETTING);};
            // speed
            setSnakeSpeed(150);
            for(let i = 0; i < speed_setting.length; i++){
                speed_setting[i].addEventListener("click", function(){
                    for(let i = 0; i < speed_setting.length; i++){
                        if(speed_setting[i].checked){
                            setSnakeSpeed(speed_setting[i].value);
                        }
                    }
                });
            }
            // wall setting
            setWall(1);
            for(let i = 0; i < wall_setting.length; i++){
                wall_setting[i].addEventListener("click", function(){
                    for(let i = 0; i < wall_setting.length; i++){
                        if(wall_setting[i].checked){
                            setWall(wall_setting[i].value);
                        }
                    }
                });
            }

            for (let i = 0; i < style_setting.length; i++) {
                style_setting[i].addEventListener("click", function () {
                    for (let i = 0; i < style_setting.length; i++) {
                        if (style_setting[i].checked) {
                            snake_style = style_setting[i].value;
                        }
                    }
                });
            }

            snakeColorSelect.addEventListener('change', function() {
                selectedColor = snakeColorSelect.value;
            });
            // activate window events
            window.addEventListener("keydown", function(evt) {
                // spacebar detected
                if(evt.code === "Space" && SCREEN !== SCREEN_SNAKE)
                    newGame();
            }, true);
        }
        /* Snake is on the Go (Driver Function)  */
        /////////////////////////////////////////////////////////////
        let mainLoop = function(){
            let _x = snake[0].x;
            let _y = snake[0].y;
            snake_dir = snake_next_dir;   // read async event key
            // Direction 0 - Up, 1 - Right, 2 - Down, 3 - Left
            switch(snake_dir){
                case 0: _y--; break;
                case 1: _x++; break;
                case 2: _y++; break;
                case 3: _x--; break;
            }
            snake.pop(); // tail is removed
            snake.unshift({x: _x, y: _y}); // head is new in new position/orientation
            // Wall Checker
            if(wall === 1){
                // Wall on, Game over test
                if (snake[0].x < 0 || snake[0].x === canvas.width / BLOCK || snake[0].y < 0 || snake[0].y === canvas.height / BLOCK){
                    showScreen(SCREEN_GAME_OVER);
                    return;
                }
            }else{
                // Wall Off, Circle around
                for(let i = 0, x = snake.length; i < x; i++){
                    if(snake[i].x < 0){
                        snake[i].x = snake[i].x + (canvas.width / BLOCK);
                    }
                    if(snake[i].x === canvas.width / BLOCK){
                        snake[i].x = snake[i].x - (canvas.width / BLOCK);
                    }
                    if(snake[i].y < 0){
                        snake[i].y = snake[i].y + (canvas.height / BLOCK);
                    }
                    if(snake[i].y === canvas.height / BLOCK){
                        snake[i].y = snake[i].y - (canvas.height / BLOCK);
                    }
                }
            }
            // Snake vs Snake checker
            for(let i = 1; i < snake.length; i++){
                // Game over test
                if (snake[0].x === snake[i].x && snake[0].y === snake[i].y){
                    showScreen(SCREEN_GAME_OVER);
                    return;
                }
            }
            // Snake eats food checker
            if(checkBlock(snake[0].x, snake[0].y, food.x, food.y)){
                snake[snake.length] = {x: snake[0].x, y: snake[0].y};
                altScore(++score);
                addFood();
                activeDot(food.x, food.y);
            }
            // Repaint canvas
            ctx.beginPath();
            ctx.fillStyle = "royalblue";
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            // Paint snake
            for(let i = 0; i < snake.length; i++){
                activeDot(snake[i].x, snake[i].y);
            }
            // Paint food
            activeDot(food.x, food.y);
            // Debug
            //document.getElementById("debug").innerHTML = snake_dir + " " + snake_next_dir + " " + snake[0].x + " " + snake[0].y;
            // Recursive call after speed delay, déjà vu
            setTimeout(mainLoop, snake_speed);
        }
        /* New Game setup */
        /////////////////////////////////////////////////////////////
        let newGame = function(){
            // snake game screen
            showScreen(SCREEN_SNAKE);
            screen_snake.focus();
            // game score to zero
            score = 0;
            altScore(score);
            // initial snake
            snake = [];
            snake.push({x: 0, y: 15});
            snake_next_dir = 1;
            // food on canvas
            addFood();
            // activate canvas event
            canvas.onkeydown = function(evt) {
                changeDir(evt.keyCode);
            }
            mainLoop();
        }
        /* Key Inputs and Actions */
        /////////////////////////////////////////////////////////////
        let changeDir = function(key){
            // test key and switch direction
            switch(key) {
                case 37:    // left arrow
                    if (snake_dir !== 1)    // not right
                        snake_next_dir = 3; // then switch left
                    break;
                case 38:    // up arrow
                    if (snake_dir !== 2)    // not down
                        snake_next_dir = 0; // then switch up
                    break;
                case 39:    // right arrow
                    if (snake_dir !== 3)    // not left
                        snake_next_dir = 1; // then switch right
                    break;
                case 40:    // down arrow
                    if (snake_dir !== 0)    // not up
                        snake_next_dir = 2; // then switch down
                    break;
            }
        }
        /* Dot for Food or Snake part */
        /////////////////////////////////////////////////////////////
        let activeDot = function (x, y) {
            ctx.lineJoin = "round";
            ctx.lineCap = "round";

            if (snake_style === "fill") {
                ctx.fillStyle = selectedColor;
                if (dotStyle === "circle") {
                    ctx.beginPath();
                    ctx.arc(x * BLOCK + BLOCK / 2, y * BLOCK + BLOCK / 2, BLOCK / 2, 0, 2 * Math.PI);
                    ctx.fill();
                } else if (dotStyle === "rounded") {
                    ctx.lineJoin = "round";
                    ctx.lineCap = "round";
                    ctx.fillRect(x * BLOCK, y * BLOCK, BLOCK, BLOCK);
                } else {
                    ctx.fillRect(x * BLOCK, y * BLOCK, BLOCK, BLOCK);
                }
            } else if (snake_style === "stroke") {
                ctx.strokeStyle = selectedColor;
                if (dotStyle === "circle") {
                    ctx.beginPath();
                    ctx.arc(x * BLOCK + BLOCK / 2, y * BLOCK + BLOCK / 2, BLOCK / 2, 0, 2 * Math.PI);
                    ctx.stroke();
                } else if (dotStyle === "rounded") {
                    ctx.lineJoin = "round";
                    ctx.lineCap = "round";
                    ctx.strokeRect(x * BLOCK, y * BLOCK, BLOCK, BLOCK);
                } else {
                    ctx.strokeRect(x * BLOCK, y * BLOCK, BLOCK, BLOCK);
                }
            }
        }

        /* Random food placement */
        /////////////////////////////////////////////////////////////
        let addFood = function(){
            food.x = Math.floor(Math.random() * ((canvas.width / BLOCK) - 1));
            food.y = Math.floor(Math.random() * ((canvas.height / BLOCK) - 1));
            for(let i = 0; i < snake.length; i++){
                if(checkBlock(food.x, food.y, snake[i].x, snake[i].y)){
                    addFood();
                }
            }
        }
        /* Collision Detection */
        /////////////////////////////////////////////////////////////
        let checkBlock = function(x, y, _x, _y){
            return (x === _x && y === _y);
        }
        /* Update Score */
        /////////////////////////////////////////////////////////////
        let altScore = function(score_val){
            ele_score.innerHTML = String(score_val);
        }
        /////////////////////////////////////////////////////////////
        // Change the snake speed...
        // 150 = slow
        // 100 = normal
        // 50 = fast
        let setSnakeSpeed = function(speed_value){
            snake_speed = speed_value;
        }
        /////////////////////////////////////////////////////////////
        let setWall = function(wall_value){
            wall = wall_value;
            if(wall === 0){screen_snake.style.borderColor = "#606060";}
            if(wall === 1){screen_snake.style.borderColor = "#FFFFFF";}
        }
    })();
</script>