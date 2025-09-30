<canvas id="scene" width="800" height="500" style="border:1px solid #000;"></canvas>

<script>
const canvas = document.getElementById("scene");
const ctx = canvas.getContext("2d");

let sunX = 650;  // ตำแหน่งเริ่มต้นของพระอาทิตย์
let sunY = 100;
let sunR = 50;
let dx = 6;      // ความเร็ว (px ต่อเฟรม)

function drawScene() {
 
  // 1. ท้องฟ้า
  const sky = ctx.createLinearGradient(0, 0, 0, 300);
  sky.addColorStop(0, "#87CEEB");
  sky.addColorStop(1, "#ffffff");
  ctx.fillStyle = sky;
  ctx.fillRect(0, 0, 800, 500);

  // 2. ภูเขา
  ctx.beginPath();
  ctx.moveTo(0, 300);
  ctx.lineTo(150, 150);
  ctx.lineTo(300, 300);
  ctx.closePath();
  ctx.fillStyle = "#556B2F";
  ctx.fill();

  ctx.beginPath();
  ctx.moveTo(200, 300);
  ctx.lineTo(400, 100);
  ctx.lineTo(600, 300);
  ctx.closePath();
  ctx.fillStyle = "#6B8E23";
  ctx.fill();

  ctx.beginPath();
  ctx.moveTo(500, 300);
  ctx.lineTo(700, 180);
  ctx.lineTo(800, 300);
  ctx.closePath();
  ctx.fillStyle = "#2E8B57";
  ctx.fill();

  // 3. พระอาทิตย์ (เคลื่อนไหว)
  ctx.beginPath();
  ctx.arc(sunX, sunY, sunR, 0, Math.PI * 2);
  ctx.fillStyle = "red";
  ctx.fill();

  // 4. ท้องนา
  ctx.fillStyle = "#FFD700";
  ctx.fillRect(0, 300, 800, 200);

  // 5. ต้นไม้
  ctx.fillStyle = "#8B4513";
  ctx.fillRect(100, 260, 20, 60);
  ctx.beginPath();
  ctx.arc(110, 250, 30, 0, Math.PI * 2);
  ctx.fillStyle = "green";
  ctx.fill();

  ctx.fillStyle = "#8B4513";
  ctx.fillRect(200, 270, 20, 50);
  ctx.beginPath();
  ctx.arc(210, 260, 25, 0, Math.PI * 2);
  ctx.fillStyle = "green";
  ctx.fill();

  // 6. บ้าน
  ctx.fillStyle = "#DEB887";
  ctx.fillRect(600, 280, 100, 80);
  ctx.beginPath();
  ctx.moveTo(600, 280);
  ctx.lineTo(650, 230);
  ctx.lineTo(700, 280);
  ctx.closePath();
  ctx.fillStyle = "#A0522D";
  ctx.fill();
  ctx.fillStyle = "#654321";
  ctx.fillRect(640, 320, 20, 40);

  // 7. แม่น้ำ
  const river = ctx.createLinearGradient(0, 300, 0, 500);
  river.addColorStop(0, "#1E90FF");
  river.addColorStop(1, "#0000CD");
  ctx.fillStyle = river;
  ctx.beginPath();
  ctx.moveTo(0, 400);
  ctx.bezierCurveTo(200, 380, 400, 450, 800, 420);
  ctx.lineTo(800, 500);
  ctx.lineTo(0, 500);
  ctx.closePath();
  ctx.fill();

  // อัปเดตตำแหน่งพระอาทิตย์
  sunX += dx;
  if (sunX + sunR > canvas.width || sunX - sunR < 50) {
    dx = -dx; // เด้งกลับ
  }

  requestAnimationFrame(drawScene);
}

// เริ่มการวาด
drawScene();
</script>
