<!DOCTYPE html>
<html>
<head>
  <title>Game KV+KV Sosial</title>
</head>

<body style="text-align:center; font-family:sans-serif;">

<h1>🎮 Jom Belajar Sosial</h1>

<p id="instruction">Klik butang untuk mula</p>

<button onclick="startGame()">🎤 Mula</button>

<script>
let level = 0;

const tasks = [
  "hai kawan",
  "tolong saya",
  "terima kasih"
];

function startGame() {
  if (level >= tasks.length) {
    alert("🎉 Tahniah! Semua selesai!");
    return;
  }

  let current = tasks[level];
  document.getElementById("instruction").innerHTML = 
    "Sebut: " + current.toUpperCase();

  const recognition = new webkitSpeechRecognition();
  recognition.lang = "ms-MY";

  recognition.onresult = function(event) {
    let speech = event.results[0][0].transcript.toLowerCase();

    if (speech.includes(current)) {
      alert("✅ Betul!");
      level++;
    } else {
      alert("❌ Cuba lagi!");
    }
  };

  recognition.start();
}
</script>

</body>
</html>
