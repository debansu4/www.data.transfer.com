# www.data.transfer.com
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Transferring Your Details</title>
  <link href="https://fonts.googleapis.com/css2?family=Fira+Code&display=swap" rel="stylesheet">
  <style>
    @keyframes glitch {
      0% { transform: skew(0); }
      20% { transform: skew(10deg); }
      40% { transform: skew(-10deg); }
      60% { transform: skew(5deg); }
      80% { transform: skew(-5deg); }
      100% { transform: skew(0); }
    }

    #progressBarWrapper {
      background-color: #003344;
      border: 1px solid #00ccff;
      border-radius: 10px;
      height: 20px;
      width: 100%;
      margin-top: 20px;
      overflow: hidden;
    }

    #progressBar {
      background-color: #00ff00;
      height: 100%;
      width: 0%;
      transition: width 0.2s ease;
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }
    body {
      background: radial-gradient(circle at center, #001f33, #000);
      font-family: 'Fira Code', monospace;
      color: #ccf6ff;
      min-height: 100vh;
      overflow: hidden;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
    }

    #loadingScreen {
      position: fixed;
      top: 0; left: 0;
      width: 100vw;
      height: 100vh;
      background: linear-gradient(135deg, #001133, #000);
      z-index: 9999;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      color: #ccf6ff;
      font-size: 20px;
      font-family: 'Fira Code', monospace;
      transition: opacity 1s ease;
    }

    #loadingScreen img {
      width: 300px;
      height: 300px;
      border-radius: 50%;
      margin-bottom: 20px;
      box-shadow: 0 0 25px #00ccff;
    }

    #matrix {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      z-index: 0;
    }

    .container {
      max-width: 750px;
      width: 100%;
      position: absolute;
      z-index: 1;
      background: rgba(255, 255, 255, 0.05);
      border-radius: 16px;
      box-shadow: 0 0 60px #00ccff;
      backdrop-filter: blur(10px);
      padding: 40px;
      text-align: center;
    }

    .editor {
      background-color: #001a33;
      border-radius: 12px;
      overflow: hidden;
      margin-bottom: 20px;
    }

    .header {
      background-color: #002b4d;
      display: flex;
      align-items: center;
      padding: 8px 12px;
    }

    .buttons {
      display: flex;
      gap: 6px;
    }

    .btn {
      width: 14px; height: 14px;
      border-radius: 50%;
    }

    .red { background: #ff5f56; }
    .yellow { background: #ffbd2e; }
    .green { background: #27c93f; }

    .title {
      margin-left: 12px;
      font-size: 14px;
      color: #eee;
    }

    .code-window {
      padding: 24px;
      text-align: left;
      font-size: 16px;
      background: #001122;
      height: 220px;
      color: #66e0ff;
      position: relative;
      overflow-y: auto;
      scroll-behavior: smooth;
    }

    #codeArea { white-space: pre-wrap; }

    #cursor {
      width: 10px;
      height: 20px;
      background: #00ccff;
      animation: blink 1s step-start infinite;
      position: absolute;
    }

    @keyframes blink { 50% { opacity: 0; } }

    #terminalOutput {
      background: #002b4d;
      padding: 20px;
      border-radius: 12px;
      color: #ccffcc;
      font-size: 14px;
      height: 120px;
      overflow-y: auto;
      margin-top: 20px;
      border: 1px solid #66e0ff;
      scroll-behavior: smooth;
    }

    #surpriseBtn {
      background: linear-gradient(135deg, #00ccff, #0055ff);
      border: none;
      padding: 16px 40px;
      margin-top: 30px;
      border-radius: 30px;
      font-size: 18px;
      color: #fff;
      font-weight: bold;
      cursor: pointer;
      transition: 0.3s;
      box-shadow: 0 0 20px #00ccff;
    }

    #surpriseBtn:hover {
      background: linear-gradient(135deg, #0099cc, #0044cc);
      transform: scale(1.1);
    }

    .shake {
      animation: shake 0.5s;
    }

    @keyframes shake {
      0%, 100% { transform: translateX(0); }
      25% { transform: translateX(-5px); }
      75% { transform: translateX(5px); }
    }
  </style>
</head>
<body>
<div id="loadingScreen">
  <img src="https://www.dropbox.com/scl/fi/nla69kz1n1p3qwjcesi1z/1aa561629e4ae136.jpg?rlkey=wmj83d6ewq7vup5w5ptzvy1vy&st=0cugn2g0&raw=1" alt="Profile Picture">
  <p>Initializing...</p>
</div>

<canvas id="matrix"></canvas>
<div class="container">
  <div class="editor">
    <div class="header">
      <div class="buttons">
        <span class="btn red"></span>
        <span class="btn yellow"></span>
        <span class="btn green"></span>
      </div>
      <div class="title">transferring details.js — Party Studio</div>
    </div>
    <div class="code-window">
      <pre id="codeArea"></pre><div id="cursor"></div>
    </div>
  </div>
  <div id="terminalOutput"></div>
  <button id="surpriseBtn">Execute Your Device</button>
</div>

<script>
  const canvas = document.getElementById('matrix');
  const ctx = canvas.getContext('2d');
  canvas.height = window.innerHeight;
  canvas.width = window.innerWidth;
  const letters = '01q0j682g5036n10a1';
  const fontSize = 12; // Smaller font size for higher density
  const columns = canvas.width / fontSize;
  const drops = Array.from({ length: columns }).fill(1);

  function drawMatrix() {
    ctx.fillStyle = "rgba(0, 0, 0, 0.03)"; // Lower opacity for smoother trails
    ctx.fillRect(0, 0, canvas.width, canvas.height);
    ctx.fillStyle = "#00ccff";
    ctx.font = fontSize + "px monospace";
    drops.forEach((y, x) => {
      const text = letters[Math.floor(Math.random() * letters.length)];
      ctx.fillText(text, x * fontSize, y * fontSize);
      if (y * fontSize > canvas.height && Math.random() > 0.975) {
        drops[x] = 0;
      }
      drops[x]++;
    });
  }

  setInterval(drawMatrix, 20);

  window.addEventListener("resize", () => {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;
  });

  window.onload = function() {
    const codeArea = document.getElementById("codeArea");
    const cursor = document.getElementById("cursor");
    const terminalOutput = document.getElementById("terminalOutput");

    const codeLines = [
      "const hackSystem = () => {",
      "  console.log('Establishing secure connection...');",
      "  console.log('Bypassing firewalls...');",
      "  console.log('Injecting malicious payload...');",
      "  console.log('Accessing root privileges...');",
      "  console.log('Extracting sensitive data...');",
      "};",
      "",
      "hackSystem();" ,
      "*************************************************************",
      "* SYSTEM ERROR: CONNECTION INSECURE   " ,                 
      "* HACKING MODULE ACTIVATED    " ,                        
      "* ESTABLISHING REMOTE ACCESS...   " ,                     
      "* ------------------------   ",
      "* WAIT... BYPASSING FIREWALL... " ,                          
      "* ACCESSING DATABASE...  "  ,                                
      "* LOADING SECURE FILES...  "     ,                           
      "* ------------------------ "   ,                            
      "* HACKING IN PROGRESS...   "   ,                              
      "* ----------------------------------  ",                       
      "* PASSWORD CRACKING...  "      ,                              
      "* SYSTEM COMPROMISED!    "    ,                               
      "* ----------------------------------   "  ,                    
      "* ACCESS GRANTED..." ,                              
      "* ------------------------    ",                            
      "* COMPLETE: TARGET SYSTEM HACKED!",                         
      "*************************************************************",
      "* REMOTE CONTROL ENABLED  ",                                 
      "*************************************************************",
    ];

    let lineIndex = 0;
    let charIndex = 0;
    const typingSpeed = 35;

    function typeCode() {
      if (lineIndex < codeLines.length) {
        let currentLine = codeLines[lineIndex];
        if (charIndex < currentLine.length) {
          codeArea.textContent += currentLine.charAt(charIndex);
          charIndex++;
          moveCursor();
          setTimeout(typeCode, typingSpeed);
        } else {
          codeArea.textContent += "\n";
          lineIndex++;
          charIndex = 0;
          setTimeout(typeCode, typingSpeed);
        }
        codeArea.parentElement.scrollTop = codeArea.parentElement.scrollHeight;
      }
    }

    function moveCursor() {
      const lines = codeArea.innerText.split("\n");
      const lastLine = lines[lines.length - 1];
      cursor.style.top = (lines.length - 1) * 24 + "px";
      cursor.style.left = (lastLine.length * 10) + "px";
    }

    typeCode();

    const loading = document.getElementById("loadingScreen");
    loading.style.opacity = 0;
    setTimeout(() => {
      loading.remove();
    }, 1000);

    document.getElementById("surpriseBtn").addEventListener("click", () => {
      terminalOutput.innerHTML = `
        >>> Starting Data Transfer...<br>
        <div id="progressBarWrapper">
          <div id="progressBar"></div>
        </div>
      `;

      let progress = 0;
      const bar = document.getElementById("progressBar");

      const interval = setInterval(() => {
        if (progress < 100) {
          progress += Math.floor(Math.random() * 5) + 2; // slower speed
          if (progress > 100) progress = 100;
          bar.style.width = progress + "%";
        } else {
          clearInterval(interval);
          terminalOutput.innerHTML += "<br>>> Data Transfer Complete.<br>*** DEVICE COMPROMISED ***";
          launchFireworks();
        }
      }, 500); // slower interval

      document.querySelector(".editor").classList.add("shake");
      setTimeout(() => {
        document.querySelector(".editor").classList.remove("shake");
      }, 1500);
    });
  };

  function launchFireworks() {
    for (let i = 0; i < 30; i++) {
      const flash = document.createElement('div');
      flash.style.position = 'fixed';
      flash.style.background = '#00ffcc';
      flash.style.width = Math.random() * 100 + 20 + 'px';
      flash.style.height = '4px';
      flash.style.top = Math.random() * window.innerHeight + 'px';
      flash.style.left = Math.random() * window.innerWidth + 'px';
      flash.style.opacity = 1;
      flash.style.zIndex = 10;
      flash.style.transition = 'opacity 0.4s ease-out';
      document.body.appendChild(flash);
      setTimeout(() => { flash.style.opacity = 0; }, 100);
      setTimeout(() => { flash.remove(); }, 500);
    }
  }
</script>
</body>
</html>
