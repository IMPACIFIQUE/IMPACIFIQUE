<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Pacifique</title>
  <style>
    /* 1. Dark page with purple glow at the bottom */
    body {
      margin: 0;
      min-height: 100vh;
      display: flex;
      align-items: center;
      justify-content: center;
      background: radial-gradient(ellipse at 70% 100%, #4b2a8a, #08090d 60%);
      font-family: Arial, sans-serif;
    }

    /* 2. The box that holds everything (640 x 420) */
    .banner {
      position: relative;
      width: 640px;
      height: 420px;
    }

    /* 3. The two ellipse lines */
    .ring {
      position: absolute;
      left: 50%;
      top: 190px;
      transform: translate(-50%, -50%);
      border: 1px solid rgba(255, 255, 255, 0.12);
      border-radius: 50%;
    }
    .outer { width: 580px; height: 300px; }
    .inner { width: 340px; height: 170px; }

    /* 4. Logo in the center with glow */
    .logo {
      position: absolute;
      left: 50%;
      top: 190px;
      transform: translate(-50%, -50%);
      width: 110px;
      height: 110px;
      border-radius: 50%;
      border: 3px solid #ff6a3d;
      box-shadow: 0 0 40px #ff8a1f;
      background: #0b0b12;
      color: white;
      font-size: 34px;
      font-weight: bold;
      display: flex;
      align-items: center;
      justify-content: center;
      overflow: hidden;
    }
    .logo img { width: 100%; height: 100%; object-fit: cover; }

    /* 5. Round icon buttons (JavaScript moves them) */
    .icon {
      position: absolute;
      left: 0;
      top: 0;
      width: 46px;
      height: 46px;
      border-radius: 50%;
      background: #12131a;
      border: 1px solid rgba(255, 255, 255, 0.15);
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .icon img {
      width: 24px;
      height: 24px;
      filter: invert(1);   /* makes black icons white */
    }

    /* 6. Text under the logo */
    .text {
      position: absolute;
      bottom: 0;
      width: 100%;
      text-align: center;
      color: white;
    }
    .text h1 { margin: 0; font-size: 22px; }
    .text p  { margin: 6px 0 0; font-size: 13px; color: #aaa; }

    /* 7. Smaller on phones */
    @media (max-width: 660px) {
      .banner { transform: scale(0.55); }
    }
  </style>
</head>
<body>

  <div class="banner">

    <div class="ring outer"></div>
    <div class="ring inner"></div>

    <!-- Center logo: put your logo in images/logo.png -->
    <div class="logo">
      <img src="images/logo.png" alt="IP" onerror="this.style.display='none'; this.parentNode.append('IP')">
    </div>

    <!-- Outer ring icons: data-angle is the start position (0-360) -->
    <div class="icon" data-ring="outer" data-angle="250"><img src="https://cdn.jsdelivr.net/npm/simple-icons@11/icons/nodedotjs.svg" alt="Node"></div>
    <div class="icon" data-ring="outer" data-angle="300"><img src="https://cdn.jsdelivr.net/npm/simple-icons@11/icons/github.svg" alt="GitHub"></div>
    <div class="icon" data-ring="outer" data-angle="0"><img src="https://cdn.jsdelivr.net/npm/simple-icons@11/icons/html5.svg" alt="HTML5"></div>
    <div class="icon" data-ring="outer" data-angle="70"><img src="https://cdn.jsdelivr.net/npm/simple-icons@11/icons/javascript.svg" alt="JavaScript"></div>
    <div class="icon" data-ring="outer" data-angle="110"><img src="https://cdn.jsdelivr.net/npm/simple-icons@11/icons/figma.svg" alt="Figma"></div>
    <div class="icon" data-ring="outer" data-angle="180"><img src="https://cdn.jsdelivr.net/npm/simple-icons@11/icons/php.svg" alt="PHP"></div>

    <!-- Inner ring icons -->
    <div class="icon" data-ring="inner" data-angle="270"><img src="https://cdn.jsdelivr.net/npm/simple-icons@11/icons/vite.svg" alt="Vite"></div>
    <div class="icon" data-ring="inner" data-angle="350"><img src="https://cdn.jsdelivr.net/npm/simple-icons@11/icons/vuedotjs.svg" alt="Vue"></div>
    <div class="icon" data-ring="inner" data-angle="90"><img src="https://cdn.jsdelivr.net/npm/simple-icons@11/icons/css3.svg" alt="CSS"></div>
    <div class="icon" data-ring="inner" data-angle="190"><img src="https://cdn.jsdelivr.net/npm/simple-icons@11/icons/git.svg" alt="Git"></div>

    <div class="text">
      <h1>Hi, I'm Pacifique 👋</h1>
      <p>Web Developer &amp; Vibe Coder</p>
    </div>

  </div>

  <script>
    // Center of the rings, and half-width / half-height of each ellipse
    var centerX = 320;
    var centerY = 190;
    var rings = {
      outer: { a: 290, b: 150, speed: 0.00012 },   // goes one way
      inner: { a: 170, b: 85,  speed: -0.00018 }   // goes the other way
    };

    var icons = document.querySelectorAll(".icon");

    function move(time) {
      for (var i = 0; i < icons.length; i++) {
        var icon = icons[i];
        var ring = rings[icon.dataset.ring];
        var start = Number(icon.dataset.angle) * Math.PI / 180;

        // angle changes with time
        var angle = start + time * ring.speed;

        // ellipse formula
        var x = centerX + ring.a * Math.cos(angle) - 23;  // 23 = half icon size
        var y = centerY + ring.b * Math.sin(angle) - 23;

        icon.style.left = x + "px";
        icon.style.top = y + "px";
      }
      requestAnimationFrame(move);   // repeat forever
    }

    requestAnimationFrame(move);
  </script>

</body>
</html>
