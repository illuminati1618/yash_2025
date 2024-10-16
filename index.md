---
layout: base
title: Home
units: "1"
course: compsci
description: Home Page
author: Yash Parikh
image: /images/mario_animation.png
hide: true
comments: true
---

{% include nav/home.html %}

<br>
<a href="https://illuminati1618.github.io/yash_2025/2024/10/15/finalprojectsprint2_IPYNB_2_.html">
Sprint 2 Final Project and Culmination of Lessons
</a>

<div class="grid-container">
  <a href="https://illuminati1618.github.io/yash_2025/2024/10/05/3-1-and-4homework_IPYNB_2_.html" class="box">
      Variables
      <div class="dropdown-text">
      > Store data values that can be changed
      <br>
      > Container to hold and manipulate information
      </div>
  </a>

  <a href="https://nighthawkcoders.github.io/portfolio_2025/csp/big-idea/p2/3-2/" class="box">
      Data Abstraction (Lesson Taught)
      <div class="dropdown-text">
      > Simplify complex data structures
      <br>
      > Make programs easy to understand
      <br>
      > Ensure correct use cases
      </div>
  </a>

  <a href="https://illuminati1618.github.io/yash_2025/2024/10/09/3-3-and-5homework_IPYNB_2_.html" class="box">
      Mathematical Expressions
      <div class="dropdown-text">
      > Operations involving numerical values
      <br>
      </div>
  </a>

  <a href="https://illuminati1618.github.io/yash_2025/2024/10/05/3-1-and-4homework_IPYNB_2_.html" class="box">
      Strings
      <div class="dropdown-text">
      > Text values enclosed in quotes
      <br>
      > Text can be utilized
      </div>
  </a>

  <a href="https://illuminati1618.github.io/yash_2025/2024/10/09/3-3-and-5homework_IPYNB_2_.html" class="box">
      Boolean Expressions
      <div class="dropdown-text">
      > Logical statements
      <br>
      > Simplify down to true or false
      <br>
      > Basis of conditionals and decision making
      </div>
  </a>

  <a href="https://illuminati1618.github.io/yash_2025/2024/10/04/3-6-and-7homework_IPYNB_2_.html" class="box">
      Conditionals
      <div class="dropdown-text">
      > Allow program to complete action based on input
      <br>
      > Reduce user input
      <br>
      > Increase autonomy
      </div>
  </a>

  <a href="https://illuminati1618.github.io/yash_2025/2024/10/04/3-6-and-7homework_IPYNB_2_.html" class="box">
      Nested Conditionals
      <div class="dropdown-text">
      > Conditionals in conditionals
      <br>
      > Add complexity in decision-making process
      <br>
      > Edge-case simplification
      </div>
  </a>

  <a href="https://illuminati1618.github.io/yash_2025/2024/10/04/3-8homework_IPYNB_2_.html" class="box">
      Iteration
      <div class="dropdown-text">
      > Repeat code multiple times
      <br>
      > Perform repetitive tasks effectively
      <br>
      > Simplify code
      </div>
  </a>

  <a href="https://illuminati1618.github.io/yash_2025/2024/10/04/3-10homework_IPYNB_2_.html" class="box">
      List Operations
      <div class="dropdown-text">
      > Modifying list elements
      <br>
      > Manage collections of data
      </div>
  </a>

  <a href="https://illuminati1618.github.io/yash_2025/navigation/sprite" class="box">
      Javascript Self Study
      <div class="dropdown-text">
      > Display sprite through sprite sheet
      <br>
      > Interact with DOM through JS
      </div>
  </a>

</div>

{% include scheduleStudent.html %}

<!-- Liquid:  statements -->

<!-- Include submenu from _includes to top of pages {% include nav/home.html %} -->
<!--- Concatenation of site URL to frontmatter image  --->
{% assign sprite_file = site.baseurl | append: page.image %}
<!--- Has is a list variable containing mario metadata for sprite --->
{% assign hash = site.data.mario_metadata %}  
<!--- Size width/height of Sprit images --->
{% assign pixels = 256 %}

<!--- HTML for page contains <p> tag named "Mario" and class properties for a "sprite"  -->

<p id="mario" class="sprite"></p>
  
<!--- Embedded Cascading Style Sheet (CSS) rules, 
        define how HTML elements look 
--->
<style>

  /*CSS style rules for the id and class of the sprite...
  */
  .sprite {
    height: {{pixels}}px;
    width: {{pixels}}px;
    background-image: url('{{sprite_file}}');
    background-repeat: no-repeat;
  }

  /*background position of sprite element
  */
  #mario {
    background-position: calc({{animations[0].col}} * {{pixels}} * -1px) calc({{animations[0].row}} * {{pixels}}* -1px);
  }
</style>

<!--- Embedded executable code--->
<script>
  ////////// convert YML hash to javascript key:value objects /////////

  var mario_metadata = {}; //key, value object
  {% for key in hash %}  
  
  var key = "{{key | first}}"  //key
  var values = {} //values object
  values["row"] = {{key.row}}
  values["col"] = {{key.col}}
  values["frames"] = {{key.frames}}
  mario_metadata[key] = values; //key with values added

  {% endfor %}

  ////////// game object for player /////////

  class Mario {
    constructor(meta_data) {
      this.tID = null;  //capture setInterval() task ID
      this.positionX = 0;  // current position of sprite in X direction
      this.currentSpeed = 0;
      this.marioElement = document.getElementById("mario"); //HTML element of sprite
      this.pixels = {{pixels}}; //pixel offset of images in the sprite, set by liquid constant
      this.interval = 100; //animation time interval
      this.obj = meta_data;
      this.marioElement.style.position = "absolute";
    }

    animate(obj, speed) {
      let frame = 0;
      const row = obj.row * this.pixels;
      this.currentSpeed = speed;

      this.tID = setInterval(() => {
        const col = (frame + obj.col) * this.pixels;
        this.marioElement.style.backgroundPosition = `-${col}px -${row}px`;
        this.marioElement.style.left = `${this.positionX}px`;

        this.positionX += speed;
        frame = (frame + 1) % obj.frames;

        const viewportWidth = window.innerWidth;
        if (this.positionX > viewportWidth - this.pixels) {
          document.documentElement.scrollLeft = this.positionX - viewportWidth + this.pixels;
        }
      }, this.interval);
    }

    startWalking() {
      this.stopAnimate();
      this.animate(this.obj["Walk"], 3);
    }

    startRunning() {
      this.stopAnimate();
      this.animate(this.obj["Run1"], 6);
    }

    startPuffing() {
      this.stopAnimate();
      this.animate(this.obj["Puff"], 0);
    }

    startCheering() {
      this.stopAnimate();
      this.animate(this.obj["Cheer"], 0);
    }

    startFlipping() {
      this.stopAnimate();
      this.animate(this.obj["Flip"], 0);
    }

    startResting() {
      this.stopAnimate();
      this.animate(this.obj["Rest"], 0);
    }

    stopAnimate() {
      clearInterval(this.tID);
    }
  }

  const mario = new Mario(mario_metadata);

  ////////// event control /////////

  window.addEventListener("keydown", (event) => {
    if (event.key === "ArrowRight") {
      event.preventDefault();
      if (event.repeat) {
        mario.startCheering();
      } else {
        if (mario.currentSpeed === 0) {
          mario.startWalking();
        } else if (mario.currentSpeed === 3) {
          mario.startRunning();
        }
      }
    } else if (event.key === "ArrowLeft") {
      event.preventDefault();
      if (event.repeat) {
        mario.stopAnimate();
      } else {
        mario.startPuffing();
      }
    }
  });

  //touch events that enable animations
  window.addEventListener("touchstart", (event) => {
    event.preventDefault(); // prevent default browser action
    if (event.touches[0].clientX > window.innerWidth / 2) {
      // move right
      if (currentSpeed === 0) { // if at rest, go to walking
        mario.startWalking();
      } else if (currentSpeed === 3) { // if walking, go to running
        mario.startRunning();
      }
    } else {
      // move left
      mario.startPuffing();
    }
  });

  //stop animation on window blur
  window.addEventListener("blur", () => {
    mario.stopAnimate();
  });

  //start animation on window focus
  window.addEventListener("focus", () => {
     mario.startFlipping();
  });

  //start animation on page load or page refresh
  document.addEventListener("DOMContentLoaded", () => {
    // adjust sprite size for high pixel density devices
    const scale = window.devicePixelRatio;
    const sprite = document.querySelector(".sprite");
    sprite.style.transform = `scale(${0.2 * scale})`;
    mario.startResting();
  });

</script>