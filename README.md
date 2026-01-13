<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Happy 15th Birthday Navya | A Premium Celebration</title>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        /* --- CSS VARIABLES & RESET --- */
        :root {
            --gold: #d4af37;
            --gold-light: #f1dca7;
            --crimson: #7a0019;
            --crimson-dark: #4a0010;
            --bg-dark: #0a0505;
            --text-light: #f8f5e1;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }
        body, html {
            height: 100%;
            font-family: 'Poppins', sans-serif;
            background-color: var(--bg-dark);
            color: var(--text-light);
            overflow: hidden;
            background: radial-gradient(circle at center, #1a0a0a 0%, #000000 100%);
        }

        /* --- CONTAINERS --- */
        #stage {
            position: relative;
            width: 100%;
            height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            z-index: 10;
        }

        /* Background Magic Dust Effect */
        #bg-particles {
            position: absolute; top: 0; left: 0; width: 100%; height: 100%;
            z-index: 1; pointer-events: none; opacity: 0.5;
        }

        /* --- TYPOGRAPHY --- */
        h1 {
            font-family: 'Playfair Display', serif;
            font-size: 3.5rem;
            background: linear-gradient(to right, var(--gold), var(--gold-light));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 10px;
            text-align: center;
            opacity: 0; animation: fadeUp 1s ease forwards 0.5s;
        }

        .subtitle {
            font-size: 1.2rem; letter-spacing: 3px; text-transform: uppercase; color: var(--gold);
            margin-bottom: 40px; opacity: 0; animation: fadeUp 1s ease forwards 0.8s;
        }

        /* --- THE CAKE STAGE --- */
        .cake-stage-container {
            position: relative;
            width: 300px;
            height: 300px;
            display: flex;
            justify-content: center;
            align-items: flex-end;
            cursor: pointer;
            z-index: 20;
            opacity: 0; animation: zoomIn 1s ease forwards 1s;
        }

        /* SVG Styles */
        #cake-svg { width: 250px; height: auto; overflow: visible; }
        .cake-body { fill: var(--crimson); stroke: var(--crimson-dark); stroke-width: 2; }
        .cake-frosting { fill: #fff0f5; filter: drop-shadow(0px 2px 2px rgba(0,0,0,0.2)); }
        .cake-gold-accent { fill: var(--gold); }
        .candle-body { fill: #ffcccc; }
        .candle-flame { fill: orange; animation: flicker 0.5s infinite alternate; transform-origin: center bottom; }

        /* The Knife */
        #knife-container {
            position: absolute;
            top: -100px; left: 50%;
            transform: translateX(-50%) rotate(-10deg);
            opacity: 0;
            pointer-events: none;
            z-index: 25;
            transition: all 0.5s ease;
        }
        .knife-body { fill: silver; stroke: #666; stroke-width: 1; }
        .knife-handle { fill: var(--crimson-dark); }

        /* --- ACTION CLASSES (Added by JS) --- */
        .cake-stage-container.cutting #knife-container {
            opacity: 1;
            top: 20px; /* Move down to cut */
        }

        /* Separate the cake halves */
        .cake-left-half { transition: transform 1s cubic-bezier(0.175, 0.885, 0.32, 1.275) 0.5s; }
        .cake-right-half { transition: transform 1s cubic-bezier(0.175, 0.885, 0.32, 1.275) 0.5s; }
        
        .cake-stage-container.cut-done .cake-left-half { transform: translateX(-20px) rotate(-5deg); }
        .cake-stage-container.cut-done .cake-right-half { transform: translateX(20px) rotate(5deg); }
        .cake-stage-container.cut-done #knife-container { opacity: 0; top: 100px; transition-delay: 0.8s; }
        .cake-stage-container.cut-done .candle { opacity: 0; transition: opacity 0.3s 0.5s;}

        /* Instruction Pulse */
        .tap-instruction {
            position: absolute; bottom: -40px; width: 100%; text-align: center;
            color: var(--gold-light); font-size: 0.9rem; letter-spacing: 1px;
            animation: pulse 2s infinite; pointer-events: none;
        }
        .cake-stage-container.cut-done .tap-instruction { display: none; }


        /* --- THE FINAL REVEAL SECTION --- */
        #reveal-section {
            position: absolute; top: 55%; left: 50%; transform: translate(-50%, -50%);
            width: 90%; max-width: 600px;
            text-align: center;
            opacity: 0; pointer-events: none;
            transition: all 1s ease 1.5s; /* Delayed appearance */
            z-index: 30;
        }
        .cake-stage-container.cut-done ~ #reveal-section {
             opacity: 1; pointer-events: auto; top: 50%;
        }

        .love-quote {
            font-family: 'Playfair Display', serif; font-style: italic; font-size: 1.8rem;
            color: var(--gold); margin-bottom: 30px; text-shadow: 0 2px 10px rgba(212, 175, 55, 0.3);
        }
        .wishes-box {
            background: rgba(255, 255, 255, 0.05);
            backdrop-filter: blur(10px);
            padding: 30px; border-radius: 20px;
            border: 1px solid rgba(212, 175, 55, 0.3);
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }
        .wishes-text { font-size: 1.1rem; line-height: 1.8; color: #ccc; }
        .highlight { color: var(--gold-light); font-weight: 600; }


        /* --- BALLOONS & CONFETTI --- */
        #balloon-container {
            position: fixed; bottom: 0; left: 0; width: 100%; height: 100%;
            pointer-events: none; z-index: 5; overflow: hidden;
        }
        .balloon {
            position: absolute; bottom: -100px;
            width: 60px; height: 80px;
            background: radial-gradient(circle at 30% 30%, var(--gold-light), var(--crimson));
            border-radius: 50%;
            opacity: 0.8;
            box-shadow: inset -5px -5px 10px rgba(0,0,0,0.3);
            animation: floatUp var(--speed) linear forwards;
        }
        .balloon::before { /* String */
            content: ''; position: absolute; bottom: -20px; left: 50%;
            width: 1px; height: 20px; background: rgba(255,255,255,0.5);
        }

        .confetti {
            position: absolute; width: 10px; height: 10px;
            background: var(--gold); opacity: 0;
        }

        /* --- ANIMATION KEYFRAMES --- */
        @keyframes fadeUp { from { opacity: 0; transform: translateY(30px); } to { opacity: 1; transform: translateY(0); } }
        @keyframes zoomIn { from { opacity: 0; transform: scale(0.8); } to { opacity: 1; transform: scale(1); } }
        @keyframes flicker { 0% { transform: scale(1); opacity: 1; } 100% { transform: scale(0.9); opacity: 0.8; } }
        @keyframes pulse { 0% { opacity: 0.4; } 50% { opacity: 1; } 100% { opacity: 0.4; } }
        @keyframes floatUp {
            0% { transform: translateY(0) rotate(0deg); opacity: 1; }
            80% { opacity: 0.9; }
            100% { transform: translateY(-120vh) rotate(360deg); opacity: 0; }
        }

        /* Mobile adjustments */
        @media(max-width: 480px) {
             h1 { font-size: 2.5rem; }
             .love-quote { font-size: 1.4rem; }
        }
    </style>
</head>
<body>

    <canvas id="bg-particles"></canvas>

    <div id="stage">
        <h1>Happy Birthday Navya</h1>
        <div class="subtitle">The Big 15 ❤️</div>

        <div class="cake-stage-container" onclick="cutTheCake()">
            <div id="knife-container">
                <svg width="60" height="150" viewBox="0 0 60 150">
                    <path class="knife-handle" d="M20,0 L40,0 L40,50 L20,50 Z" />
                    <path class="knife-body" d="M20,50 L40,50 L35,140 L25,140 Z" />
                </svg>
            </div>

            <svg id="cake-svg" viewBox="0 0 200 220">
                <g class="candle">
                     <rect class="candle-body" x="95" y="0" width="10" height="30" rx="2"/>
                     <path class="candle-flame" d="M100,0 Q105,-10 100,-20 Q95,-10 100,0 Z" />
                </g>
                <g class="cake-left-half">
                    <path class="cake-body" d="M10,180 L100,180 L100,130 L10,130 Z" /> <path class="cake-body" d="M30,130 L100,130 L100,80 L30,80 Z" /> <path class="cake-frosting" d="M10,130 Q30,140 55,130 T100,130 L100,125 L10,125 Z" />
                    <path class="cake-frosting" d="M30,80 Q50,90 65,80 T100,80 L100,75 L30,75 Z" />
                    <rect class="cake-gold-accent" x="10" y="175" width="90" height="5" />
                </g>
                <g class="cake-right-half">
                    <path class="cake-body" d="M100,180 L190,180 L190,130 L100,130 Z" /> <path class="cake-body" d="M100,130 L170,130 L170,80 L100,80 Z" /> <path class="cake-frosting" d="M100,130 Q125,140 145,130 T190,130 L190,125 L100,125 Z" />
                    <path class="cake-frosting" d="M100,80 Q120,90 135,80 T170,80 L170,75 L100,75 Z" />
                     <rect class="cake-gold-accent" x="100" y="175" width="90" height="5" />
                </g>
            </svg>
            <div class="tap-instruction">Tap to cut the cake ✨</div>
        </div>

        <div id="reveal-section">
            <div class="love-quote">
                "In a world full of trends, you remain my timeless classic. Happy 15th, my Queen."
            </div>
            <div class="wishes-box">
                <p class="wishes-text">
                    Navya, may this 15th chapter be filled with pages of <span class="highlight">endless joy</span>, dreams that take flight, and moments that sparkle as brightly as you do. You are celebrated today and loved every day.
                </p>
                <p style="margin-top: 20px; font-family:'Playfair Display'; color:var(--gold);">Forever Yours ❤️</p>
            </div>
        </div>

    </div>

    <div id="balloon-container"></div>


    <script>
        let isCut = false;
        const stage = document.querySelector('.cake-stage-container');
        const balloonContainer = document.getElementById('balloon-container');

        function cutTheCake() {
            if (isCut) return;
            isCut = true;

            // 1. Animate Knife downwards
            stage.classList.add('cutting');

            // 2. Wait for knife to reach bottom, then separate cake and perform effects
            setTimeout(() => {
                stage.classList.add('cut-done');
                // Wait a tiny bit for the separation to start before launching balloons
                setTimeout(() => {
                    launchCelebration();
                }, 300);
            }, 600); // Matches the CSS transition time for the knife
        }

        function launchCelebration() {
            // Launch Balloons Loop
            let balloonCount = 0;
            const balloonInterval = setInterval(() => {
                createBalloon();
                balloonCount++;
                if (balloonCount > 25) clearInterval(balloonInterval); // Stop after 25 balloons
            }, 200);

            // Launch Confetti Explosion
            explodeConfetti(window.innerWidth / 2, window.innerHeight / 2);
        }


        function createBalloon() {
            const balloon = document.createElement('div');
            balloon.classList.add('balloon');
            // Randomize starting position and speed
            balloon.style.left = Math.random() * 90 + 5 + '%';
            balloon.style.setProperty('--speed', (Math.random() * 4 + 5) + 's'); // between 5s and 9s duration
            
            // Randomize colors slightly
            const hue = Math.floor(Math.random() * 50); // Golds to reds
            balloon.style.background = `radial-gradient(circle at 30% 30%, hsl(${hue}, 80%, 70%), hsl(${hue+340}, 90%, 30%))`;

            balloonContainer.appendChild(balloon);

            // Clean up DOM
            setTimeout(() => { balloon.remove(); }, 9000);
        }

        function explodeConfetti(x, y) {
            const colors = [varCSS('--gold'), varCSS('--crimson'), '#ffffff'];
            for (let i = 0; i < 100; i++) {
                const confetti = document.createElement('div');
                confetti.classList.add('confetti');
                document.body.appendChild(confetti);

                const color = colors[Math.floor(Math.random() * colors.length)];
                confetti.style.background = color;
                confetti.style.left = x + 'px';
                confetti.style.top = y + 'px';

                // Random trajectory
                const angle = Math.random() * Math.PI * 2;
                const velocity = Math.random() * 15 + 5;
                const tx = Math.cos(angle) * velocity * 15;
                const ty = Math.sin(angle) * velocity * 15 - 200; // Upward bias

                confetti.animate([
                    { transform: `translate(0,0) rotate(0)`, opacity: 1 },
                    { transform: `translate(${tx}px, ${ty}px) rotate(${Math.random()*720}deg)`, opacity: 0 }
                ], {
                    duration: Math.random() * 1500 + 500,
                    easing: 'cubic-bezier(0.25, 0.46, 0.45, 0.94)',
                    fill: 'forwards'
                });
                
                setTimeout(() => confetti.remove(), 2500);
            }
        }

        // Helper to get CSS variable value
        function varCSS(v) {
             return getComputedStyle(document.documentElement).getPropertyValue(v).trim();
        }

        // --- Subtle Background Particles (The "Special" touch) ---
        const canvas = document.getElementById('bg-particles');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        let particlesArray = [];

        class Particle {
            constructor() {
                this.x = Math.random() * canvas.width;
                this.y = Math.random() * canvas.height;
                this.size = Math.random() * 2 + 0.5;
                this.speedX = Math.random() * 0.5 - 0.25;
                this.speedY = Math.random() * 0.5 - 0.25;
                this.color = 'rgba(212, 175, 55, 0.3)'; // Transparent Gold
            }
            update() {
                this.x += this.speedX;
                this.y += this.speedY;
                if (this.x > canvas.width || this.x < 0) this.speedX *= -1;
                if (this.y > canvas.height || this.y < 0) this.speedY *= -1;
            }
            draw() {
                ctx.fillStyle = this.color;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
            }
        }

        function initParticles() {
            for (let i = 0; i < 100; i++) { particlesArray.push(new Particle()); }
        }
        function animateParticles() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            for (let i = 0; i < particlesArray.length; i++) {
                particlesArray[i].update();
                particlesArray[i].draw();
            }
            requestAnimationFrame(animateParticles);
        }
        initParticles();
        animateParticles();
        window.addEventListener('resize', () => {
             canvas.width = window.innerWidth; canvas.height = window.innerHeight;
        });

    </script>
</body>
</html>
