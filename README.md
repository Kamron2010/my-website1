<!DOCTYPE html>
<html lang="uz">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>KN COIN</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: #FFEB3B;
      font-family: Arial, sans-serif;
    }
    .coin-container {
      text-align: center;
      position: relative;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    .coin-count {
      font-size: 80px;
      color: #F57C00;
      font-weight: bold;
      margin-bottom: 30px;
    }
    .coin {
      width: 200px;
      height: 200px;
      background-color: #F57C00;
      border-radius: 50%;
      display: flex;
      justify-content: center;
      align-items: center;
      font-size: 40px;
      color: white;
      font-weight: bold;
      cursor: pointer;
      transition: all 0.2s ease;
      position: relative;
      box-shadow: 0 0 30px rgba(245, 124, 0, 0.8), 0 0 60px rgba(245, 124, 0, 0.6);
      animation: glowCoin 1.5s infinite alternate;
      margin: 0 auto;
    }
    .coin:hover {
      transform: scale(1.1);
    }
    .coin-text {
      font-size: 35px;
      color: white;
      font-weight: bold;
      animation: glowText 1.5s infinite alternate;
    }
    .progress-bar-container {
      width: 300px;
      height: 20px;
      background-color: #F5F5F5;
      border-radius: 20px;
      overflow: hidden;
      margin: 30px auto 10px;
      border: 3px solid #F57C00;
    }
    .progress-bar {
      height: 100%;
      background-color: #F57C00;
      width: 100%;
      transition: width 0.2s;
    }
    .energy-text {
      font-size: 14px; /* Kichikroq o'lcham */
      margin-top: 10px;
      color: #333;
      align-self: flex-start;
      margin-left: 30px;
    }
    .auto-clicker-button {
      margin-top: 30px;
      padding: 15px 30px;
      background-color: #FF9800;
      color: white;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      font-size: 22px;
    }
    .auto-clicker-button:disabled {
      background-color: #FFC107;
      cursor: not-allowed;
    }
    @keyframes glowCoin {
      0% {
        box-shadow: 0 0 30px rgba(245, 124, 0, 0.8), 0 0 60px rgba(245, 124, 0, 0.6);
      }
      100% {
        box-shadow: 0 0 50px rgba(245, 124, 0, 1), 0 0 100px rgba(245, 124, 0, 0.8);
      }
    }
    @keyframes glowText {
      0% {
        text-shadow: 0 0 15px rgba(245, 124, 0, 0.8), 0 0 45px rgba(245, 124, 0, 0.6);
      }
      100% {
        text-shadow: 0 0 30px rgba(245, 124, 0, 1), 0 0 60px rgba(245, 124, 0, 0.8);
      }
    }
  </style>
</head>
<body>
<div class="coin-container">
  <div class="coin-count" id="coinCount">0</div>
  <div class="coin" id="coin" onclick="increaseCoin()">
    <span class="coin-text">KN COIN</span>
  </div>
  <div class="progress-bar-container">
    <div class="progress-bar" id="progressBar"></div>
  </div>
  <div class="energy-text" id="energyText">500</div>
  <button class="auto-clicker-button" id="autoClickerButton" onclick="buyAutoClicker()">AutoClicker=500🪙</button>
</div>
<script>
  let coinCount = 0;
  let energy = 500;
  let maxEnergy = 500;
  let autoClickerCost = 500;
  let autoClickerActive = false;
  function increaseCoin() {
    if (energy > 0) {
      coinCount++;
      energy--;
      updateDisplay();
    } else {
      alert('Energiya tugadi!');
    }
  }
  function updateDisplay() {
    document.getElementById('coinCount').innerText = coinCount;
    // Foiz hisoblash va progress barni yangilash
    let energyPercentage = Math.round((energy / maxEnergy) * 100);
    document.getElementById('progressBar').style.width = energyPercentage + '%';
    // Qolgan bosishlar ko'rsatkichi
    document.getElementById('energyText').innerText = `${energy}`;
    if (coinCount >= autoClickerCost) {
      document.getElementById('autoClickerButton').disabled = false;
    } else {
      document.getElementById('autoClickerButton').disabled = true;
    }
  }
  function buyAutoClicker() {
    if (coinCount >= autoClickerCost) {
      coinCount -= autoClickerCost;
      autoClickerActive = true;
      autoClickerCost *= 2;
      updateDisplay();
      startAutoClicker();
    } else {
      alert('Tangalarni sotib olish uchun yetarli miqdorda tanga kerak!');
    }
  }
  function startAutoClicker() {
    if (autoClickerActive) {
      setInterval(() => {
        if (energy > 0) {
          increaseCoin();
        }
      }, 1000); // Auto Clicker har 1 sekundda tanga bosadi
    }
  }
  setInterval(() => {
    if (energy < maxEnergy) {
      energy++;
      updateDisplay();
    }
  }, 1000); // Energiyani 1 sekundda bitta ko'paytirish
</script>
</body>
</html>
