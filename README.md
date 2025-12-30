<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FLAMES Love Calculator Pro</title>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    
    <style>
        /* --- 1. ANIMATED BACKGROUND --- */
        body {
            margin: 0;
            padding: 0;
            font-family: 'Poppins', sans-serif;
            height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            overflow: hidden;
            background: linear-gradient(-45deg, #ff9a9e, #fad0c4, #ffd1ff, #a18cd1);
            background-size: 400% 400%;
            animation: gradientBG 15s ease infinite;
            position: relative;
        }

        @keyframes gradientBG {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        /* Floating Hearts Animation */
        .hearts-bg {
            position: absolute;
            top: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none;
            z-index: 0;
        }
        .heart-particle {
            position: absolute;
            bottom: -20px;
            color: rgba(255, 255, 255, 0.5);
            font-size: 20px;
            animation: floatUp 10s linear infinite;
        }
        @keyframes floatUp {
            0% { transform: translateY(0) rotate(0deg); opacity: 0; }
            50% { opacity: 0.8; }
            100% { transform: translateY(-100vh) rotate(360deg); opacity: 0; }
        }

        /* --- 2. MAIN CARD CARD --- */
        .container {
            background: rgba(255, 255, 255, 0.9);
            backdrop-filter: blur(15px);
            padding: 40px;
            border-radius: 25px;
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.2);
            width: 90%;
            max-width: 420px;
            text-align: center;
            z-index: 150; /* Above background */
            transition: transform 0.2s;
            border: 1px solid rgba(255, 255, 255, 0.5);
        }

        .container:hover { transform: translateY(-5px); }

        h1 {
            background: linear-gradient(to right, #ff416c, #ff4b2b);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            font-weight: 700;
            margin-bottom: 5px;
            letter-spacing: 2px;
        }

        /* Input Styling with Icons */
        .input-group {
            position: relative;
            margin-bottom: 20px;
            text-align: left;
        }
        
        .input-group i {
            position: absolute;
            left: 15px;
            top: 48px; /* Adjusted for label */
            color: #ff4b2b;
        }

        label { margin-left: 5px; font-weight: 600; font-size: 0.9em; color: #555; }

        input {
            width: 90%;
            padding: 12px 15px 12px 40px; /* Space for icon */
            border: 2px solid #eee;
            border-radius: 50px;
            font-size: 12px;
            outline: none;
            transition: 0.3s;
            background: #f9f9f9;
        }

        input:focus {
            border-color: #ff416c;
            background: #fff;
            box-shadow: 0 0 10px rgba(255, 65, 108, 0.2);
        }

        /* Modern Button */
        button {
            width: 100%;
            padding: 15px;
            margin-top: 10px;
            background: linear-gradient(90deg, #ff416c, #ff4b2b);
            color: white;
            border: none;
            border-radius: 50px;
            font-size: 18px;
            font-weight: 700;
            cursor: pointer;
            box-shadow: 0 5px 20px rgba(255, 65, 108, 0.4);
            transition: all 0.3s ease;
        }

        button:hover {
            transform: scale(1.05);
            box-shadow: 0 8px 25px rgba(255, 65, 108, 0.6);
        }

        /* --- 3. POPUP MODAL --- */
        .popup-overlay {
            position: fixed; top: 0; left: 0;
            width: 100%; height: 100%;
            background: rgba(0, 0, 0, 0.6);
            display: none;
            justify-content: center; align-items: center;
            z-index: 100;
            backdrop-filter: blur(8px);
        }

        .popup-content {
            background: white;
            padding: 40px;
            border-radius: 20px;
            text-align: center;
            width: 85%; max-width: 350px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.3);
            animation: popIn 0.5s cubic-bezier(0.68, -0.55, 0.27, 1.55);
            position: relative;
        }

        @keyframes popIn {
            0% { transform: scale(0); }
            100% { transform: scale(1); }
        }

        .popup-emoji { font-size: 60px; margin-bottom: 15px; display: block; animation: bounce 2s infinite; }
        @keyframes bounce { 0%, 20%, 50%, 80%, 100% {transform: translateY(0);} 40% {transform: translateY(-20px);} 60% {transform: translateY(-10px);} }

        .popup-title { font-size: 28px; font-weight: bold; margin-bottom: 10px; }
        .popup-message { font-size: 16px; color: #666; margin-bottom: 25px; line-height: 1.5; }
        
        .close-btn { background: #333; box-shadow: none; width: auto; padding: 10px 30px; font-size: 14px; }
        .close-btn:hover { background: #555; transform: none; }

        /* --- 4. SPECIAL EFFECTS --- */
        
        /* Shake Animation for Enemy */
        .shake { animation: shake 0.5s; }
        @keyframes shake {
            0% { transform: translate(1px, 1px) rotate(0deg); }
            10% { transform: translate(-1px, -2px) rotate(-1deg); }
            20% { transform: translate(-3px, 0px) rotate(1deg); }
            30% { transform: translate(3px, 2px) rotate(0deg); }
            40% { transform: translate(1px, -1px) rotate(1deg); }
            50% { transform: translate(-1px, 2px) rotate(-1deg); }
            60% { transform: translate(-3px, 1px) rotate(0deg); }
            70% { transform: translate(3px, 1px) rotate(-1deg); }
            80% { transform: translate(-1px, -1px) rotate(1deg); }
            90% { transform: translate(1px, 2px) rotate(0deg); }
            100% { transform: translate(1px, -2px) rotate(-1deg); }
        }

        /* Canvas for Confetti */
        #confetti-canvas {
            position: absolute; top: 0; left: 0;
            width: 100%; height: 100%;
            pointer-events: none;
            z-index: 50;
        }

        .footer { margin-top: 25px; font-size: 0.8em; color: #888; }
    </style>
</head>
<body>

    <div class="hearts-bg" id="hearts-bg"></div>
    
    <canvas id="confetti-canvas"></canvas>

    <div class="container" id="main-card">
        <h1>🔥 FLAMES </h1>
        <p> Chusukoo Bro....😁<br>Predict your relationship destiny!</p>

        <div class="input-group">
            <label>Your Name</label>
            <i class="fas fa-user"></i>
            <input type="text" id="name1" placeholder="Enter Your Name...">
        </div>

        <div class="input-group">
            <label>Crush's Name</label>
            <i class="fas fa-heart"></i>
            <input type="text" id="name2" placeholder="Enter Crush's Name...">
        </div>

        <button onclick="calculateFlames()">REVEAL DESTINY ✨</button>
        <div class="footer">Note : Enter Full name with Intial to get exact result</div>    
        <div class="footer">Made by Navii ❤️</div>
    </div>

    <div id="popup" class="popup-overlay">
        <div class="popup-content">
            <span id="popup-emoji" class="popup-emoji"></span>
            <div id="popup-title" class="popup-title"></div>
            <div id="popup-message" class="popup-message"></div>
            <button class="close-btn" onclick="closePopup()">Try Again</button>
        </div>
    </div>

    <script>
        // Generate Floating Background Hearts
        function createHearts() {
            const container = document.getElementById('hearts-bg');
            for(let i=0; i<15; i++){
                let heart = document.createElement('div');
                heart.innerHTML = '❤️';
                heart.className = 'heart-particle';
                heart.style.left = Math.random() * 100 + '%';
                heart.style.animationDuration = (Math.random() * 5 + 5) + 's';
                heart.style.animationDelay = Math.random() * 5 + 's';
                container.appendChild(heart);
            }
        }
        createHearts();

        // --- FLAMES LOGIC ---
        function calculateFlames() {
            let name1 = document.getElementById("name1").value.trim();
            let name2 = document.getElementById("name2").value.trim();

            if (name1 === "" || name2 === "") {
                alert("Please enter both names!");
                return;
            }

            let n1 = name1.toLowerCase().replace(/\s/g, '').split('');
            let n2 = name2.toLowerCase().replace(/\s/g, '').split('');

            for (let i = 0; i < n1.length; i++) {
                for (let j = 0; j < n2.length; j++) {
                    if (n1[i] === n2[j]) {
                        n1[i] = '*'; n2[j] = '*'; break;
                    }
                }
            }

            let count = (n1.join('') + n2.join('')).replace(/\*/g, '').length;
            let flames = ["Friends", "Lovers", "Affection", "Marriage", "Enemy", "Siblings"];
            
            if (count === 0) {
                handleResult("Soulmates");
                return;
            }

            let index = 0;
            while (flames.length > 1) {
                index = (index + count - 1) % flames.length;
                flames.splice(index, 1);
            }

            handleResult(flames[0]);
        }

        function handleResult(result) {
            let message = "", emoji = "", color = "";
            let triggerConfetti = false;
            let triggerShake = false;

            switch(result) {
                case "Friends":
                    message = "Besties for life!Friendship is better than love bro🤧  🤝"; emoji = "👯"; color = "#2196F3";
                    break;
                case "Lovers":
                    message = "True Love Alert! All The Best Broo ❤️"; emoji = "💑"; color = "#ff416c";
                    triggerConfetti = true;
                    break;
                case "Affection":
                    message = "Someone has a crush... 👀"; emoji = "😍"; color = "#ff416c";
                    break;
                case "Marriage":
                    message = "Wedding Bells! Ewww Inkem Broo.. 💍"; emoji = "👰"; color = "#e0aa3e";
                    triggerConfetti = true;
                    break;
                case "Enemy":
                    message = "So bad of you!Parii Pooo Broo Run!🏃🏼‍♂️ ⚔️ "; emoji = "👿"; color = "#8b0000";
                    triggerShake = true;
                    break;
                case "Siblings":
                    message = "Brother/Sister Zone! 🚫"; emoji = "👦👧"; color = "#4CAF50";
                    break;
                case "Soulmates":
                    message = "Made for each other! ♾️"; emoji = "💖"; color = "#ff00cc";
                    triggerConfetti = true;
                    break;
            }

            // Apply Visual Effects
            let titleEl = document.getElementById("popup-title");
            titleEl.innerText = result.toUpperCase();
            titleEl.style.color = color;

            document.getElementById("popup-message").innerText = message;
            document.getElementById("popup-emoji").innerText = emoji;
            document.getElementById("popup").style.display = "flex";

            if (triggerConfetti) startConfetti();
            if (triggerShake) doShake();
        }

        function closePopup() {
            document.getElementById("popup").style.display = "none";
            document.getElementById("name1").value = "";
            document.getElementById("name2").value = "";
            
            // Clear effects
            const canvas = document.getElementById("confetti-canvas");
            const ctx = canvas.getContext("2d");
            ctx.clearRect(0, 0, canvas.width, canvas.height);
        }

        // --- EFFECT: SCREEN SHAKE (FOR ENEMY) ---
        function doShake() {
            let body = document.body;
            body.classList.add('shake');
            body.style.background = "linear-gradient(to right, #000000, #434343)"; // Dark background
            setTimeout(() => {
                body.classList.remove('shake');
                // Reset background after shake
                body.style.background = "linear-gradient(-45deg, #ff9a9e, #fad0c4, #ffd1ff, #a18cd1)"; 
            }, 1000);
        }

        // --- EFFECT: SIMPLE CONFETTI (FOR LOVERS) ---
        let confettiParticles = [];
        function startConfetti() {
            const canvas = document.getElementById("confetti-canvas");
            const ctx = canvas.getContext("2d");
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;

            for(let i=0; i<100; i++) {
                confettiParticles.push({
                    x: Math.random() * canvas.width,
                    y: Math.random() * canvas.height - canvas.height,
                    color: `hsl(${Math.random() * 360}, 100%, 50%)`,
                    size: Math.random() * 10 + 5,
                    speed: Math.random() * 5 + 2
                });
            }
            animateConfetti();
        }

        function animateConfetti() {
            const canvas = document.getElementById("confetti-canvas");
            const ctx = canvas.getContext("2d");
            if(document.getElementById("popup").style.display === "none") return;

            ctx.clearRect(0, 0, canvas.width, canvas.height);
            confettiParticles.forEach((p, index) => {
                p.y += p.speed;
                if(p.y > canvas.height) p.y = 0;
                
                ctx.fillStyle = p.color;
                ctx.beginPath();
                ctx.arc(p.x, p.y, p.size, 0, Math.PI * 2);
                ctx.fill();
            });
            requestAnimationFrame(animateConfetti);
        }
    </script>

</body>
</html>
