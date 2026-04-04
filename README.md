<!DOCTYPE html>
<html>
<head>
  <title>Game KV+KV Sosial</title>
  <style>
    body {
      text-align: center;
      font-family: sans-serif;
      background-color: #f0f8ff;
    }
    button {
      font-size: 20px;
      padding: 10px 20px;
      border-radius: 10px;
      cursor: pointer;
    }
    img {
      border-radius: 20px;
    }
    #reward {
      display: none;
      font-size: 30px;
      color: gold;
      margin-top: 15px;
      animation: bounce 1s ease;
    }
    @keyframes bounce {
      0% {transform: scale(1);}
      50% {transform: scale(1.5);}
      100% {transform: scale(1);}
    }
    #game {
      display: none;
    }
  </style>
</head>

<body>

<h1>🛒 Jom Ke Pasaraya!</h1>
<img src="pasaraya-cartoon.png" width="300">
<p style="font-size:18px;">Belajar bercakap sambil bermain!</p>

<button onclick="startGame()">▶️ Mula Game</button>

<div id="game">
  <h2>Game Pasaraya</h2>
  <img id="itemImage" src="" width="200">
  <p id="instruction"></p>
  <button onclick="startVoice()">🎤 Jawab</button>
  <h2 id="reward">⭐ ⭐ ⭐</h2>
</div>

<audio id="bgMusic" src="bg-music.mp3" loop></audio>

<script>
  // ===== BACKGROUND MUSIC =====
  const bgMusic = document.getElementById("bgMusic");
  bgMusic.volume = 0.2; // lembut

  // ===== ITEM LIST =====
  const items = [
    {name:"susu", image:"susu.png"},
    {name:"bola", image:"bola.png"},
    {name:"meja", image:"meja.png"},
    {name:"buku", image:"buku.png"},
    {name:"roti", image:"roti.png"},
    {name:"labu", image:"labu.png"},
    {name:"jeli", image:"jeli.png"},
    {name:"kopi", image:"kopi.png"}
  ];

  let currentItem = 0;

  // ===== SUARA DALAM BAHASA MELAYU =====
  function speak(text) {
    const msg = new SpeechSynthesisUtterance(text);
    let voices = speechSynthesis.getVoices();
    let selectedVoice = voices.find(v => v.lang.includes("ms") || v.lang.includes("id"));
    if(selectedVoice) msg.voice = selectedVoice;
    msg.lang = "ms-MY";
    msg.pitch = 1;
    msg.rate = 0.9;
    speechSynthesis.speak(msg);
  }

  // ===== START GAME =====
  function startGame() {
    bgMusic.play(); // mula music
    document.getElementById("game").style.display = "block";
    showItem();
  }

  // ===== SHOW ITEM =====
  function showItem() {
    if(currentItem >= items.length) {
      speak("Tahniah! Semua item selesai!");
      document.getElementById("instruction").innerHTML = "🎉 Semua selesai!";
      document.getElementById("itemImage").style.display = "none";
      return;
    }
    const item = items[currentItem];
    document.getElementById("itemImage").src = item.image;
    document.getElementById("reward").style.display = "none";
    document.getElementById("instruction").innerHTML = "Sebut: " + item.name.toUpperCase();
    speak("Apa yang awak beli itu?");
  }

  // ===== MIC & CHECK ANSWER =====
  function startVoice() {
    const recognition = new webkitSpeechRecognition();
    recognition.lang = "ms-MY";
    recognition.onresult = function(event) {
      let speech = event.results[0][0].transcript.toLowerCase();
      const itemName = items[currentItem].name;
      if (speech.includes(itemName)) {
        document.getElementById("reward").style.display = "block";
        speak("Tahniah! Awak betul! Tepuk tangan untuk diri sendiri");
        currentItem++;
        setTimeout(showItem, 2000); // pergi item seterusnya selepas 2 saat
      } else {
        speak("Cuba lagi");
      }
    };
    recognition.start();
  }
</script>

</body>
</html>
