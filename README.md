<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>G-Loop</title>

<style>
body {
  margin:0;
  font-family: Arial, sans-serif;
  background:#000;
  color:#fff;
  text-align:center;
}

h1 { font-size:3rem; }
p { color:#aaa; }

button {
  padding:10px 20px;
  border:none;
  border-radius:20px;
  cursor:pointer;
  margin:5px;
}

.primary {
  background:#00BFFF;
  color:#fff;
  box-shadow:0 0 15px #00BFFF;
}

.love { background:#ff2d55; color:#fff; }
.dislike { background:#555; color:#fff; }

.container { padding:40px 20px; }

/* glowing ring */
.ring {
  width:200px;
  height:200px;
  border:4px solid #00BFFF;
  border-radius:50%;
  margin:20px auto;
  box-shadow:0 0 20px #00BFFF;
  animation: spin 10s linear infinite;
}

@keyframes spin {
  0% { transform:rotate(0); }
  100% { transform:rotate(360deg); }
}

/* post card */
.post {
  background:#111;
  padding:20px;
  border-radius:15px;
  margin:20px auto;
  width:300px;
}

iframe {
  width:90%;
  height:300px;
  border:none;
  border-radius:10px;
}
</style>

</head>
<body>

<!-- HERO -->
<div class="container">
  <div class="ring"></div>
  <h1>G-Loop</h1>
  <p>One World. One Loop.</p>

  <button class="primary" onclick="scrollToLive()">Go Live</button>
</div>

<!-- LIVE STREAM -->
<div class="container" id="live">
  <h2>🔴 Live Now</h2>

  <!-- 🔥 REPLACE VIDEO ID -->
  <iframe src="https://www.youtube.com/embed/live_stream?channel=YOUR_CHANNEL_ID"></iframe>
</div>

<!-- SOCIAL POST -->
<div class="container">
  <h2>Social Feed</h2>

  <div class="post">
    <p>🌍 Welcome to G-Loop — Go Live & Connect!</p>

    <button class="love" onclick="love()">❤️ Love <span id="loveCount">0</span></button>
    <button class="dislike" onclick="dislike()">👎 Dislike <span id="dislikeCount">0</span></button>

    <br><br>

    <button onclick="message()">💬 Message</button>
  </div>
</div>

<!-- EMAIL -->
<div class="container">
  <h2>Stay in the Loop</h2>
  <input id="email" placeholder="Enter email" style="padding:10px;border-radius:20px;border:none;">
  <button class="primary" onclick="saveEmail()">Join</button>
</div>

<script>
let loveCount = 0;
let dislikeCount = 0;

function love() {
  loveCount++;
  document.getElementById("loveCount").innerText = loveCount;
}

function dislike() {
  dislikeCount++;
  document.getElementById("dislikeCount").innerText = dislikeCount;
}

function message() {
  window.open("https://wa.me/64204203785", "_blank");
}

function saveEmail() {
  let email = document.getElementById("email").value;
  alert("Saved: " + email);
}

function scrollToLive() {
  document.getElementById("live").scrollIntoView({ behavior: 'smooth' });
}
</script>

</body>
</html>
