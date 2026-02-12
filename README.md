<html>
<head>
  <style>
    body {
      margin: 0;
      background: #f2f2f2;
      height: 100vh;
      position: relative;
      overflow: hidden;
    }
  </style>
</head>

<body>

<script>
  function getClickPosition(callback) {
  document.addEventListener("pointerdown", function(event) {
      let x = event.clientX;
      let y = event.clientY;
      callback(x, y);
    });
  }
  // Curved Rectangle Function
  function curvedRect(x, y, width, height, color, curve) {
    let rect = document.createElement("div");

    rect.style.position = "absolute";
    rect.style.left = x + "px";
    rect.style.top = y + "px";
    rect.style.width = width + "px";
    rect.style.height = height + "px";
    rect.style.backgroundColor = color;
    rect.style.borderRadius = curve + "px";
    rect.style.boxShadow = "0px 6px 15px rgba(0,0,0,0.2)";

    document.body.appendChild(rect);

    return rect;
  }

  // Text Function
  function drawText(x, y, text, color, font, size) {
    let t = document.createElement("div");

    t.innerText = text;
    t.style.position = "absolute";
    t.style.left = x + "px";
    t.style.top = y + "px";
    t.style.color = color;
    t.style.fontFamily = font;
    t.style.fontSize = size + "px";
    t.style.whiteSpace = "pre"; // keeps spacing + line breaks

    document.body.appendChild(t);

    return t;
  }

  // Example usage
  curvedRect(100, 100, 300, 180, "white", 25);
  drawText(130, 140, "Hello World!", "black", "Arial", 28);

  curvedRect(450, 250, 250, 120, "dodgerblue", 20);
  drawText(480, 290, "Cool Button", "white", "Verdana", 22);
  while (1) {
    getClickPosition(function(x, y) {
    console.log("Clicked at:", x, y);
  });
  }

</script>

</body>
</html>
