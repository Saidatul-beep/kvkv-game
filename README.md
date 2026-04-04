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

  // cuba cari suara Melayu / Indonesia
  let voices = speechSynthesis.getVoices();
  let selectedVoice = voices.find(voice => 
    voice.lang.includes("ms") || voice.lang.includes("id")
  );

  if (selectedVoice) {
    msg.voice = selectedVoice;
  }

  msg.lang = "ms-MY";
  msg.pitch = 1;     // nada suara (boleh ubah 0.8 - 1.5)
  msg.rate = 0.9;    // kelajuan (slow sikit, sesuai budak)

  speechSynthesis.speak(msg);
}

function startGame() {
  // start music
  document.getElementById("bgMusic").play();

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
      speak("Tahniah! Pandai! Tepuk tangan untuk diri sendiri");
    } else {
      speak("Cuba lagi");
    }
  };

  recognition.start();
}
</script>

</body><audio id="bgMusic" src="bg-music.mp3" loop autoplay></audio>
</html>
