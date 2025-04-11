---
layout: post
title: Random Lesson Simulation
type: issues
comments: True
permalink: /csp/randomlessonsimulation
---

<style>
    :root {
        --primary-color: #3498db !important;
        --secondary-color: #2ecc71 !important;
        --card-color: #ffffff !important;
        --text-color: #333333 !important;
        --shadow: 0 4px 6px rgba(0, 0, 0, 0.1) !important;
    }

    body {
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif !important;
        background-color: var(--background-color) !important;
        margin: 0 !important;
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
        transition: all 0.3s ease !important;
    }

    h1 {
        color: var(--primary-color) !important;
        text-align: center !important;
        margin-top: 0 !important;
        margin-bottom: 30px !important;
        font-weight: 600 !important;
    }

    .diagram {
        display: flex !important;
        flex-direction: column !important;
        gap: 30px !important;
        align-items: center !important;
    }

    .input-section {
        width: 100% !important;
        background-color: rgba(52, 152, 219, 0.05) !important;
        border-radius: 8px !important;
        padding: 20px !important;
        border: 1px solid rgba(52, 152, 219, 0.2) !important;
    }

    .form-group {
        margin-bottom: 15px !important;
    }

    label {
        display: block !important;
        margin-bottom: 5px !important;
        font-weight: 500 !important;
    }

    input[type="number"], select {
        width: 100% !important;
        padding: 10px !important;
        border: 1px solid #ddd !important;
        border-radius: 4px !important;
        font-size: 16px !important;
    }

    .arrow {
        display: flex !important;
        flex-direction: column !important;
        align-items: center !important;
        position: relative !important;
    }

    .arrow-line {
        width: 4px !important;
        height: 40px !important;
        background-color: var(--primary-color) !important;
    }

    .arrow-head {
        width: 0 !important;
        height: 0 !important;
        border-left: 10px solid transparent !important;
        border-right: 10px solid transparent !important;
        border-top: 15px solid var(--primary-color) !important;
    }

    .process-box {
        display: flex !important;
        justify-content: center !important;
        align-items: center !important;
        width: 200px !important;
        height: 70px !important;
        background-color: var(--primary-color) !important;
        color: white !important;
        border-radius: 8px !important;
        text-align: center !important;
        font-weight: 500 !important;
        box-shadow: var(--shadow) !important;
        position: relative !important;
        overflow: hidden !important;
    }

    .process-box::before {
        content: "" !important;
        position: absolute !important;
        width: 200% !important;
        height: 100% !important;
        background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.2), transparent) !important;
        transform: translateX(-100%) !important;
        animation: shimmer 3s infinite !important;
    }

    @keyframes shimmer {
        100% {
            transform: translateX(100%) !important;
        }
    }

    .output-section {
        width: 100% !important;
        background-color: rgba(46, 204, 113, 0.05) !important;
        border-radius: 8px !important;
        padding: 20px !important;
        text-align: center !important;
        border: 1px solid rgba(46, 204, 113, 0.2) !important;
    }

    .result {
        font-size: 36px !important;
        font-weight: bold !important;
        color: var(--secondary-color) !important;
        margin: 20px 0 !important;
        height: 50px !important;
        display: flex !important;
        align-items: center !important;
        justify-content: center !important;
    }

    .generate-btn {
        background-color: var(--secondary-color) !important;
        color: white !important;
        border: none !important;
        padding: 12px 30px !important;
        font-size: 18px !important;
        border-radius: 6px !important;
        cursor: pointer !important;
        transition: all 0.2s ease !important;
        box-shadow: var(--shadow) !important;
        margin-top: 10px !important;
    }

    .generate-btn:hover {
        background-color: #27ae60 !important;
        transform: translateY(-2px) !important;
        box-shadow: 0 6px 12px rgba(0, 0, 0, 0.15) !important;
    }

    .generate-btn:active {
        transform: translateY(0) !important;
        box-shadow: var(--shadow) !important;
    }

    .history {
        margin-top: 30px !important;
        padding: 15px !important;
        background-color: rgba(0, 0, 0, 0.02) !important;
        border-radius: 8px !important;
        max-height: 150px !important;
        overflow-y: auto !important;
    }

    .history h3 {
        margin-top: 0 !important;
        color: var(--text-color) !important;
        font-size: 18px !important;
        border-bottom: 1px solid #eee !important;
        padding-bottom: 10px !important;
    }

    .history-items {
        display: flex !important;
        flex-wrap: wrap !important;
        gap: 8px !important;
    }

    .history-item {
        background-color: #f1f1f1 !important;
        padding: 5px 10px !important;
        border-radius: 4px !important;
        font-size: 14px !important;
    }

    .distribution-section {
        margin-top: 20px !important;
    }

    .distribution-visual {
        height: 70px !important;
        background-color: #f1f1f1 !important;
        border-radius: 4px !important;
        position: relative !important;
        overflow: hidden !important;
        margin-top: 10px !important;
    }

    .distribution-bar {
        position: absolute !important;
        bottom: 0 !important;
        background-color: rgba(52, 152, 219, 0.7) !important;
        transition: height 0.3s ease, width 0.3s ease !important;
    }

    @media (max-width: 768px) {
        .container {
            padding: 20px 15px !important;
        }
    }
</style>
<div class="container">
    <h1>Interactive Random Number Generator</h1>
    
    <div class="diagram">
        <div class="input-section">
            <div class="form-group">
                <label for="min">Minimum Value:</label>
                <input type="number" id="min" value="1">
            </div>
            <div class="form-group">
                <label for="max">Maximum Value:</label>
                <input type="number" id="max" value="100">
            </div>
            <div class="form-group">
                <label for="distribution">Distribution Type:</label>
                <select id="distribution">
                    <option value="uniform">Uniform (Equal Probability)</option>
                    <option value="gaussian">Gaussian (Normal Distribution)</option>
                    <option value="weighted">Weighted (Lower Values More Likely)</option>
                </select>
            </div>
            <div class="form-group">
                <label for="quantity">Number of Values to Generate:</label>
                <input type="number" id="quantity" value="1" min="1" max="100">
            </div>
        </div>
        
        <div class="arrow">
            <div class="arrow-line"></div>
            <div class="arrow-head"></div>
        </div>
        
        <div class="process-box">
            Random Algorithm
        </div>
        
        <div class="arrow">
            <div class="arrow-line"></div>
            <div class="arrow-head"></div>
        </div>
        
        <div class="output-section">
            <h2>Generated Result</h2>
            <div id="result" class="result">-</div>
            <button id="generate" class="generate-btn">Generate Random Number</button>
            
            <div class="distribution-section">
                <h3>Distribution Visualization</h3>
                <div id="distribution-visual" class="distribution-visual"></div>
            </div>
            
            <div class="history">
                <h3>Generation History</h3>
                <div id="history-items" class="history-items"></div>
            </div>
        </div>
    </div>
</div>

<script>
    document.addEventListener('DOMContentLoaded', function() {
        const minInput = document.getElementById('min');
        const maxInput = document.getElementById('max');
        const distributionSelect = document.getElementById('distribution');
        const quantityInput = document.getElementById('quantity');
        const generateBtn = document.getElementById('generate');
        const resultElement = document.getElementById('result');
        const historyItemsElement = document.getElementById('history-items');
        const distributionVisual = document.getElementById('distribution-visual');
        
        let distributionData = {};
        let history = [];
        
        // Gaussian random number generation (Box-Muller transform)
        function gaussianRandom(min, max) {
            let u = 0, v = 0;
            while(u === 0) u = Math.random();
            while(v === 0) v = Math.random();
            
            // Standard Normal Distribution (mean = 0, std = 1)
            let standard = Math.sqrt(-2.0 * Math.log(u)) * Math.cos(2.0 * Math.PI * v);
            
            // Scale to our desired range
            // Map from [-3, 3] to [min, max]
            standard = Math.min(Math.max(standard, -3), 3); // Clamp to reasonable values
            let scaled = ((standard + 3) / 6) * (max - min) + min;
            
            return Math.round(scaled);
        }
        
        // Weighted random (higher values more likely)
        function weightedRandom(min, max) {
            // Square the random value to bias towards higher numbers
            let r = Math.random();
            r = r * r;  // Square to increase probability of higher values
            return Math.floor(min + r * (max - min + 1));
        }
        
        function generateRandomNumber() {
            const min = parseInt(minInput.value);
            const max = parseInt(maxInput.value);
            const distribution = distributionSelect.value;
            const quantity = parseInt(quantityInput.value);
            
            // Input validation
            if (isNaN(min) || isNaN(max) || min > max) {
                resultElement.textContent = "Error: Invalid range";
                return;
            }
            
            if (isNaN(quantity) || quantity < 1 || quantity > 100) {
                resultElement.textContent = "Error: Invalid quantity";
                return;
            }
            
            // Reset distribution data
            distributionData = {};
            for (let i = min; i <= max; i++) {
                distributionData[i] = 0;
            }
            
            // Generate random numbers
            let results = [];
            for (let i = 0; i < quantity; i++) {
                let randomNum;
                
                switch(distribution) {
                    case 'gaussian':
                        randomNum = gaussianRandom(min, max);
                        break;
                    case 'weighted':
                        randomNum = weightedRandom(min, max);
                        break;
                    case 'uniform':
                    default:
                        randomNum = Math.floor(Math.random() * (max - min + 1)) + min;
                }
                
                // Keep the number within bounds (for gaussian especially)
                randomNum = Math.min(Math.max(randomNum, min), max);
                
                results.push(randomNum);
                
                // Update distribution data
                if (distributionData[randomNum] !== undefined) {
                    distributionData[randomNum]++;
                }
            }
            
            // Update UI
            if (quantity === 1) {
                resultElement.textContent = results[0];
            } else {
                resultElement.textContent = results.join(', ');
            }
            
            // Add to history
            const timestamp = new Date().toLocaleTimeString();
            history.unshift({
                values: results,
                timestamp: timestamp,
                min: min,
                max: max,
                distribution: distribution
            });
            
            // Keep history limited to 10 entries
            if (history.length > 10) {
                history.pop();
            }
            
            updateHistoryUI();
            updateDistributionVisualization();
            
            // Add animation effect
            resultElement.style.animation = 'none';
            setTimeout(() => {
                resultElement.style.animation = 'fadeIn 0.5s';
            }, 10);
        }
        
        function updateHistoryUI() {
            historyItemsElement.innerHTML = '';
            
            history.forEach(entry => {
                const historyItem = document.createElement('div');
                historyItem.className = 'history-item';
                
                if (entry.values.length === 1) {
                    historyItem.textContent = `${entry.values[0]} (${entry.min}-${entry.max})`;
                } else {
                    historyItem.textContent = `[${entry.values.length} values] (${entry.min}-${entry.max})`;
                }
                
                historyItem.title = `Generated at ${entry.timestamp}\nDistribution: ${entry.distribution}\nValues: ${entry.values.join(', ')}`;
                historyItemsElement.appendChild(historyItem);
            });
        }
        
        function updateDistributionVisualization() {
            distributionVisual.innerHTML = '';
            
            // Find the maximum frequency
            const maxFreq = Math.max(...Object.values(distributionData));
            if (maxFreq === 0) return;
            
            // Calculate bar width based on the number of values
            const barWidth = 100 / Object.keys(distributionData).length;
            
            // Create bars
            let i = 0;
            for (const [value, freq] of Object.entries(distributionData)) {
                if (freq > 0) {
                    const bar = document.createElement('div');
                    bar.className = 'distribution-bar';
                    bar.style.left = `${i * barWidth}%`;
                    bar.style.width = `${barWidth}%`;
                    bar.style.height = `${(freq / maxFreq) * 100}%`;
                    bar.title = `Value: ${value}, Count: ${freq}`;
                    distributionVisual.appendChild(bar);
                }
                i++;
            }
        }
        
        // Event listeners
        generateBtn.addEventListener('click', generateRandomNumber);
        
        // Initialize with a random number
        generateRandomNumber();
    });
</script>