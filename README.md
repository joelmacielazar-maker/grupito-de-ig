# grupito-de-ig
<!DOCTYPE html>
<html lang="es" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Nuestro Grupo // Atardecer Estrellado</title>

    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Google Fonts: Cinzel, Inter, Pinyon Script, VT323 (for VHS HUD) -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Cinzel:wght@400;600;700&family=Inter:wght@300;400;500;600;700&family=Pinyon+Script&family=VT323&display=swap" rel="stylesheet">
    
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>

    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Inter', 'sans-serif'],
                        serif: ['Cinzel', 'serif'],
                        cursive: ['Pinyon Script', 'cursive'],
                        vhs: ['VT323', 'monospace'],
                    }
                }
            }
        }
    </script>

    <style>
        body {
            background-color: #0b0314;
            color: #f3f4f6;
            font-family: 'Inter', sans-serif;
            overflow-x: hidden;
            user-select: none;
        }

        /* Glassmorphism Cards */
        .glass-card {
            background: rgba(35, 12, 55, 0.45);
            backdrop-filter: blur(16px);
            -webkit-backdrop-filter: blur(16px);
            border: 1px solid rgba(255, 255, 255, 0.1);
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.5), inset 0 1px 1px rgba(255, 255, 255, 0.15);
            transition: all 0.35s ease;
        }

        .glass-card:hover {
            background: rgba(55, 18, 85, 0.6);
            border-color: rgba(244, 114, 182, 0.35);
            box-shadow: 0 12px 35px rgba(244, 114, 182, 0.2), inset 0 1px 2px rgba(255, 255, 255, 0.25);
            transform: translateY(-4px);
        }

        /* Cursive Typography Styling */
        .hero-cursive {
            font-family: 'Pinyon Script', cursive;
            background: linear-gradient(135deg, #ffd1ea 0%, #f472b6 50%, #e85d9e 100%);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            filter: drop-shadow(0 0 20px rgba(232, 93, 158, 0.6));
        }

        /* Gradient CTA Button */
        .btn-gradient {
            background: linear-gradient(135deg, #f472b6 0%, #a855f7 50%, #6366f1 100%);
            box-shadow: 0 0 25px rgba(244, 114, 182, 0.5), inset 0 1px 1px rgba(255, 255, 255, 0.6);
            transition: all 0.3s ease;
        }

        .btn-gradient:hover {
            transform: scale(1.04) translateY(-2px);
            box-shadow: 0 0 35px rgba(244, 114, 182, 0.8), inset 0 1px 2px rgba(255, 255, 255, 0.9);
        }

        /* VHS / CRT Filter Overlay Effects */
        .vhs-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            pointer-events: none;
            z-index: 40;
            background: linear-gradient(
                rgba(18, 16, 16, 0) 50%, 
                rgba(0, 0, 0, 0.25) 50%
            ), linear-gradient(
                90deg,
                rgba(255, 0, 0, 0.03),
                rgba(0, 255, 0, 0.01),
                rgba(0, 0, 255, 0.03)
            );
            background-size: 100% 3px, 6px 100%;
            box-shadow: inset 0 0 100px rgba(0,0,0,0.7);
        }

        /* VHS Tracking Line Glitch Animation */
        .vhs-tracking-line {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 8px;
            background: rgba(255, 255, 255, 0.08);
            opacity: 0.6;
            pointer-events: none;
            z-index: 41;
            animation: vhsScan 8s linear infinite;
        }

        @keyframes vhsScan {
            0% { top: -10px; }
            100% { top: 105vh; }
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar { width: 8px; }
        ::-webkit-scrollbar-track { background: #0b0314; }
        ::-webkit-scrollbar-thumb { background: #3b1254; border-radius: 4px; }
        ::-webkit-scrollbar-thumb:hover { background: #f472b6; }
    </style>
</head>
<body class="relative min-h-screen text-slate-100 flex flex-col justify-between">

    <div class="fixed top-4 left-6 z-50 pointer-events-none font-vhs text-cyan-300 text-lg sm:text-xl tracking-widest flex items-center gap-3 drop-shadow-[0_0_8px_rgba(0,240,255,0.8)]">
        <span class="inline-block w-2.5 h-2.5 rounded-full bg-cyan-400 animate-pulse"></span>
        <span>PLAY</span>
        <span id="vhs-timestamp" class="text-xs sm:text-sm text-pink-300 ml-2">00:00:00</span>
    </div>

    <!-- VHS Scanline and CRT Glitch Overlay -->
    <div class="vhs-overlay"></div>
    <div class="vhs-tracking-line"></div>

    <div class="relative w-full overflow-hidden">
        <canvas id="sunset-canvas" class="absolute top-0 left-0 w-full h-full pointer-events-none z-0"></canvas>

        <!-- Navigation Header -->
        <header class="relative z-30 max-w-6xl mx-auto px-6 py-6 flex items-center justify-between">
            <div class="flex items-center gap-2 select-none">
                <span class="text-pink-300 text-xl font-serif">✦</span>
                <span class="font-cursive text-3xl md:text-4xl text-pink-200 tracking-wide">
                    Nuestro Grupo
                </span>
            </div>

            <nav class="hidden md:flex items-center gap-8 text-sm font-medium text-slate-200">
                <a href="#hero" class="border-b-2 border-pink-400 pb-0.5 text-white">Inicio</a>
                <a href="#que-encontraras" class="hover:text-pink-300 transition-colors">Sobre nosotros</a>
                <a href="#nuestras-reglas" class="hover:text-pink-300 transition-colors">Reglas</a>
                <a href="https://ig.me/j/AbbUa9YUVSSnbLIy/" target="_blank" class="hover:text-pink-300 transition-colors">Únete</a>
            </nav>

            <a href="https://ig.me/j/AbbUa9YUVSSnbLIy/" target="_blank" rel="noopener noreferrer" class="text-slate-200 hover:text-pink-300 transition-colors p-2" title="Instagram">
                <i data-lucide="instagram" class="w-5 h-5"></i>
            </a>
        </header>

        <section id="hero" class="relative z-20 max-w-4xl mx-auto px-6 pt-16 pb-36 text-center flex flex-col items-center justify-center">
            
            <div class="space-y-2 mb-6">
                <h1 class="font-serif text-4xl sm:text-6xl md:text-7xl font-light text-white tracking-wide">
                    Conecta.<br>
                    Comparte.<br>
                    <span class="hero-cursive text-6xl sm:text-8xl md:text-9xl block -mt-2">Sé tú. ♡</span>
                </h1>
            </div>

            <p class="max-w-md mx-auto text-sm sm:text-base text-slate-200 font-light leading-relaxed mb-8">
                Un lugar para jóvenes de 14 a 19 años que quieren conocer gente nueva, hacer amigos y crear recuerdos.
            </p>

            <div class="flex flex-col items-center gap-3">
                <a href="https://ig.me/j/AbbUa9YUVSSnbLIy/" target="_blank" rel="noopener noreferrer" class="btn-gradient text-white font-semibold text-sm px-8 py-3.5 rounded-full inline-flex items-center gap-2.5 shadow-lg uppercase tracking-wider">
                    <span>✦</span> QUIERO UNIRME
                </a>
                <span class="text-xs text-slate-300 font-light">Únete a nuestra comunidad</span>
            </div>

        </section>
    </div>

    <section id="que-encontraras" class="relative z-20 py-16 px-6 bg-[#0a0214]/85 backdrop-blur-md">
        <div class="max-w-5xl mx-auto text-center">
            
            <h2 class="font-serif text-2xl sm:text-3xl text-white font-light mb-12 inline-flex items-center gap-2">
                ¿Qué encontrarás aquí? <span class="text-pink-400 text-xl">✦</span>
            </h2>

            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-8">
                
                <div class="flex flex-col items-center text-center space-y-3 p-4 rounded-2xl hover:bg-white/5 transition-colors">
                    <div class="w-14 h-14 rounded-2xl bg-pink-500/10 border border-pink-500/20 flex items-center justify-center text-pink-300">
                        <i data-lucide="users" class="w-7 h-7"></i>
                    </div>
                    <h3 class="font-medium text-base text-white">Nuevas amistades</h3>
                    <p class="text-xs text-slate-400 leading-relaxed font-light">
                        Conoce personas increíbles como tú.
                    </p>
                </div>

                <div class="flex flex-col items-center text-center space-y-3 p-4 rounded-2xl hover:bg-white/5 transition-colors">
                    <div class="w-14 h-14 rounded-2xl bg-pink-500/10 border border-pink-500/20 flex items-center justify-center text-pink-300">
                        <i data-lucide="message-square" class="w-7 h-7"></i>
                    </div>
                    <h3 class="font-medium text-base text-white">Conversaciones</h3>
                    <p class="text-xs text-slate-400 leading-relaxed font-light">
                        Comparte ideas, gustos y mucho más.
                    </p>
                </div>

                <div class="flex flex-col items-center text-center space-y-3 p-4 rounded-2xl hover:bg-white/5 transition-colors">
                    <div class="w-14 h-14 rounded-2xl bg-pink-500/10 border border-pink-500/20 flex items-center justify-center text-pink-300">
                        <i data-lucide="star" class="w-7 h-7"></i>
                    </div>
                    <h3 class="font-medium text-base text-white">Diversión</h3>
                    <p class="text-xs text-slate-400 leading-relaxed font-light">
                        Participa en dinámicas, juegos y eventos.
                    </p>
                </div>

                <div class="flex flex-col items-center text-center space-y-3 p-4 rounded-2xl hover:bg-white/5 transition-colors">
                    <div class="w-14 h-14 rounded-2xl bg-pink-500/10 border border-pink-500/20 flex items-center justify-center text-pink-300">
                        <i data-lucide="shield-check" class="w-7 h-7"></i>
                    </div>
                    <h3 class="font-medium text-base text-white">Ambiente seguro</h3>
                    <p class="text-xs text-slate-400 leading-relaxed font-light">
                        Respetamos a todos y cuidamos nuestra comunidad.
                    </p>
                </div>

            </div>
        </div>
    </section>

    <section id="nuestras-reglas" class="relative z-20 py-20 px-6 bg-[#070110]">
        <div class="max-w-6xl mx-auto text-center">
            
            <h2 class="font-serif text-2xl sm:text-3xl text-white font-light mb-14 inline-flex items-center gap-2">
                <i data-lucide="scroll" class="w-6 h-6 text-pink-400"></i>
                Nuestras reglas <span class="text-pink-400 text-xl">✦</span>
            </h2>

            <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-5">
                
                <div class="glass-card rounded-2xl p-6 flex flex-col items-center text-center space-y-4">
                    <div class="w-12 h-12 rounded-xl bg-pink-500/10 border border-pink-400/20 flex items-center justify-center text-pink-300">
                        <i data-lucide="heart" class="w-6 h-6"></i>
                    </div>
                    <h3 class="font-medium text-sm text-white">Respeto</h3>
                    <p class="text-xs text-slate-300 font-light leading-relaxed">
                        Trata a todos con respeto. No se toleran insultos ni discriminación.
                    </p>
                </div>

                <div class="glass-card rounded-2xl p-6 flex flex-col items-center text-center space-y-4">
                    <div class="w-12 h-12 rounded-xl bg-pink-500/10 border border-pink-400/20 flex items-center justify-center text-pink-300">
                        <i data-lucide="ban" class="w-6 h-6"></i>
                    </div>
                    <h3 class="font-medium text-sm text-white">No acoso</h3>
                    <p class="text-xs text-slate-300 font-light leading-relaxed">
                        No está permitido acosar, molestar o amenazar a otros miembros.
                    </p>
                </div>

                <div class="glass-card rounded-2xl p-6 flex flex-col items-center text-center space-y-4">
                    <div class="w-12 h-12 rounded-xl bg-pink-500/10 border border-pink-400/20 flex items-center justify-center text-pink-300">
                        <i data-lucide="shield" class="w-6 h-6"></i>
                    </div>
                    <h3 class="font-medium text-sm text-white">Contenido apropiado</h3>
                    <p class="text-xs text-slate-300 font-light leading-relaxed">
                        No se permite contenido sexual, violento o inapropiado.
                    </p>
                </div>

                <div class="glass-card rounded-2xl p-6 flex flex-col items-center text-center space-y-4">
                    <div class="w-12 h-12 rounded-xl bg-pink-500/10 border border-pink-400/20 flex items-center justify-center text-pink-300">
                        <i data-lucide="user" class="w-6 h-6"></i>
                    </div>
                    <h3 class="font-medium text-sm text-white">Edad</h3>
                    <p class="text-xs text-slate-300 font-light leading-relaxed">
                        Este grupo es para jóvenes de 14 a 19 años.
                    </p>
                </div>

                <div class="glass-card rounded-2xl p-6 flex flex-col items-center text-center space-y-4">
                    <div class="w-12 h-12 rounded-xl bg-pink-500/10 border border-pink-400/20 flex items-center justify-center text-pink-300">
                        <i data-lucide="alert-triangle" class="w-6 h-6"></i>
                    </div>
                    <h3 class="font-medium text-sm text-white">Incumplimiento</h3>
                    <p class="text-xs text-slate-300 font-light leading-relaxed">
                        Romper las reglas puede resultar en la expulsión del grupo.
                    </p>
                </div>

            </div>
        </div>
    </section>

    <footer class="relative z-20 py-16 px-6 border-t border-white/5 bg-[#04000a] text-center space-y-6">
        <p class="font-cursive text-3xl sm:text-4xl text-pink-300">
            ✦ "Sé tú, conecta, comparte y brilla." ♡
        </p>

        <div class="flex items-center justify-center gap-6">
            <a href="https://ig.me/j/AbbUa9YUVSSnbLIy/" target="_blank" rel="noopener noreferrer" class="w-10 h-10 rounded-full bg-white/5 border border-white/10 flex items-center justify-center text-pink-300 hover:border-pink-400 transition-colors">
                <i data-lucide="instagram" class="w-5 h-5"></i>
            </a>
            <a href="mailto:comunidad@nuestrogrupo.org" class="w-10 h-10 rounded-full bg-white/5 border border-white/10 flex items-center justify-center text-pink-300 hover:border-pink-400 transition-colors">
                <i data-lucide="mail" class="w-5 h-5"></i>
            </a>
        </div>

      
        </p>
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            lucide.createIcons();
            initSunsetCanvas();
            initVhsTimestamp();
        });

        // VHS Live Timestamp Counter
        function initVhsTimestamp() {
            let seconds = 0;
            const el = document.getElementById('vhs-timestamp');
            setInterval(() => {
                seconds++;
                const hrs = String(Math.floor(seconds / 3600)).padStart(2, '0');
                const mins = String(Math.floor((seconds % 3600) / 60)).padStart(2, '0');
                const secs = String(seconds % 60).padStart(2, '0');
                el.textContent = `${hrs}:${mins}:${secs}`;
            }, 1000);
        }

        // Pure Sunset Sky Canvas Render (No horizon, No city, No moon)
        function initSunsetCanvas() {
            const canvas = document.getElementById('sunset-canvas');
            const ctx = canvas.getContext('2d');
            let stars = [];
            let clouds = [];

            function resize() {
                canvas.width = window.innerWidth;
                canvas.height = window.innerHeight;
                initStars();
                initClouds();
            }

            // Generate realistic dispersed twinkling stars
            function initStars() {
                stars = [];
                const numStars = Math.floor((canvas.width * canvas.height) / 3200);
                for (let i = 0; i < numStars; i++) {
                    stars.push({
                        x: Math.random() * canvas.width,
                        y: Math.random() * (canvas.height * 0.75),
                        radius: Math.random() * 1.6 + 0.3,
                        alpha: Math.random() * 0.8 + 0.2,
                        speed: Math.random() * 0.02 + 0.005,
                        phase: Math.random() * Math.PI * 2
                    });
                }
            }

            // Soft atmospheric twilight cloud layers
            function initClouds() {
                clouds = [];
                for (let i = 0; i < 6; i++) {
                    clouds.push({
                        x: Math.random() * canvas.width,
                        y: canvas.height * 0.35 + Math.random() * (canvas.height * 0.45),
                        width: canvas.width * (0.4 + Math.random() * 0.5),
                        height: 80 + Math.random() * 100,
                        speed: 0.15 + Math.random() * 0.2,
                        alpha: 0.15 + Math.random() * 0.15
                    });
                }
            }

            function animate() {
                ctx.clearRect(0, 0, canvas.width, canvas.height);

                // Pure Twilight Sunset Sky Gradient
                const skyGrad = ctx.createLinearGradient(0, 0, 0, canvas.height);
                skyGrad.addColorStop(0, '#0d041c');     // Deep Night Purple
                skyGrad.addColorStop(0.32, '#230a3b');  // Violet Twilight
                skyGrad.addColorStop(0.60, '#591653');  // Deep Magenta
                skyGrad.addColorStop(0.82, '#b2396c');  // Vibrant Pink Sunset
                skyGrad.addColorStop(1, '#e3687c');     // Warm Peach Sunset Glow
                ctx.fillStyle = skyGrad;
                ctx.fillRect(0, 0, canvas.width, canvas.height);

                // Render Dispersed Realistic Stars
                stars.forEach(s => {
                    s.phase += s.speed;
                    const tw = Math.sin(s.phase) * 0.35;
                    const currentAlpha = Math.min(1, Math.max(0.1, s.alpha + tw));

                    ctx.beginPath();
                    ctx.arc(s.x, s.y, s.radius, 0, Math.PI * 2);
                    ctx.fillStyle = `rgba(255, 235, 245, ${currentAlpha})`;
                    ctx.shadowColor = 'rgba(255, 255, 255, 0.8)';
                    ctx.shadowBlur = s.radius > 1.2 ? 6 : 2;
                    ctx.fill();
                    ctx.shadowBlur = 0;
                });

                // Render Drifting Twilight Cloud Layers
                clouds.forEach(c => {
                    c.x += c.speed;
                    if (c.x - c.width > canvas.width) c.x = -c.width;

                    const cloudGrad = ctx.createRadialGradient(
                        c.x, c.y, 10,
                        c.x, c.y, c.width / 2
                    );
                    cloudGrad.addColorStop(0, `rgba(180, 50, 110, ${c.alpha})`);
                    cloudGrad.addColorStop(0.6, `rgba(80, 20, 70, ${c.alpha * 0.5})`);
                    cloudGrad.addColorStop(1, 'rgba(0, 0, 0, 0)');

                    ctx.fillStyle = cloudGrad;
                    ctx.beginPath();
                    ctx.ellipse(c.x, c.y, c.width / 2, c.height / 2, 0, 0, Math.PI * 2);
                    ctx.fill();
                });

                requestAnimationFrame(animate);
            }

            window.addEventListener('resize', resize);
            resize();
            animate();
        }
    </script>
</body>
</html>
