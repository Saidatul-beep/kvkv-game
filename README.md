<!DOCTYPE html>
<html>
<head>
  <title>Game KV+KV Sosial</title>
</head>

<body style="text-align:center; font-family:sans-serif; background-color:#f0f8ff;">

<h1>🛒 Jom Ke Pasaraya!</h1>

<img src="pasaraya-cartoon.png" width="300" style="border-radius:20px;">

<p style="font-size:18px;">Belajar bercakap sambil bermain!</p>

<button onclick="startGame()" style="font-size:20px; padding:10px 20px; border-radius:10px;">
  ▶️ Mula Game
</button>

<br><br>

<div id="game" style="display:none;">

  <h2>Game Pasaraya</h2>

  <img src="baju.png" width="200">

  <p id="instruction"></p>

  <button onclick="startVoice()">🎤 Jawab</button>

  <h2 id="reward" style="display:none;">⭐ ⭐ ⭐</h2>

</div>

<script>
function speak(text) {
  const msg = new SpeechSynthesisUtterance(text);
  msg.lang = "ms-MY";
  speechSynthesis.speak(msg);
}

function startGame() {
  document.getElementById("game").style.display = "block";

  speak("Apa yang awak beli itu");

  document.getElementById("instruction").innerHTML = 
    "Sebut: BAJU";
}

function startVoice() {
  const recognition = new webkitSpeechRecognition();
  recognition.lang = "ms-MY";

  recognition.onresult = function(event) {
    let speech = event.results[0][0].transcript.toLowerCase();

    if (speech.includes("baju")) {
      document.getElementById("reward").style.display = "block";
      speak("Tahniah! Awak betul! Tepuk tangan untuk diri sendiri");
    } else {
      speak("Cuba lagi");
    }
  };

  recognition.start();
}
</script>

</body>
</html>
