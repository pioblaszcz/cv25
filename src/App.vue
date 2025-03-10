<script setup>
import "./style.css";

(function () {
  let loadedImages = 0;
  let totalImages = document.images.length;
  let checkInterval;

  function getResourceProgress() {
    const resources = performance.getEntriesByType("resource");
    const total = resources.length;
    let loaded = 0;

    if (total === 0) return 100;

    resources.forEach((resource) => {
      if (resource.responseEnd) loaded++;
    });

    return Math.round((loaded / total) * 100);
  }

  function getDocumentProgress() {
    if (document.readyState === "loading") return 25;
    if (document.readyState === "interactive") return 75;
    if (document.readyState === "complete") return 100;
    return 0;
  }

  function getImageProgress() {
    if (totalImages === 0) return 100;
    return Math.round((loadedImages / totalImages) * 100);
  }

  function calculateOverallProgress() {
    let docProgress = getDocumentProgress();
    let resProgress = getResourceProgress();
    let imgProgress = getImageProgress();

    let overallProgress = Math.round(
      docProgress * 0.4 + resProgress * 0.4 + imgProgress * 0.2
    );

    updatePreloader(overallProgress);
    return overallProgress;
  }

  function trackImageLoading() {
    if (totalImages === 0) return;

    Array.from(document.images).forEach((img) => {
      if (img.complete) {
        loadedImages++;
      } else {
        img.addEventListener("load", () => {
          loadedImages++;
        });
        img.addEventListener("error", () => {
          loadedImages++;
        });
      }
    });
  }

  document.onreadystatechange = function () {
    calculateOverallProgress();
  };

  window.addEventListener("DOMContentLoaded", () => {
    trackImageLoading();
    calculateOverallProgress();
  });

  window.addEventListener("load", () => {
    calculateOverallProgress();
    clearInterval(checkInterval);
    removePreloader();
  });

  checkInterval = setInterval(() => {
    let progress = calculateOverallProgress();
    if (progress >= 100) {
      removePreloader();
      clearInterval(checkInterval);
    }
  }, 100);
})();

function updatePreloader(value) {
  if (typeof value !== "number" || value < 0 || value > 100) {
    console.error("Value must be an integer between 0 and 100.");
    return;
  }

  let onesTranslation = value * -2; // Ones place moves -2ch per percent
  let tensTranslation = Math.floor(value / 10) * -2; // Tens place moves -2ch per 10%
  let hundredsTranslation = Math.floor(value / 100) * -2; // Hundreds place moves -2ch per 100%

  document.querySelector(
    "#number-track-100"
  ).style.transform = `translateY(${hundredsTranslation}ch)`;
  document.querySelector(
    "#number-track-10"
  ).style.transform = `translateY(${tensTranslation}ch)`;
  document.querySelector(
    "#number-track-1"
  ).style.transform = `translateY(${onesTranslation}ch)`;
}

function removePreloader() {
  setTimeout(() => {
    document.querySelector("p").style.transform = "scale(1.2)";
    setTimeout(() => {
      const tracks = document.querySelectorAll("#preloader > p > span");
      tracks.forEach((track, index) => {
        setTimeout(() => {
          let currentTransform = track.style.transform || "translateY(0ch)";
          let currentY = parseFloat(currentTransform.match(/-?\d+/)) || 0;
          track.style.transform = `translateY(${currentY - 2}ch)`;
        }, index * 50);
      });
    }, 700);
  }, 1000);

  setTimeout(() => {
    document.querySelector("#preloader").style.opacity = 0;
    setTimeout(() => {
      document.querySelector("#preloader").remove();
    }, 1000);
  }, 3700);
}
</script>

<template>
  <div id="preloader">
    <p>
      <span class="number-track">​ w</span>
      <span class="number-track">​ e</span>
      <span class="number-track" id="number-track-100"> 0 1 l </span>
      <span class="number-track" id="number-track-10">
        0 1 2 3 4 5 6 7 8 9 0 c
      </span>
      <span class="number-track" id="number-track-1">
        0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5
        6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
        2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 o
      </span>
      <span class="number-track">​ m</span>
      <span class="number-track">​ e</span>
    </p>
  </div>
  <router-view />
</template>

<style scoped lang="scss">
@import url("https://fonts.googleapis.com/css2?family=JetBrains+Mono:ital,wght@0,100..800;1,100..800&display=swap");

#preloader {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100vw;
  height: 100vh;
  overflow: none;
  background-color: #030303;
  position: fixed;
  transition: 0.5s cubic-bezier(0.65, 0.05, 0, 1) opacity;
  z-index: 9999;
  top: 0;
  left: 0;
}

p {
  font-family: "JetBrains Mono", serif;
  font-optical-sizing: auto;
  font-weight: 200;
  font-style: normal;
  font-size: 8vh;
  display: flex;
  justify-content: center;
  flex-direction: row;
  height: 2ch;
  line-height: 2ch;
  overflow: clip;
  color: white;
  transition: 1.6s cubic-bezier(0.65, 0.05, 0, 1) transform;

  @media screen and (max-width: 768px) {
    font-size: 6vh;
  }
}

.number-track {
  width: 1ch;
  transition: 1.8s cubic-bezier(0.65, 0.05, 0, 1) transform;
  pointer-events: none;
  user-select: none;
}
</style>
