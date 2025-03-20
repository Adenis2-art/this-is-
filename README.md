<!DOCTYPE html>
<html lang="uk">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Клікер-гра</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; }
        .container { display: flex; justify-content: space-around; margin-top: 50px; }
        .panel { border: 2px solid black; padding: 20px; width: 200px; }
        button { margin-top: 10px; padding: 10px; cursor: pointer; }
    </style>
</head>
<body>
    <h1>Клікер-гра</h1>
    <div class="container">
        <div class="panel">
            <h2>Поінти: <span id="points">0</span> <span id="perSec"></span></h2>
            <button onclick="clickButton()">Клік!</button>
        </div>
        <div class="panel">
            <h2>Апгрейди</h2>
            <button onclick="buyUpgrade(1)">+1 до кліка (10 поінтів)</button>
            <button onclick="buyUpgrade(2)">Х2 кліків (100 поінтів)</button>
            <button onclick="buyUpgrade(3)">+1 поінт/с (50 поінтів)</button>
        </div>
    </div>
    
    <script>
        let points = 0;
        let clickValue = 1;
        let multiplier = 1;
        let autoPoints = 0;
        let upgradeCosts = { 1: 10, 2: 100, 3: 50 };
        
        function updateUI() {
            document.getElementById("points").textContent = points;
            document.getElementById("perSec").textContent = autoPoints > 0 ? `(+${autoPoints} p/s)` : "";
        }
        
        function clickButton() {
            points += clickValue * multiplier;
            updateUI();
        }
        
        function buyUpgrade(type) {
            if (points >= upgradeCosts[type]) {
                points -= upgradeCosts[type];
                
                if (type === 1) {
                    clickValue += 1;
                    upgradeCosts[1] = Math.floor(upgradeCosts[1] * 1.5);
                } 
                else if (type === 2) {
                    multiplier *= 2;
                    upgradeCosts[2] *= 5;
                } 
                else if (type === 3) {
                    autoPoints += 1;
                    upgradeCosts[3] = Math.floor(upgradeCosts[3] * 1.1);
                    if (autoPoints === 1) setInterval(() => { points += autoPoints; updateUI(); }, 1000);
                }
                
                updateUI();
            }
        }
        
        updateUI();
    </script>
</body>
</html>
