<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>New Year 2026 ✨</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background: linear-gradient(120deg, #0f2027, #203a43, #2c5364);
      color: white;
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      text-align: center;
    }

    .card {
      background: rgba(255, 255, 255, 0.1);
      padding: 40px;
      border-radius: 20px;
      box-shadow: 0 0 40px rgba(255,255,255,0.2);
      max-width: 500px;
    }

    h1 {
      font-size: 3em;
      margin-bottom: 10px;
      text-shadow: 0 0 15px #ffd700;
    }

    h2 {
      font-weight: 300;
      margin-bottom: 30px;
      opacity: 0.9;
    }

    .countdown {
      font-size: 2em;
      letter-spacing: 2px;
      margin-bottom: 30px;
    }

    button {
      background: #ffd700;
      color: #000;
      border: none;
      padding: 12px 25px;
      border-radius: 25px;
      font-size: 1em;
      cursor: pointer;
      transition: transform 0.2s, box-shadow 0.2s;
    }

    button:hover {
      transform: scale(1.05);
      box-shadow: 0 0 15px #ffd700;
    }

    footer {
      margin-top: 25px;
      font-size: 0.8em;
      opacity: 0.7;
    }
  </style>
</head>
<body>

  <div class="card">
    <h1>✨ Happy New Year ✨</h1>
    <h2>New year. New chances. New mindset.</h2>

    <div class="countdown" id="countdown">
      Loading countdown...
    </div>

    <button onclick="alert('Make this year count 🚀')">
      Start Fresh
    </button>

    <footer>
      © 2026 • Made by Dea
    </footer>
  </div>

  <script>
    const countdownEl = document.getElementById("countdown");
    const newYear = new Date("January 1, 2026 00:00:00").getTime();

    setInterval(() => {
      const now = new Date().getTime();
      const diff = newYear - now;

      if (diff <= 0) {
        countdownEl.innerHTML = "🎉 It's the New Year!";
        return;
      }

      const days = Math.floor(diff / (1000 * 60 * 60 * 24));
      const hours = Math.floor((diff / (1000 * 60 * 60)) % 24);
      const minutes = Math.floor((diff / (1000 * 60)) % 60);
      const seconds = Math.floor((diff / 1000) % 60);

      countdownEl.innerHTML =
        `${days}d ${hours}h ${minutes}m ${seconds}s`;
    }, 1000);
  </script>

</body>
</html>

