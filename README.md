<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Casino Plus - Ruleta</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #0b0b0b;
      color: white;
      text-align: center;
      padding-top: 40px;
    }
    .wheel {
      margin: 30px auto;
      width: 300px;
      height: 300px;
      border-radius: 50%;
      border: 10px solid #fff;
      background: radial-gradient(circle, #2e2e2e 0%, #111 70%);
      position: relative;
    }
    #result {
      font-size: 24px;
      margin-top: 20px;
    }
    button {
      margin-top: 20px;
      padding: 10px 20px;
      font-size: 16px;
    }
    input[type=number] {
      padding: 5px;
      width: 80px;
    }
  </style>
</head>
<body>

  <h1>Casino Plus - Ruleta Europea</h1>
  <p>Saldo: $<span id="balance">1000</span></p>
  <p>Tu apuesta: $<input type="number" id="betAmount" value="100" min="1"></p>
  <p>Elige un número (0–36): <input type="number" id="chosenNumber" value="7" min="0" max="36"></p>
  <button onclick="spinWheel()">Girar Ruleta</button>

  <div class="wheel" id="wheel"></div>
  <div id="result"></div>

  <script>
    let balance = 1000;

    function spinWheel() {
      const bet = parseInt(document.getElementById('betAmount').value);
      const chosen = parseInt(document.getElementById('chosenNumber').value);

      if (bet > balance || bet <= 0 || chosen < 0 || chosen > 36) {
        alert("Apuesta inválida.");
        return;
      }

      const result = Math.floor(Math.random() * 37); // 0–36
      const wheel = document.getElementById("wheel");
      const degrees = 360 * 5 + (result * (360 / 37));

      wheel.style.transition = "transform 4s ease-out";
      wheel.style.transform = `rotate(${degrees}deg)`;

      setTimeout(() => {
        let message;
        if (result === chosen) {
          const winnings = bet * 35;
          balance += winnings;
          message = `¡Ganaste! Salió el ${result}. Ganaste $${winnings}`;
        } else {
          balance -= bet;
          message = `Perdiste. Salió el ${result}.`;
        }

        document.getElementById("balance").textContent = balance;
        document.getElementById("result").textContent = message;
      }, 4000);
    }
  </script>

</body>
</html>
