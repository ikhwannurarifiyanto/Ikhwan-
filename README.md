<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Autonomous HD Cyber Snake</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }

    body {
      background-color: #0d1117;
      display: flex;
      justify-content: center;
      align-items: center;
      min-height: 100vh;
      overflow: hidden;
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    }

    .container {
      position: relative;
      padding: 4px;
      border-radius: 16px;
      background: linear-gradient(135deg, #00f2fe, #4facfe, #00c6ff);
      box-shadow: 0 0 35px rgba(0, 242, 254, 0.3);
    }

    .canvas-wrapper {
      position: relative;
      background: #0d1117;
      border-radius: 12px;
      overflow: hidden;
    }

    canvas {
      display: block;
      background: radial-gradient(circle at center, #161b22 0%, #0d1117 100%);
    }

    .overlay {
      position: absolute;
      top: 16px;
      left: 20px;
      color: #f0f6fc;
      font-size: 13px;
      letter-spacing: 1.5px;
      text-transform: uppercase;
      font-weight: 600;
      pointer-events: none;
      display: flex;
      align-items: center;
      gap: 10px;
      text-shadow: 0 2px 4px rgba(0,0,0,0.8);
      z-index: 10;
    }

    .badge {
      background: rgba(255, 0, 127, 0.2);
      border: 1px solid rgba(ff, 0, 127, 0.5);
      color: #ff007f;
      padding: 3px 8px;
      border-radius: 6px;
      font-size: 11px;
    }
  </style>
</head>
<body>

  <div class="container">
    <div class="canvas-wrapper">
      <div class="overlay">
        <span>AI Autonomous Snake</span>
        <span class="badge">HARD BOUNDARY</span>
      </div>
      <canvas id="snakeCanvas" width="800" height="400"></canvas>
    </div>
  </div>

  <script>
    const canvas = document.getElementById("snakeCanvas");
    const ctx = canvas.getContext("2d");

    const GRID_SIZE = 20;
    const COLS = canvas.width / GRID_SIZE;
    const ROWS = canvas.height / GRID_SIZE;

    // Batas wilayah gerak Aman (Aman dari Dinding Luar)
    const MIN_X = 1;
    const MAX_X = COLS - 2;
    const MIN_Y = 1;
    const MAX_Y = ROWS - 2;

    let snake = [
      { x: 10, y: 10 },
      { x: 9, y: 10 },
      { x: 8, y: 10 }
    ];

    let dir = { x: 1, y: 0 };
    let food = generateFood();
    let particles = [];

    // Algoritma Penjelajah Aman
    function getNextDirection() {
      const head = snake[0];
      const possibleMoves = [
        { x: 1, y: 0 },
        { x: -1, y: 0 },
        { x: 0, y: 1 },
        { x: 0, y: -1 }
      ];

      // Filter: HANYA BOLEH GERAK DI DALAM AREA SAFE ZONE (MIN_X s/d MAX_X, MIN_Y s/d MAX_Y)
      const validMoves = possibleMoves.filter(move => {
        const nextX = head.x + move.x;
        const nextY = head.y + move.y;

        const isInsideWall = nextX >= MIN_X && nextX <= MAX_X && nextY >= MIN_Y && nextY <= MAX_Y;
        const isSelfCollision = snake.some(segment => segment.x === nextX && segment.y === nextY);

        return isInsideWall && !isSelfCollision;
      });

      // Jika terjebak tanpa opsi aman, terpaksa reset game
      if (validMoves.length === 0) return null;

      // Pilih jalur terdekat menuju makanan
      validMoves.sort((a, b) => {
        const distA = Math.abs((head.x + a.x) - food.x) + Math.abs((head.y + a.y) - food.y);
        const distB = Math.abs((head.x + b.x) - food.x) + Math.abs((head.y + b.y) - food.y);
        return distA - distB;
      });

      return validMoves[0];
    }

    function generateFood() {
      let newFood;
      while (!newFood || snake.some(segment => segment.x === newFood.x && segment.y === newFood.y)) {
        newFood = {
          x: Math.floor(Math.random() * (MAX_X - MIN_X + 1)) + MIN_X,
          y: Math.floor(Math.random() * (MAX_Y - MIN_Y + 1)) + MIN_Y
        };
      }
      return newFood;
    }

    function createParticles(x, y) {
      for (let i = 0; i < 12; i++) {
        particles.push({
          x: x * GRID_SIZE + GRID_SIZE / 2,
          y: y * GRID_SIZE + GRID_SIZE / 2,
          vx: (Math.random() - 0.5) * 4,
          vy: (Math.random() - 0.5) * 4,
          alpha: 1,
          size: Math.random() * 3 + 1
        });
      }
    }

    function resetGame() {
      snake = [
        { x: 10, y: 10 },
        { x: 9, y: 10 },
        { x: 8, y: 10 }
      ];
      dir = { x: 1, y: 0 };
      food = generateFood();
    }

    function update() {
      const nextDir = getNextDirection();

      // Reset jika AI terpojok / menabrak
      if (!nextDir) {
        resetGame();
        return;
      }

      dir = nextDir;
      const head = { x: snake[0].x + dir.x, y: snake[0].y + dir.y };

      snake.unshift(head);

      // Cek Makan Makanan
      if (head.x === food.x && head.y === food.y) {
        createParticles(food.x, food.y);
        food = generateFood();
      } else {
        snake.pop();
      }

      // Update Efek Partikel
      particles.forEach((p, index) => {
        p.x += p.vx;
        p.y += p.vy;
        p.alpha -= 0.03;
        if (p.alpha <= 0) particles.splice(index, 1);
      });
    }

    function drawWalls() {
      // Draw Dinding Penghalang Padat (Solid Wall Blocks)
      ctx.fillStyle = "rgba(255, 0, 127, 0.15)";
      ctx.strokeStyle = "#ff007f";
      ctx.lineWidth = 2;

      // Gambar Blok Dinding Luar
      for (let x = 0; x < COLS; x++) {
        for (let y = 0; y < ROWS; y++) {
          if (x < MIN_X || x > MAX_X || y < MIN_Y || y > MAX_Y) {
            ctx.fillRect(x * GRID_SIZE, y * GRID_SIZE, GRID_SIZE, GRID_SIZE);
          }
        }
      }

      // Garis Neon Pembatas Dalam
      ctx.save();
      ctx.shadowBlur = 12;
      ctx.shadowColor = "#ff007f";
      ctx.strokeRect(
        MIN_X * GRID_SIZE,
        MIN_Y * GRID_SIZE,
        (MAX_X - MIN_X + 1) * GRID_SIZE,
        (MAX_Y - MIN_Y + 1) * GRID_SIZE
      );
      ctx.restore();
    }

    function drawGrid() {
      ctx.strokeStyle = "rgba(255, 255, 255, 0.02)";
      ctx.lineWidth = 1;
      for (let x = MIN_X * GRID_SIZE; x <= (MAX_X + 1) * GRID_SIZE; x += GRID_SIZE) {
        ctx.beginPath();
        ctx.moveTo(x, MIN_Y * GRID_SIZE);
        ctx.lineTo(x, (MAX_Y + 1) * GRID_SIZE);
        ctx.stroke();
      }
      for (let y = MIN_Y * GRID_SIZE; y <= (MAX_Y + 1) * GRID_SIZE; y += GRID_SIZE) {
        ctx.beginPath();
        ctx.moveTo(MIN_X * GRID_SIZE, y);
        ctx.lineTo((MAX_X + 1) * GRID_SIZE, y);
        ctx.stroke();
      }
    }

    function draw() {
      ctx.fillStyle = "#0d1117";
      ctx.fillRect(0, 0, canvas.width, canvas.height);

      drawGrid();
      drawWalls();

      // Draw Partikel
      particles.forEach(p => {
        ctx.save();
        ctx.globalAlpha = p.alpha;
        ctx.fillStyle = "#00f2fe";
        ctx.shadowBlur = 10;
        ctx.shadowColor = "#00f2fe";
        ctx.beginPath();
        ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
        ctx.fill();
        ctx.restore();
      });

      // Draw Makanan (Pink Glowing Orb)
      ctx.save();
      ctx.fillStyle = "#ff007f";
      ctx.shadowBlur = 15;
      ctx.shadowColor = "#ff007f";
      ctx.beginPath();
      ctx.arc(
        food.x * GRID_SIZE + GRID_SIZE / 2,
        food.y * GRID_SIZE + GRID_SIZE / 2,
        GRID_SIZE / 2.8,
        0,
        Math.PI * 2
      );
      ctx.fill();
      ctx.restore();

      // Draw Ular (Gradient Blue-Cyan)
      snake.forEach((segment, index) => {
        ctx.save();
        
        const progress = index / snake.length;
        const color = index === 0 ? "#00f2fe" : `hsl(${190 + progress * 50}, 100%, 50%)`;
        
        ctx.fillStyle = color;
        ctx.shadowBlur = index === 0 ? 12 : 4;
        ctx.shadowColor = "#00f2fe";

        const x = segment.x * GRID_SIZE + 1;
        const y = segment.y * GRID_SIZE + 1;
        const size = GRID_SIZE - 2;
        const radius = index === 0 ? 6 : 4;

        ctx.beginPath();
        ctx.roundRect(x, y, size, size, radius);
        ctx.fill();

        ctx.restore();
      });
    }

    // Interval Kecepatan Gerak (80ms)
    setInterval(() => {
      update();
      draw();
    }, 80);
  </script>
</body>
</html>
