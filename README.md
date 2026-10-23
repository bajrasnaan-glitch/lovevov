<!DOCTYPE html>
<html lang="ru">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Для тебя ❤️</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    min-height: 100vh;
    font-family: 'Segoe UI', 'Comic Sans MS', cursive, sans-serif;
    background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 50%, #ffd1dc 100%);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    overflow-x: hidden;
    position: relative;
    padding: 20px;
  }

  /* Летающие сердечки на фоне */
  .heart-bg {
    position: fixed;
    color: rgba(255, 255, 255, 0.6);
    font-size: 24px;
    animation: floatUp linear infinite;
    pointer-events: none;
    z-index: 0;
  }
  @keyframes floatUp {
    0% { transform: translateY(110vh) rotate(0deg); opacity: 0; }
    10% { opacity: 1; }
    90% { opacity: 1; }
    100% { transform: translateY(-10vh) rotate(360deg); opacity: 0; }
  }

  .card {
    position: relative;
    z-index: 2;
    background: rgba(255, 255, 255, 0.85);
    backdrop-filter: blur(10px);
    border-radius: 30px;
    padding: 45px 30px;
    max-width: 650px;
    width: 100%;
    box-shadow: 0 20px 60px rgba(255, 80, 120, 0.35), 0 0 0 3px rgba(255,255,255,0.6) inset;
    text-align: center;
    animation: cardIn 1.2s ease-out;
  }
  @keyframes cardIn {
    from { opacity: 0; transform: translateY(40px) scale(0.95); }
    to { opacity: 1; transform: translateY(0) scale(1); }
  }

  h1 {
    font-size: 2.2em;
    color: #d6336c;
    margin-bottom: 12px;
    text-shadow: 0 2px 8px rgba(255, 150, 180, 0.5);
  }
  .subtitle {
    color: #b0426e;
    font-size: 1.1em;
    margin-bottom: 35px;
    font-style: italic;
  }

  /* Таймер */
  .timer-title {
    font-size: 1.1em;
    color: #a12b5e;
    margin-bottom: 15px;
    font-weight: 600;
  }
  .timer {
    display: flex;
    justify-content: center;
    gap: 12px;
    flex-wrap: wrap;
    margin-bottom: 35px;
  }
  .time-block {
    background: linear-gradient(145deg, #ff6b9d, #d6336c);
    color: #fff;
    border-radius: 16px;
    padding: 15px 10px;
    min-width: 75px;
    box-shadow: 0 6px 18px rgba(214, 51, 108, 0.4), 0 2px 0 rgba(255,255,255,0.4) inset;
  }
  .time-block .num {
    font-size: 1.8em;
    font-weight: 800;
    display: block;
    line-height: 1.1;
    font-variant-numeric: tabular-nums;
  }
  .time-block .label {
    font-size: 0.7em;
    opacity: 0.9;
    text-transform: uppercase;
    letter-spacing: 1px;
  }

  /* Кнопки */
  .btn {
    background: linear-gradient(145deg, #ff6b9d, #d6336c);
    color: #fff;
    border: none;
    border-radius: 50px;
    padding: 15px 35px;
    font-size: 1.1em;
    font-weight: 700;
    cursor: pointer;
    box-shadow: 0 8px 20px rgba(214, 51, 108, 0.45);
    transition: all 0.25s ease;
    font-family: inherit;
  }
  .btn:hover {
    transform: translateY(-3px) scale(1.03);
    box-shadow: 0 12px 28px rgba(214, 51, 108, 0.6);
  }
  .btn:active { transform: translateY(0) scale(0.98); }

  /* Сообщение с милыми словами */
  #loveMessage {
    margin-top: 25px;
    font-size: 1.2em;
    color: #a12b5e;
    min-height: 30px;
    opacity: 0;
    transition: opacity 0.6s ease;
    line-height: 1.5;
    font-weight: 600;
  }
  #loveMessage.show { opacity: 1; }

  /* Финальный вопрос */
  #finalBlock {
    display: none;
    animation: cardIn 0.8s ease-out;
  }
  #finalQuestion {
    font-size: 1.4em;
    color: #d6336c;
    font-weight: 800;
    margin: 20px 0 30px;
    line-height: 1.4;
  }
  .answer-buttons {
    display: flex;
    gap: 20px;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    min-height: 70px;
  }
  #yesBtn {
    background: linear-gradient(145deg, #ff4d88, #c9184a);
    font-size: 1.25em;
    padding: 18px 45px;
    animation: pulse 1.6s infinite;
  }
  @keyframes pulse {
    0%, 100% { box-shadow: 0 8px 20px rgba(214, 51, 108, 0.45); }
    50% { box-shadow: 0 8px 35px rgba(214, 51, 108, 0.9); }
  }
  #noBtn {
    background: linear-gradient(145deg, #b0b0b0, #888);
    box-shadow: 0 8px 20px rgba(100, 100, 100, 0.35);
    font-size: 1em;
    padding: 14px 28px;
    position: relative;
    transition: transform 0.2s ease, left 0.2s ease, top 0.2s ease;
  }

  #successBlock {
    display: none;
    animation: cardIn 0.8s ease-out;
    margin-top: 10px;
  }
  #successBlock .big-heart {
    font-size: 5em;
    animation: heartbeat 1s infinite;
    display: inline-block;
    margin-bottom: 10px;
  }
  @keyframes heartbeat {
    0%, 100% { transform: scale(1); }
    25% { transform: scale(1.15); }
    40% { transform: scale(1); }
    60% { transform: scale(1.1); }
  }
  #successBlock p {
    color: #d6336c;
    font-size: 1.3em;
    font-weight: 700;
    margin-top: 10px;
    line-height: 1.4;
  }

  .hint {
    font-size: 0.9em;
    color: #c96a8d;
    margin-top: 20px;
    font-style: italic;
  }
</style>
</head>
<body>

<!-- Фоновая музыка (если добавите файл music.mp3 рядом с index.html, она заиграет) -->
<audio id="bgMusic" loop>
  <source src="music.mp3" type="audio/mpeg">
</audio>

<div class="card">
  <h1>Моему любимому ❤️</h1>
  <p class="subtitle">Официально мой любимый человек (и по совместительству лучший)</p>

  <!-- Таймер -->
  <p class="timer-title">⏳ Сколько ты меня уже терпишь:</p>
  <div class="timer" id="timer">
    <div class="time-block"><span class="num" id="days">0</span><span class="label">дней</span></div>
    <div class="time-block"><span class="num" id="hours">0</span><span class="label">часов</span></div>
    <div class="time-block"><span class="num" id="minutes">0</span><span class="label">минут</span></div>
    <div class="time-block"><span class="num" id="seconds">0</span><span class="label">секунд</span></div>
  </div>

  <!-- Интерактив -->
  <div id="interactiveBlock">
    <button class="btn" id="loveBtn">Нажми на меня 💌</button>
    <div id="loveMessage"></div>
    <p class="hint" id="hintText">(нажимай, пока не растаешь)</p>
  </div>

  <!-- Финальный вопрос -->
  <div id="finalBlock">
    <p id="finalQuestion">А теперь главный вопрос...<br>Ты будешь моим каблуком? 👠💕</p>
    <div class="answer-buttons">
      <button class="btn" id="yesBtn">Да 💖</button>
      <button class="btn" id="noBtn">Нет</button>
    </div>
  </div>

  <!-- Успех -->
  <div id="successBlock">
    <span class="big-heart">💖</span>
    <p>Я знала! Ты самый лучший каблук на свете!<br>Люблю тебя бесконечно 💕</p>
  </div>
</div>

<script>
  /* ====== МУЗЫКА ====== */
  const bgMusic = document.getElementById('bgMusic');
  
  /* ====== ТАЙМЕР ====== */
  // 23 июня 2026, 01:23 по Новосибирску (UTC+7) => 22 июня 2026 18:23 UTC
  const startDate = new Date(Date.UTC(2026, 5, 22, 18, 23, 0));

  function updateTimer() {
    const now = new Date();
    let diff = now - startDate;
    if (diff < 0) diff = 0;

    const totalSec = Math.floor(diff / 1000);
    const days = Math.floor(totalSec / 86400);
    const hours = Math.floor((totalSec % 86400) / 3600);
    const minutes = Math.floor((totalSec % 3600) / 60);
    const seconds = totalSec % 60;

    document.getElementById('days').textContent = days;
    document.getElementById('hours').textContent = String(hours).padStart(2, '0');
    document.getElementById('minutes').textContent = String(minutes).padStart(2, '0');
    document.getElementById('seconds').textContent = String(seconds).padStart(2, '0');
  }
  updateTimer();
  setInterval(updateTimer, 1000);

  /* ====== ЛЕТАЮЩИЕ СЕРДЕЧКИ ====== */
  const heartChars = ['❤️', '💖', '💕', '💗', '💓', '🩷', '💞'];
  function spawnHeart() {
    const h = document.createElement('div');
    h.className = 'heart-bg';
    h.textContent = heartChars[Math.floor(Math.random() * heartChars.length)];
    h.style.left = Math.random() * 100 + 'vw';
    h.style.fontSize = (16 + Math.random() * 26) + 'px';
    h.style.animationDuration = (8 + Math.random() * 8) + 's';
    h.style.animationDelay = Math.random() * 2 + 's';
    document.body.appendChild(h);
    setTimeout(() => h.remove(), 18000);
  }
  for (let i = 0; i < 15; i++) spawnHeart();
  setInterval(spawnHeart, 1200);

  /* ====== ИНТЕРАКТИВ С МИЛЫМИ СЛОВАМИ ====== */
  const loveMessages = [
    "Ты делаешь мой день ярче ☀️",
    "Люблю тебя пупсик! 💕",
    "Ты мой любимый 💖",
    "Мне так повезло, что ты есть 🥰",
    "Я уже скучаю по нашим обнимашкам 🤗",
    "Я люблю тебя больше, чем шоколадки... а это много ❤️",
    "Ты делаешь меня счастливой каждый день ✨",
    "Спасибо, что терпишь меня 🌞",
    "С тобой я чувствую себя комфортно 🌌💫",
    "Жду нашей встречи 🏡💗"
  ];
  let msgIndex = 0;
  const loveBtn = document.getElementById('loveBtn');
  const loveMessage = document.getElementById('loveMessage');
  const hintText = document.getElementById('hintText');

  loveBtn.addEventListener('click', () => {
    // Включаем музыку при первом клике
    if (bgMusic.paused) {
      bgMusic.volume = 0.5;
      bgMusic.play().catch(() => {});
    }

    loveMessage.textContent = loveMessages[msgIndex % loveMessages.length];
    loveMessage.classList.add('show');
    msgIndex++;

    // Эффект сердечек от кнопки
    for (let i = 0; i < 6; i++) {
      const h = document.createElement('div');
      h.className = 'heart-bg';
      h.textContent = heartChars[Math.floor(Math.random() * heartChars.length)];
      h.style.left = (loveBtn.getBoundingClientRect().left + Math.random() * 120) + 'px';
      h.style.top = (loveBtn.getBoundingClientRect().top) + 'px';
      h.style.animationDuration = (2 + Math.random() * 2) + 's';
      h.style.position = 'fixed';
      h.style.fontSize = (18 + Math.random() * 14) + 'px';
      document.body.appendChild(h);
      setTimeout(() => h.remove(), 4000);
    }

    if (msgIndex >= loveMessages.length) {
      // Показать финальный вопрос
      hintText.style.display = 'none';
      loveBtn.style.display = 'none';
      setTimeout(() => {
        document.getElementById('interactiveBlock').style.display = 'none';
        document.getElementById('finalBlock').style.display = 'block';
      }, 900);
    }
  });

  /* ====== УБЕГАЮЩАЯ КНОПКА "НЕТ" ====== */
  const noBtn = document.getElementById('noBtn');
  const yesBtn = document.getElementById('yesBtn');

  function moveNoBtn() {
    const maxX = window.innerWidth - noBtn.offsetWidth - 20;
    const maxY = window.innerHeight - noBtn.offsetHeight - 20;
    const x = Math.max(10, Math.random() * maxX);
    const y = Math.max(10, Math.random() * maxY);
    noBtn.style.position = 'fixed';
    noBtn.style.left = x + 'px';
    noBtn.style.top = y + 'px';
  }

  noBtn.addEventListener('mouseenter', moveNoBtn);
  noBtn.addEventListener('touchstart', (e) => { e.preventDefault(); moveNoBtn(); }, { passive: false });
  noBtn.addEventListener('click', moveNoBtn);

  /* ====== КНОПКА "ДА" ====== */
  yesBtn.addEventListener('click', () => {
    document.getElementById('finalBlock').style.display = 'none';
    document.getElementById('successBlock').style.display = 'block';

    // Салют из сердечек
    for (let i = 0; i < 60; i++) {
      setTimeout(() => {
        const h = document.createElement('div');
        h.className = 'heart-bg';
        h.textContent = heartChars[Math.floor(Math.random() * heartChars.length)];
        h.style.left = Math.random() * 100 + 'vw';
        h.style.fontSize = (20 + Math.random() * 30) + 'px';
        h.style.animationDuration = (3 + Math.random() * 4) + 's';
        h.style.position = 'fixed';
        document.body.appendChild(h);
        setTimeout(() => h.remove(), 7000);
      }, i * 80);
    }
  });
</script>

</body>
</html>
