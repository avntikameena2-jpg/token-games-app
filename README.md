<!DOCTYPE html>
<html lang="hi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>50-in-1 Games Hub</title>
  <style>
    body { font-family: sans-serif; background: #121212; color: #fff; margin: 0; padding: 16px; text-align: center; }
    .wallet { background: #1f1f1f; padding: 15px; border-radius: 12px; margin-bottom: 20px; font-size: 20px; font-weight: bold; border: 1px solid #333; }
    .token-count { color: #ffd700; }
    .btn-ad { background: #28a745; color: white; border: none; padding: 8px 16px; border-radius: 6px; font-size: 14px; margin-top: 8px; cursor: pointer; }
    .grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 12px; }
    .card { background: #222; padding: 14px; border-radius: 10px; border: 1px solid #333; }
    .card h3 { margin: 8px 0 4px; font-size: 16px; }
    .card p { margin: 0 0 10px; font-size: 12px; color: #aaa; }
    .play-btn { background: #007bff; color: white; border: none; padding: 8px 14px; border-radius: 6px; font-weight: bold; cursor: pointer; width: 100%; }
  </style>
</head>
<body>

  <div class="wallet">
    टोकन बैलेंस: <span id="token-balance" class="token-count">50</span> 🪙<br>
    <button class="btn-ad" onclick="rewardTokens()">+20 टोकन प्राप्त करें (Watch Ad)</button>
  </div>

  <h2>🎮 50 मिनी गेम्स</h2>
  <div class="grid" id="games-container"></div>

  <script>
    let tokens = parseInt(localStorage.getItem("user_tokens")) || 50;

    function updateWallet() {
      document.getElementById("token-balance").innerText = tokens;
      localStorage.setItem("user_tokens", tokens);
    }

    function rewardTokens() {
      tokens += 20;
      updateWallet();
      alert("बधाई हो! आपको 20 टोकन मिल गए हैं।");
    }

    function launchGame(gameTitle, cost) {
      if (tokens >= cost) {
        tokens -= cost;
        updateWallet();
        alert(gameTitle + " शुरू हो रहा है! 10 टोकन काटे गए।");
        // यहाँ गेम का लिंक लोड होगा
      } else {
        alert("टोकन खत्म हो गए हैं! पहले ऊपर दिए गए बटन से टोकन प्राप्त करें।");
      }
    }

    const container = document.getElementById("games-container");
    for (let i = 1; i <= 50; i++) {
      const card = document.createElement("div");
      card.className = "card";
      card.innerHTML = `
        <h3>गेम #${i}</h3>
        <p>फीस: 10 टोकन</p>
        <button class="play-btn" onclick="launchGame('गेम #' + ${i}, 10)">खेलें</button>
      `;
      container.appendChild(card);
    }

    updateWallet();
  </script>
</body>
</html>
