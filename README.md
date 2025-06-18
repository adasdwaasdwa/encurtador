<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Botão com Chuva</title>
  <style>
    body {
      margin: 0;
      overflow: hidden;
      background: black;
    }

    canvas {
      position: fixed;
      top: 0;
      left: 0;
      z-index: 0;
    }

    #meuBotao {
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      z-index: 1;
      padding: 15px 30px;
      background-color: #4CAF50;
      color: white;
      border: none;
      border-radius: 10px;
      font-size: 18px;
      cursor: pointer;
      transition: transform 0.3s, opacity 0.3s;
    }

    #meuBotao.animar {
      transform: scale(0.9);
      opacity: 0.5;
    }
  </style>
</head>
<body>

  <canvas id="chuvaCanvas"></canvas>
  <button id="meuBotao">Clique aqui</button>

  <script>
    // BOTÃO
    const botao = document.getElementById('meuBotao');
    botao.addEventListener('click', () => {
      botao.classList.add('animar');
      setTimeout(() => {
        window.location.href = 'https://google.com'; // Coloque seu link aqui
      }, 300);
    });

    // CHUVA
    const canvas = document.getElementById('chuvaCanvas');
    const ctx = canvas.getContext('2d');
    let width = canvas.width = window.innerWidth;
    let height = canvas.height = window.innerHeight;

    let mouseX = width / 2;

    const raindrops = [];
    const maxDrops = 300;

    for (let i = 0; i < maxDrops; i++) {
      raindrops.push({
        x: Math.random() * width,
        y: Math.random() * height,
        length: Math.random() * 20 + 10,
        speed: Math.random() * 4 + 2
      });
    }

    function drawRain() {
      ctx.clearRect(0, 0, width, height);
      ctx.strokeStyle = 'rgba(173, 216, 230, 0.6)';
      ctx.lineWidth = 1.5;

      for (let drop of raindrops) {
        ctx.beginPath();
        ctx.moveTo(drop.x, drop.y);
        ctx.lineTo(drop.x + (mouseX - width / 2) * 0.002, drop.y + drop.length);
        ctx.stroke();

        drop.y += drop.speed;

        if (drop.y > height) {
          drop.y = -drop.length;
          drop.x = Math.random() * width;
        }
      }

      requestAnimationFrame(drawRain);
    }

    drawRain();

    window.addEventListener('resize', () => {
      width = canvas.width = window.innerWidth;
      height = canvas.height = window.innerHeight;
    });

    window.addEventListener('mousemove', (e) => {
      mouseX = e.clientX;
    });
  </script>

</body>
</html>
