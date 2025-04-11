---
layout: post
title: Physics - Bouncing Ball Simulation
type: issues
comments: True
permalink: /csp/bouncingball
---

<style>
    /* reuse your original styles */
    :root {
        --primary-color: #3498db !important;
        --secondary-color: #2ecc71 !important;
        --card-color: #ffffff !important;
        --text-color: #333333 !important;
        --shadow: 0 4px 6px rgba(0, 0, 0, 0.1) !important;
    }

    body {
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif !important;
        padding: 20px !important;
        display: flex !important;
        justify-content: center !important;
        align-items: center !important;
        min-height: 100vh !important;
        color: var(--text-color) !important;
    }

    .container {
        width: 100% !important;
        max-width: 800px !important;
        background-color: var(--card-color) !important;
        border-radius: 12px !important;
        box-shadow: var(--shadow) !important;
        padding: 30px !important;
    }

    canvas {
        width: 100% !important;
        height: 300px !important;
        background-color: #ecf0f1 !important;
        display: block;
        border-radius: 8px;
        margin-bottom: 20px;
    }

    label {
        font-weight: 500 !important;
        display: block;
        margin-bottom: 5px;
    }

    input {
        width: 100%;
        padding: 10px;
        margin-bottom: 15px;
        border-radius: 6px;
        border: 1px solid #ccc;
    }

    .generate-btn {
        background-color: var(--secondary-color);
        color: white;
        padding: 12px 30px;
        border: none;
        border-radius: 6px;
        cursor: pointer;
        font-size: 18px;
        box-shadow: var(--shadow);
    }

    .generate-btn:hover {
        background-color: #27ae60;
    }
</style>

<div class="container">
    <h1>Bouncing Ball Physics Simulation</h1>
    <canvas id="ballCanvas" width="800" height="300"></canvas>

    <div>
        <label for="gravity">Gravity (m/s²):</label>
        <input type="number" id="gravity" value="-9.8" step="0.1">

        <label for="restitution">Restitution (Bounce Energy Loss):</label>
        <input type="number" id="restitution" value="0.75" step="0.05" min="0" max="1">

        <label for="initialHeight">Initial Height (m):</label>
        <input type="number" id="initialHeight" value="10" min="0" step="0.5">

        <button class="generate-btn" onclick="resetSimulation()">Start Simulation</button>
    </div>
</div>

<script>
    const canvas = document.getElementById("ballCanvas");
    const ctx = canvas.getContext("2d");

    let gravity, restitution, initialY, velocity;
    const timeStep = 0.05;
    const pixelsPerMeter = canvas.height / 12;
    const radius = 20;

    function resetSimulation() {
        gravity = parseFloat(document.getElementById("gravity").value);
        restitution = parseFloat(document.getElementById("restitution").value);
        initialY = parseFloat(document.getElementById("initialHeight").value);
        velocity = 0;
        y = initialY;
        animate();
    }

    let y = 10;
    function updatePhysics() {
        velocity += gravity * timeStep;
        y += velocity * timeStep;

        if (y <= 0) {
            y = 0;
            velocity = -velocity * restitution;
        }
    }

    function drawBall(yMeters) {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        const x = canvas.width / 2;
        const yPixels = canvas.height - yMeters * pixelsPerMeter - radius;
        ctx.beginPath();
        ctx.arc(x, yPixels, radius, 0, Math.PI * 2);
        ctx.fillStyle = "#3498db";
        ctx.fill();
        ctx.closePath();
    }

    function animate() {
        updatePhysics();
        drawBall(y);
        requestAnimationFrame(animate);
    }

    // Start first simulation
    resetSimulation();
</script>
