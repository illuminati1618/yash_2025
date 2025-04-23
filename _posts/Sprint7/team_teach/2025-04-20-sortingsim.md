---
layout: post
title: Sorting Sim
type: issues
comments: True
permalink: /csp/sortingsim
---

<style>
  body {
    font-family: sans-serif;
    background-color: #1e1e2f;
    color: #eee;
    text-align: center;
    margin: 0;
    padding: 20px;
  }
  canvas {
    background: #2e2e3e;
    display: block;
    margin: 20px auto;
    border-radius: 8px;
  }
  button, select {
    margin: 10px;
    padding: 10px 20px;
    font-size: 16px;
    background-color: #3498db;
    border: none;
    border-radius: 5px;
    color: white;
    cursor: pointer;
  }
  button:hover {
    background-color: #2980b9;
  }
</style>

<h1>Sorting Algorithm Speed Simulator</h1>
<select id="algorithm">
  <option value="bubble">Bubble Sort</option>
  <option value="merge">Merge Sort</option>
  <option value="selection">Selection Sort</option>
  <option value="insertion">Insertion Sort</option>
  <option value="quick">Quick Sort</option>
</select>
<button onclick="startSimulation()">Run Sort</button>
<button onclick="shuffleArray()">Shuffle</button>
<canvas id="canvas" width="800" height="400"></canvas>

<script>
  const canvas = document.getElementById("canvas");
  const ctx = canvas.getContext("2d");
  let array = [];
  const size = 100;

  function generateArray() {
    array = Array.from({ length: size }, (_, i) => i + 1);
    shuffleArray();
  }

  function shuffleArray() {
    for (let i = array.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [array[i], array[j]] = [array[j], array[i]];
    }
    drawArray();
  }

  function drawArray(highlight = -1) {
    ctx.clearRect(0, 0, canvas.width, canvas.height);
    const barWidth = canvas.width / size;
    for (let i = 0; i < size; i++) {
      ctx.fillStyle = i === highlight ? "#e74c3c" : "#1abc9c";
      const height = (array[i] / size) * canvas.height;
      ctx.fillRect(i * barWidth, canvas.height - height, barWidth - 1, height);
    }
  }

  async function startSimulation() {
    const algo = document.getElementById("algorithm").value;
    if (algo === "bubble") await bubbleSort();
    else if (algo === "merge") await mergeSortWrapper();
    else if (algo === "selection") await selectionSort();
    else if (algo === "insertion") await insertionSort();
    else if (algo === "quick") await quickSortWrapper();
    drawArray();
  }

  async function bubbleSort() {
    for (let i = 0; i < array.length; i++) {
      for (let j = 0; j < array.length - i - 1; j++) {
        if (array[j] > array[j + 1]) {
          [array[j], array[j + 1]] = [array[j + 1], array[j]];
          drawArray(j);
          await sleep(2);
        }
      }
    }
  }

  async function selectionSort() {
    for (let i = 0; i < array.length; i++) {
      let minIdx = i;
      for (let j = i + 1; j < array.length; j++) {
        if (array[j] < array[minIdx]) minIdx = j;
      }
      [array[i], array[minIdx]] = [array[minIdx], array[i]];
      drawArray(i);
      await sleep(10);
    }
  }

  async function insertionSort() {
    for (let i = 1; i < array.length; i++) {
      let key = array[i];
      let j = i - 1;
      while (j >= 0 && array[j] > key) {
        array[j + 1] = array[j];
        drawArray(j);
        await sleep(5);
        j--;
      }
      array[j + 1] = key;
    }
  }

  async function mergeSortWrapper() {
    await mergeSort(array, 0, array.length - 1);
  }

  async function mergeSort(arr, left, right) {
    if (left >= right) return;
    const mid = Math.floor((left + right) / 2);
    await mergeSort(arr, left, mid);
    await mergeSort(arr, mid + 1, right);
    await merge(arr, left, mid, right);
  }

  async function merge(arr, left, mid, right) {
    const leftArr = arr.slice(left, mid + 1);
    const rightArr = arr.slice(mid + 1, right + 1);
    let i = 0, j = 0, k = left;

    while (i < leftArr.length && j < rightArr.length) {
      arr[k++] = leftArr[i] <= rightArr[j] ? leftArr[i++] : rightArr[j++];
      drawArray(k);
      await sleep(2);
    }
    while (i < leftArr.length) {
      arr[k++] = leftArr[i++];
      drawArray(k);
      await sleep(2);
    }
    while (j < rightArr.length) {
      arr[k++] = rightArr[j++];
      drawArray(k);
      await sleep(2);
    }
  }

  async function quickSortWrapper() {
    await quickSort(0, array.length - 1);
  }

  async function quickSort(low, high) {
    if (low < high) {
      let pi = await partition(low, high);
      await quickSort(low, pi - 1);
      await quickSort(pi + 1, high);
    }
  }

  async function partition(low, high) {
    let pivot = array[high];
    let i = low - 1;
    for (let j = low; j < high; j++) {
      if (array[j] < pivot) {
        i++;
        [array[i], array[j]] = [array[j], array[i]];
        drawArray(j);
        await sleep(2);
      }
    }
    [array[i + 1], array[high]] = [array[high], array[i + 1]];
    drawArray(i + 1);
    await sleep(2);
    return i + 1;
  }

  function sleep(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
  }

  generateArray();
</script>
