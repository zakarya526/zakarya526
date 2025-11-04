<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Muhammad Zakarya - Portfolio</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #0a0e27 0%, #1a1a2e 50%, #16213e 100%);
            overflow-x: hidden;
        }

        .header-container {
            position: relative;
            width: 100%;
            height: 400px;
            overflow: hidden;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        #particles-canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 1;
        }

        .content {
            position: relative;
            z-index: 2;
            text-align: center;
            padding: 20px;
        }

        .crown {
            font-size: 80px;
            animation: float 3s ease-in-out infinite;
            filter: drop-shadow(0 0 20px #ffd700);
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
        }

        .main-title {
            font-size: 48px;
            font-weight: 800;
            background: linear-gradient(45deg, #ffd700, #ffed4e, #ffd700);
            background-size: 200% auto;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            animation: shimmer 3s linear infinite;
            text-shadow: 0 0 30px rgba(255, 215, 0, 0.5);
            margin: 20px 0;
            letter-spacing: 2px;
        }

        @keyframes shimmer {
            to { background-position: 200% center; }
        }

        .subtitle {
            font-size: 20px;
            color: #a8dadc;
            font-weight: 300;
            margin-top: 15px;
            letter-spacing: 1px;
        }

        .badges {
            display: flex;
            gap: 15px;
            justify-content: center;
            margin-top: 25px;
            flex-wrap: wrap;
        }

        .badge {
            padding: 10px 20px;
            background: rgba(255, 215, 0, 0.1);
            border: 2px solid #ffd700;
            border-radius: 25px;
            color: #ffd700;
            font-size: 14px;
            font-weight: 600;
            backdrop-filter: blur(10px);
            transition: all 0.3s ease;
            cursor: default;
        }

        .badge:hover {
            background: rgba(255, 215, 0, 0.2);
            transform: translateY(-3px);
            box-shadow: 0 5px 20px rgba(255, 215, 0, 0.4);
        }

        .sparkle {
            position: absolute;
            width: 4px;
            height: 4px;
            background: #ffd700;
            border-radius: 50%;
            pointer-events: none;
            animation: sparkleAnim 1.5s ease-out forwards;
            z-index: 3;
        }

        @keyframes sparkleAnim {
            0% {
                transform: scale(0) translateY(0);
                opacity: 1;
            }
            100% {
                transform: scale(1) translateY(-100px);
                opacity: 0;
            }
        }

        @media (max-width: 768px) {
            .main-title {
                font-size: 32px;
            }
            .crown {
                font-size: 50px;
            }
            .subtitle {
                font-size: 16px;
            }
        }
    </style>
</head>
<body>
    <div class="header-container">
        <canvas id="particles-canvas"></canvas>
        <div class="content">
            <div class="crown">👑</div>
            <h1 class="main-title">Muhammad Zakarya</h1>
            <p class="subtitle">Full-Stack Architect | Crafting Digital Excellence</p>
            <div class="badges">
                <span class="badge">⚡ React Native</span>
                <span class="badge">🚀 Next.js</span>
                <span class="badge">💻 Innovation</span>
            </div>
        </div>
    </div>

    <script>
        const canvas = document.getElementById('particles-canvas');
        const ctx = canvas.getContext('2d');
        canvas.width = window.innerWidth;
        canvas.height = 400;

        const particles = [];
        const particleCount = 120;
        const colors = ['#ffd700', '#ffed4e', '#ffa500', '#ff6b6b', '#4ecdc4'];

        class Particle {
            constructor() {
                this.reset();
                this.y = Math.random() * canvas.height;
                this.opacity = Math.random();
            }

            reset() {
                this.x = Math.random() * canvas.width;
                this.y = canvas.height + 10;
                this.size = Math.random() * 4 + 1;
                this.speedY = -Math.random() * 2 - 0.5;
                this.speedX = Math.random() * 2 - 1;
                this.color = colors[Math.floor(Math.random() * colors.length)];
                this.opacity = 1;
            }

            update() {
                this.y += this.speedY;
                this.x += this.speedX;
                this.opacity -= 0.003;

                if (this.y < -10 || this.opacity <= 0) {
                    this.reset();
                }
            }

            draw() {
                ctx.save();
                ctx.globalAlpha = this.opacity;
                ctx.fillStyle = this.color;
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
                
                ctx.shadowBlur = 15;
                ctx.shadowColor = this.color;
                ctx.fill();
                ctx.restore();
            }
        }

        for (let i = 0; i < particleCount; i++) {
            particles.push(new Particle());
        }

        function animate() {
            ctx.fillStyle = 'rgba(10, 14, 39, 0.1)';
            ctx.fillRect(0, 0, canvas.width, canvas.height);

            particles.forEach(particle => {
                particle.update();
                particle.draw();
            });

            requestAnimationFrame(animate);
        }

        animate();

        window.addEventListener('resize', () => {
            canvas.width = window.innerWidth;
            canvas.height = 400;
        });

        // Sparkle effect on hover
        const content = document.querySelector('.content');
        content.addEventListener('mousemove', (e) => {
            if (Math.random() > 0.8) {
                const sparkle = document.createElement('div');
                sparkle.className = 'sparkle';
                sparkle.style.left = e.clientX + 'px';
                sparkle.style.top = e.clientY + 'px';
                document.body.appendChild(sparkle);
                
                setTimeout(() => sparkle.remove(), 1500);
            }
        });
    </script>
</body>
</html>

