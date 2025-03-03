
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Happy Anniversary</title>
  
  <script src="https://www.youtube.com/iframe_api"></script> <!-- YouTube API -->
  
  <style>
    body {
      margin: 0;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: #ffe6ec;
      font-family: 'Pacifico', cursive, sans-serif;
      text-align: center;
      overflow: hidden;
      position: relative;
      flex-direction: column;
    }

    .heart-container {
      position: relative;
      width: 400px;
      height: 400px;
      cursor: pointer;
      animation: bounce 3s ease-in-out infinite;
    }

    @keyframes bounce {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-5px); }
    }

    .heart-border {
      position: absolute;
      width: 400px;
      height: 400px;
      border: 8px solid transparent;
      clip-path: path("M200 50 C250 0, 400 0, 400 150 C400 300, 200 400, 200 400 C200 400, 0 300, 0 150 C0 0, 150 0, 200 50 Z");
      box-shadow: 0 0 20px rgba(255, 0, 0, 0.7);
      transition: border-color 3s ease-in-out;
    }

    .fill {
      position: absolute;
      top: 100%;
      left: 0;
      width: 400px;
      height: 0;
      background: linear-gradient(45deg, #ff4d4d, #ff0000);
      clip-path: path("M200 50 C250 0, 400 0, 400 150 C400 300, 200 400, 200 400 C200 400, 0 300, 0 150 C0 0, 150 0, 200 50 Z");
      transition: height 6s ease-in-out;
    }

    .click-text {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 1.5rem;
      color: white;
      font-weight: bold;
      animation: blink 1s infinite alternate;
    }

    @keyframes blink {
      0% { opacity: 1; }
      100% { opacity: 0.5; }
    }

    .content-container {
      display: none;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
      padding: 20px;
    }

    .anniversary-text {
  font-size: 4rem;
  font-weight: bold;
  color: #ff66b2; /* Đổi thành màu bạn thích, ví dụ: đỏ hồng */
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 2s ease-out, transform 2s ease-out;
}

    @keyframes gradientText {
      0% { background-position: 0% 50%; }
      50% { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }

    .photo-grid {
      flex: 1;
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 20px;
      opacity: 0;
      transform: translateY(30px);
      transition: opacity 2s ease-out 2s, transform 2s ease-out 2s;
    }

    .photo-frame {
      width: 200px;
      height: 250px;
      border: 8px solid #ff66b2;
      background-color: white;
      box-shadow: 0 0 15px rgba(255, 105, 180, 0.7);
      overflow: hidden;
      border-radius: 15px;
    }

    .photo-frame img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      background-color: #fff;
    }

    .falling-heart {
      position: absolute;
      font-size: 1.5rem;
      animation: fallDown 5s linear infinite;
      opacity: 0.7;
    }

    @keyframes fallDown {
      from { transform: translateY(-10vh); opacity: 1; }
      to { transform: translateY(100vh); opacity: 0; }
    }
  </style>
</head>
<body>

  <div id="player"></div> <!-- YouTube API Player -->

  <div class="heart-container" onclick="fillHeart()">
    <div class="fill" id="fill"></div>
    <div class="heart-border"></div>
    <div class="click-text">Bấm vào đây! 💖</div>
  </div>

  <div class="content-container" id="contentContainer">
    <div class="anniversary-text">Bé iu ơi, chúc mừng sinh nhật! 🎉💖</div>
    <div class="photo-grid">
      <div class="photo-frame"><img src="463908956_1790504155093977_5075643793816551247_n_2.jpg" alt="Ảnh 1"></div>
      <div class="photo-frame"><img src="463952513_1790315671779492_2888170445373960567_n.jpg" alt="Ảnh 2"></div>
      <div class="photo-frame"><img src="464073861_1790316315112761_5703383311592428759_n.jpg" alt="Ảnh 3"></div>
      <div class="photo-frame"><img src="464151436_1790315151779544_5034684494483909960_n.jpg" alt="Ảnh 4"></div>
    </div>
  </div>

  <script>
    let player;

    function onYouTubeIframeAPIReady() {
      player = new YT.Player('player', {
        height: '0',
        width: '0',
        videoId: 'yX4-GIeRBj0',
        playerVars: { 'autoplay': 0, 'loop': 1, 'playlist': 'yX4-GIeRBj0' }
      });
    }

    function fillHeart() {
      const fill = document.getElementById('fill');
      const heartContainer = document.querySelector('.heart-container');
      const contentContainer = document.getElementById('contentContainer');
      const anniversaryText = document.querySelector('.anniversary-text');
      const photoGrid = document.querySelector('.photo-grid');

      fill.style.height = `100%`;
      fill.style.top = `0%`;

      setTimeout(() => {
        heartContainer.style.display = 'none';
        contentContainer.style.display = 'flex';
        anniversaryText.style.opacity = 1;
        anniversaryText.style.transform = 'translateY(0)';
        setTimeout(() => {
          photoGrid.style.opacity = 1;
          photoGrid.style.transform = 'translateY(0)';
        }, 2000);
        player.playVideo();
      }, 6000);
    }
     function createFallingHearts() {
      let heart = document.createElement("div");
      heart.innerHTML = "💖";
      heart.classList.add("falling-heart");
      document.body.appendChild(heart);
      heart.style.left = Math.random() * window.innerWidth + "px";
      setTimeout(() => heart.remove(), 5000);
    }  
    setInterval(createFallingHearts, 500);
  </script>
</body>
</html>

