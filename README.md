<!DOCTYPE html>
<html>
<head>
  <style>
    body {
      margin: 0;
      overflow: hidden;
      background: #111;
    }

    canvas {
      display: block;
    }
  </style>
</head>

<body>
<canvas id="gameCanvas"></canvas>

<script>
  const canvas = document.getElementById("gameCanvas");
  const ctx = canvas.getContext("2d");

  // Resize canvas to full screen
  function resizeCanvas() {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  }
  window.addEventListener("resize", resizeCanvas);
  resizeCanvas();

  let objects = [];

  function addRect(x, y, width, height, color, curve, rotation = 0) {
    objects.push({
      type: "rect",
      x: x,
      y: y,
      width: width,
      height: height,
      color: color,
      curve: curve,
      rotation: rotation,
      vx: 0,   // velocity X
      vy: 0    // velocity Y
    });
  }
  function addText(x, y, text, color, font, size) {
    objects.push({
      type: "text",
      x: x,
      y: y,
      text: text,
      color: color,
      font: font,
      size: size
    });
  }
  function addImage(x, y, width, height, src) {
    let img = new Image();
    img.src = src;

    objects.push({
      type: "image",
      x: x,
      y: y,
      width: width,
      height: height,
      img: img
    });
  }

function drawRoundedRect(x, y, width, height, radius, color) {
    ctx.fillStyle = color;

    ctx.beginPath();
    ctx.moveTo(x + radius, y);
    ctx.lineTo(x + width - radius, y);
    ctx.quadraticCurveTo(x + width, y, x + width, y + radius);
    ctx.lineTo(x + width, y + height - radius);
    ctx.quadraticCurveTo(x + width, y + height, x + width - radius, y + height);
    ctx.lineTo(x + radius, y + height);
    ctx.quadraticCurveTo(x, y + height, x, y + height - radius);
    ctx.lineTo(x, y + radius);
    ctx.quadraticCurveTo(x, y, x + radius, y);
    ctx.closePath();

    ctx.fill();
  }

  let mouseX = 0;
  let mouseY = 0;

  canvas.addEventListener("pointerdown", (event) => {
    mouseX = event.clientX;
    mouseY = event.clientY;

    console.log("Clicked at:", mouseX, mouseY);

  });

  let frames = 0;

  let state = 0;
  function logic() {
    switch (state) {
      case 0: // Scene 1 :
        objects[0].x = mouseX - objects[0].width/2;
        objects[0].y = mouseY - objects[0].height/2;
        objects[1].rotation += Math.PI / 15;
        objects[1].rotation %= 2*Math.PI;
        break;
      case 0:
        break;
      case 0:
        break;
      case 0:
        break;
      case 0:
        break;
      case 0:
        break;
      case 0:
        break;
    }

  }

  function draw() {
    // Clear screen
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    
    for (let ob of objects) {
      if (ob.type == "rect") { // Draw rectangle
        ctx.save();
        ctx.translate(ob.x + ob.width/2, ob.y + ob.height/2);
        ctx.rotate(ob.rotation);
        drawRoundedRect(-ob.width/2, -ob.height/2, ob.width, ob.height, ob.curve, ob.color);
        ctx.restore();
      } else if (ob.type == "text") { // Draw text
        ctx.fillStyle = ob.color;
        ctx.font = `${ob.size}px ${ob.font}`;
        ctx.fillText(ob.text, ob.x, ob.y);
      } else if (ob.type == "image") { // Draw image 
        if (ob.img.complete) {
          ctx.drawImage(ob.img, ob.x, ob.y, ob.width, ob.height);
        }
      }
      
    }

    

  }
  let fpsLimit = 30;
  let frameTime = 1000 / fpsLimit; // ms per frame
  let lastFrame = 0;
  addImage(100, 100,200, 200, "https://pngimg.com/d/dog_PNG50361.png");
  addRect(400, 200, 20, 200, "red", 15, Math.PI / 6);
  function mainLoop() {
    timestamp = Date.now();
    if (timestamp - lastFrame >= frameTime) {
      lastFrame = timestamp;
      logic();
      draw();
    }
    requestAnimationFrame(mainLoop);
  }



  mainLoop();
</script>
</body>
</html>
