<!doctype html>
<html lang="de">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Eine Frage für dich</title>
  <style>
    body {
      margin: 0;
      min-height: 100vh;
      display: grid;
      place-items: center;
      background: #fce4ec;
      font-family: Arial, sans-serif;
      color: #880e4f;
    }
    main {
      width: min(88vw, 480px);
      padding: 28px 20px;
      text-align: center;
      background: #fff8fa;
      border-radius: 22px;
      box-shadow: 0 10px 30px #880e4f24;
    }
    .roses { font-size: 32px; }
    h1 { font-size: clamp(22px, 6vw, 30px); }
    #buttons {
      position: relative;
      height: 130px;
      margin-top: 20px;
    }
    button {
      position: absolute;
      width: 110px;
      height: 48px;
      border: 0;
      border-radius: 12px;
      font-size: 17px;
      cursor: pointer;
    }
    #yes {
      left: 18%;
      top: 40px;
      color: white;
      background: #d81b60;
    }
    #no {
      left: 58%;
      top: 40px;
      color: #880e4f;
      background: #f8bbd0;
      touch-action: manipulation;
    }
  </style>
</head>
<body>
  <main>
    <div class="roses">🌹 💕 🌹</div>
    <p>Eine kleine Frage ...</p>
    <h1>Ist Nur die beste Frau auf der Welt?</h1>
    <div class="roses">🌹</div>

    <div id="buttons">
      <button id="yes">Ja 💖</button>
      <button id="no">Nein</button>
    </div>
  </main>

  <script>
    const area = document.querySelector("#buttons");
    const yes = document.querySelector("#yes");
    const no = document.querySelector("#no");
    let dodges = 0;

    yes.addEventListener("click", () => alert("Ja, ich wusste es *-*!"));
    no.addEventListener("click", () => alert("Alles gut 💕"));

    function moveNo(event) {
      if (dodges >= 20) return;
      if (event.type === "touchstart") event.preventDefault();

      const maxX = area.clientWidth - no.offsetWidth;
      const maxY = area.clientHeight - no.offsetHeight;
      let x, y;

      // Keep Nein from landing on top of Ja.
      do {
        x = Math.random() * maxX;
        y = Math.random() * maxY;
      } while (
        x < yes.offsetLeft + yes.offsetWidth &&
        x + no.offsetWidth > yes.offsetLeft &&
        y < yes.offsetTop + yes.offsetHeight &&
        y + no.offsetHeight > yes.offsetTop
      );

      no.style.left = `${x}px`;
      no.style.top = `${y}px`;
      dodges++;
    }

    no.addEventListener("pointerenter", moveNo);
    no.addEventListener("touchstart", moveNo, { passive: false });
  </script>
</body>
</html>
