#```html
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Spesial Untukmu ❤️</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <!-- Canvas Confetti -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <!-- html2canvas untuk fitur simpan kartu sebagai gambar -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/html2canvas/1.4.1/html2canvas.min.js"></script>
    <!-- Google Fonts: Pacifico & Poppins -->
    <link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    
    <style>
        body {
            font-family: 'Poppins', sans-serif;
            background: linear-gradient(135deg, #fff0f5 0%, #ffe4e1 50%, #f3e5f5 100%);
            min-height: 100vh;
            overflow-x: hidden;
        }
        .font-pacifico {
            font-family: 'Pacifico', cursive;
        }
        /* Style Canvas Partikel Latar Belakang */
        #bgCanvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 0;
        }
        /* Custom Glassmorphism Card */
        .glass-card {
            background: rgba(255, 255, 255, 0.75);
            backdrop-filter: blur(12px);
            border: 1px solid rgba(255, 255, 255, 0.8);
            box-shadow: 0 8px 32px 0 rgba(255, 182, 193, 0.3);
        }
        /* Soft Tab Button Active Effect */
        .tab-btn.active {
            background-color: #ff6b81;
            color: white;
            box-shadow: 0 4px 15px rgba(255, 107, 129, 0.4);
        }
    </style>
</head>
<body class="relative text-gray-700 pb-12">

    <!-- Canvas Partikel Hati Melayang -->
    <canvas id="bgCanvas"></canvas>

    <!-- Container Utama -->
    <div class="relative z-10 max-w-lg mx-auto px-4 pt-8">
        
        <!-- Header / Judul Utama -->
        <header class="text-center mb-6">
            <div class="inline-block p-3 bg-pink-100 rounded-full mb-3 text-pink-500 animate-bounce shadow-md">
                <i data-lucide="heart" class="w-8 h-8 fill-pink-500"></i>
            </div>
            <h1 class="font-pacifico text-3xl md:text-4xl text-pink-600 mb-1">Ada Pesan Untukmu ✨</h1>
            <p class="text-xs md:text-sm text-pink-400 font-medium">Dibuat khusus dengan rasa sayang yang melimpah!</p>
        </header>

        <!-- Navigasi Menu Utama -->
        <nav class="flex justify-center gap-2 mb-6 bg-white/60 p-1.5 rounded-full backdrop-blur-md shadow-sm border border-pink-100">
            <button onclick="switchTab('pesan')" id="tab-pesan" class="tab-btn active text-xs md:text-sm px-4 py-2 rounded-full font-medium transition-all duration-300 flex items-center gap-1.5">
                <i data-lucide="sparkles" class="w-4 h-4"></i> Pesan Manis
            </button>
            <button onclick="switchTab('pertanyaan')" id="tab-pertanyaan" class="tab-btn text-xs md:text-sm px-4 py-2 rounded-full font-medium transition-all duration-300 flex items-center gap-1.5">
                <i data-lucide="help-circle" class="w-4 h-4"></i> Sayang Aku?
            </button>
            <button onclick="switchTab('custom')" id="tab-custom" class="tab-btn text-xs md:text-sm px-4 py-2 rounded-full font-medium transition-all duration-300 flex items-center gap-1.5">
                <i data-lucide="pen-tool" class="w-4 h-4"></i> Buat Ucapan
            </button>
        </nav>

        <!-- KONTEN 1: Kartu Pesan Bucin Acak -->
        <section id="section-pesan" class="tab-content transition-all duration-300">
            <div class="glass-card rounded-3xl p-6 text-center relative overflow-hidden">
                <div class="absolute -top-10 -left-10 w-24 h-24 bg-pink-200/50 rounded-full blur-xl"></div>
                <div class="absolute -bottom-10 -right-10 w-24 h-24 bg-purple-200/50 rounded-full blur-xl"></div>
                
                <div class="min-h-[160px] flex flex-col justify-center items-center px-2">
                    <i data-lucide="quote" class="w-8 h-8 text-pink-300 mb-2 opacity-50"></i>
                    <p id="quoteText" class="text-base md:text-lg font-medium text-gray-700 leading-relaxed transition-opacity duration-300">
                        "Kalau kamu itu lagu, kamu adalah melodi favorit yang nggak pernah bosen aku putar setiap hari."
                    </p>
                    <span id="quoteAuthor" class="text-xs text-pink-500 mt-4 font-semibold italic">~ Untuk yang Tercinta ❤️</span>
                </div>

                <button onclick="generateRandomQuote()" class="mt-6 w-full py-3 px-6 bg-gradient-to-r from-pink-400 to-rose-400 hover:from-pink-500 hover:to-rose-500 text-white rounded-2xl font-semibold shadow-lg shadow-pink-200 hover:shadow-pink-300 transition-all duration-200 active:scale-95 flex items-center justify-center gap-2">
                    <i data-lucide="shuffle" class="w-4 h-4"></i> Acak Kata Manis
                </button>
            </div>
        </section>

        <!-- KONTEN 2: Interactive Question "Sayang Aku Ga?" -->
        <section id="section-pertanyaan" class="tab-content hidden transition-all duration-300">
            <div class="glass-card rounded-3xl p-6 text-center relative min-h-[320px] flex flex-col justify-between items-center">
                <div class="w-full">
                    <div id="emojiDisplay" class="text-6xl mb-4 animate-bounce">🥺</div>
                    <h2 id="questionTitle" class="text-xl md:text-2xl font-bold text-pink-600 mb-2">Kamu Sayang Sama Aku Nggak?</h2>
                    <p id="questionSubtitle" class="text-xs text-gray-500">Jawab jujur ya, gaboleh bohong! 😜</p>
                </div>

                <!-- Tombol Pilihan -->
                <div id="buttonGroup" class="w-full flex justify-center items-center gap-4 my-6 relative min-h-[80px]">
                    <button id="btnYes" onclick="handleYesClick()" class="px-6 py-3 bg-pink-500 hover:bg-pink-600 text-white font-bold rounded-2xl shadow-lg shadow-pink-200 transition-all duration-200 hover:scale-105 active:scale-95 flex items-center gap-2">
                        <i data-lucide="heart-handshake" class="w-5 h-5"></i> Sayang Banget!
                    </button>
                    
                    <button id="btnNo" onmouseenter="runAwayBtn()" onclick="runAwayBtn()" class="px-6 py-3 bg-gray-200 text-gray-600 font-semibold rounded-2xl transition-all duration-150 absolute md:static">
                        Enggak 😜
                    </button>
                </div>

                <!-- Hasil Ucapan (Hidden awal) -->
                <div id="resultModal" class="hidden w-full bg-pink-50/90 rounded-2xl p-4 border border-pink-200 text-pink-700 animate-fade-in">
                    <p class="font-bold text-lg mb-1">Yeayyy! Makasih ya Sayang! 🥰✨</p>
                    <p class="text-xs">Aku juga sayang banget sama kamu, melebihi apapun!</p>
                </div>
            </div>
        </section>

        <!-- KONTEN 3: Pembuat Pesan Custom -->
        <section id="section-custom" class="tab-content hidden transition-all duration-300">
            <div class="glass-card rounded-3xl p-6">
                <h2 class="text-lg font-bold text-pink-600 mb-4 flex items-center gap-2">
                    <i data-lucide="heart" class="w-5 h-5 text-pink-500"></i> Buat Kartu Spesial
                </h2>
                
                <!-- Form Input -->
                <div class="space-y-3 mb-6">
                    <div>
                        <label class="block text-xs font-semibold text-pink-500 mb-1">Nama Pasangan / Crush</label>
                        <input type="text" id="inputName" placeholder="Contoh: Princess / Mas Ganteng" class="w-full px-4 py-2.5 rounded-xl border border-pink-200 focus:outline-none focus:ring-2 focus:ring-pink-400 bg-white/80 text-sm">
                    </div>
                    <div>
                        <label class="block text-xs font-semibold text-pink-500 mb-1">Pesan Romantis</label>
                        <textarea id="inputMessage" rows="3" placeholder="Tuliskan pesan manismu di sini..." class="w-full px-4 py-2.5 rounded-xl border border-pink-200 focus:outline-none focus:ring-2 focus:ring-pink-400 bg-white/80 text-sm resize-none"></textarea>
                    </div>
                </div>

                <!-- Preview Card yang Siap Ditingkatkan/Di-screenshot -->
                <div id="cardPreview" class="bg-gradient-to-br from-pink-100 via-purple-50 to-rose-100 p-5 rounded-2xl border border-pink-200 shadow-inner relative text-center">
                    <div class="w-10 h-10 bg-white/80 rounded-full flex items-center justify-center mx-auto mb-2 shadow-sm">
                        <i data-lucide="sparkles" class="w-5 h-5 text-pink-500"></i>
                    </div>
                    <h3 id="previewTitle" class="font-pacifico text-xl text-pink-600 mb-2">Untuk: Nama Pasangan</h3>
                    <p id="previewText" class="text-xs md:text-sm text-gray-600 italic leading-relaxed">
                        "Pesan romantis kamu akan muncul di sini. Tuliskan sesuatu yang paling tulus dari hatimu!"
                    </p>
                    <div class="mt-4 pt-3 border-t border-pink-200/60 flex justify-between items-center text-[10px] text-pink-400">
                        <span>Spesial Dari Hati ❤️</span>
                        <span id="previewDate"></span>
                    </div>
                </div>

                <!-- Action Button -->
                <button onclick="downloadCard()" class="mt-4 w-full py-3 bg-pink-500 hover:bg-pink-600 text-white rounded-xl font-semibold shadow-md shadow-pink-200 transition-all flex items-center justify-center gap-2 text-sm">
                    <i data-lucide="download" class="w-4 h-4"></i> Simpan Kartu Ucapan
                </button>
            </div>
        </section>

    </div>

    <!-- Script Utama -->
    <script>
        // Initialize Icons
        lucide.createIcons();

        // 1. Logika Partikel Hati Melayang (Background Canvas)
        const canvas = document.getElementById('bgCanvas');
        const ctx = canvas.getContext('2d');
        let particles = [];

        function resizeCanvas() {
            canvas.width = window.innerWidth;
            canvas.height = window.innerHeight;
        }
        window.addEventListener('resize', resizeCanvas);
        resizeCanvas();

        class Particle {
            constructor() {
                this.reset();
            }
            reset() {
                this.x = Math.random() * canvas.width;
                this.y = canvas.height + 20;
                this.size = Math.random() * 12 + 8;
                this.speedY = Math.random() * 1.5 + 0.5;
                this.speedX = Math.sin(Math.random() * Math.PI) * 0.5;
                this.opacity = Math.random() * 0.5 + 0.3;
                this.color = `hsl(${Math.random() * 20 + 340}, 100%, 75%)`;
            }
            update() {
                this.y -= this.speedY;
                this.x += this.speedX;
                if (this.y < -20) this.reset();
            }
            draw() {
                ctx.save();
                ctx.globalAlpha = this.opacity;
                ctx.fillStyle = this.color;
                ctx.beginPath();
                // Gambar Bentuk Hati
                const topCurveHeight = this.size * 0.3;
                ctx.moveTo(this.x, this.y + topCurveHeight);
                ctx.bezierCurveTo(this.x, this.y, this.x - this.size / 2, this.y, this.x - this.size / 2, this.y + topCurveHeight);
                ctx.bezierCurveTo(this.x - this.size / 2, this.y + (this.size + topCurveHeight) / 2, this.x, this.y + this.size, this.x, this.y + this.size);
                ctx.bezierCurveTo(this.x, this.y + this.size, this.x + this.size / 2, this.y + (this.size + topCurveHeight) / 2, this.x + this.size / 2, this.y + topCurveHeight);
                ctx.bezierCurveTo(this.x + this.size / 2, this.y, this.x, this.y, this.x, this.y + topCurveHeight);
                ctx.closePath();
                ctx.fill();
                ctx.restore();
            }
        }

        // Buat 25 Partikel
        for (let i = 0; i < 25; i++) {
            particles.push(new Particle());
        }

        function animateParticles() {
            ctx.clearRect(0, 0, canvas.width, canvas.height);
            particles.forEach(p => {
                p.update();
                p.draw();
            });
            requestAnimationFrame(animateParticles);
        }
        animateParticles();

        // 2. Logika Navigasi Tab
        function switchTab(tabName) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            document.querySelectorAll('.tab-btn').forEach(el => el.classList.remove('active'));

            document.getElementById(`section-${tabName}`).classList.remove('hidden');
            document.getElementById(`tab-${tabName}`).classList.add('active');
        }

        // 3. Logika Kartu Pesan Bucin Acak
        const quotes = [
            "Kalau kamu itu lagu, kamu adalah melodi favorit yang nggak pernah bosen aku putar setiap hari.",
            "Tahu gak bedanya kamu sama bintang? Bintang ada di langit, kalau kamu ada di hatiku.",
            "Bukan karena aku butuh kamu, tapi karena bersama kamu segalanya terasa jauh lebih indah.",
            "Aku gak minta banyak, cukup kamu tetap di sini dan tersenyum seperti biasanya.",
            "Semesta itu luas banget, tapi anehnya fokus mataku cuma tertuju ke kamu.",
            "Setiap kali HP-ku bunyi, orang pertama yang aku harapkan ngirim chat itu cuma kamu."
        ];

        function generateRandomQuote() {
            const quoteText = document.getElementById('quoteText');
            quoteText.style.opacity = 0;
            setTimeout(() => {
                const randomIndex = Math.floor(Math.random() * quotes.length);
                quoteText.textContent = `"${quotes[randomIndex]}"`;
                quoteText.style.opacity = 1;
            }, 200);
        }

        // 4. Logika Interactive Button "Sayang Aku Ga?"
        const btnNo = document.getElementById('btnNo');
        let escapeCount = 0;

        function runAwayBtn() {
            escapeCount++;
            const container = document.getElementById('buttonGroup');
            const containerRect = container.getBoundingClientRect();
            
            // Hitung posisi acak di sekitar container
            const maxX = containerRect.width - btnNo.offsetWidth - 20;
            const maxY = 150; // Jangkauan vertikal
            
            const randomX = Math.floor(Math.random() * maxX) - (maxX / 2);
            const randomY = Math.floor(Math.random() * maxY) - (maxY / 2);

            btnNo.style.transform = `translate(${randomX}px, ${randomY}px)`;

            if(escapeCount > 3) {
                document.getElementById('questionSubtitle').textContent = "Eits! Nggak bisa diklik kan? Harus pilih 'Sayang Banget' dong! 😜";
            }
        }

        function handleYesClick() {
            // Efek Confetti / Kembang Api Hati
            confetti({
                particleCount: 100,
                spread: 70,
                origin: { y: 0.6 },
                colors: ['#ff6b81', '#ff4757', '#ffffff']
            });

            document.getElementById('emojiDisplay').textContent = "🥰💖";
            document.getElementById('questionTitle').textContent = "Aku Tahu Kamu Pasti Sayang!";
            document.getElementById('questionSubtitle').textContent = "Makasih udah bikin hariku makin bahagia ✨";
            document.getElementById('buttonGroup').classList.add('hidden');
            document.getElementById('resultModal').classList.remove('hidden');
        }

        // 5. Logika Form & Live Preview Kartu Custom
        const inputName = document.getElementById('inputName');
        const inputMessage = document.getElementById('inputMessage');
        const previewTitle = document.getElementById('previewTitle');
        const previewText = document.getElementById('previewText');
        const previewDate = document.getElementById('previewDate');

        // Set tanggal saat ini
        const today = new Date().toLocaleDateString('id-ID', { day: 'numeric', month: 'short', year: 'numeric' });
        previewDate.textContent = today;

        inputName.addEventListener('input', (e) => {
            previewTitle.textContent = e.target.value.trim() ? `Untuk: ${e.target.value}` : 'Untuk: Nama Pasangan';
        });

        inputMessage.addEventListener('input', (e) => {
            previewText.textContent = e.target.value.trim() ? `"${e.target.value}"` : '"Pesan romantis kamu akan muncul di sini. Tuliskan sesuatu yang paling tulus dari hatimu!"';
        });

        // Function Download Kartu sebagai Gambar
        function downloadCard() {
            const cardElement = document.getElementById('cardPreview');
            html2canvas(cardElement, {
                scale: 2,
                backgroundColor: null,
                borderRadius: 16
            }).then(canvas => {
                const link = document.createElement('a');
                link.download = `kartu-bucin-${Date.now()}.png`;
                link.href = canvas.toDataURL('image/png');
                link.click();
            });
        }
    </script>
</body>
</html>
```
Link-bucin
