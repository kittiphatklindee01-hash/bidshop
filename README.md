<!DOCTYPE html>
<html lang="th" class="dark">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>BIDSHOP - ศูนย์รวมไอดีเกมและสินค้าดิจิทัล 24 ชม.</title>
  
  <!-- Tailwind CSS -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Font Awesome Icons -->
  <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css" rel="stylesheet">
  <!-- Google Fonts: Prompt & Montserrat -->
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@700;900&family=Prompt:wght@300;400;500;600;700&display=swap" rel="stylesheet">

  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          fontFamily: {
            sans: ['Prompt', 'sans-serif'],
            display: ['Montserrat', 'Prompt', 'sans-serif'],
          },
          colors: {
            cyber: {
              bg: '#05070d',
              card: 'rgba(13, 19, 33, 0.75)',
              border: 'rgba(6, 182, 212, 0.25)',
              cyan: '#06b6d4',
              purple: '#a855f7',
              pink: '#ec4899',
            }
          },
          animation: {
            'pulse-slow': 'pulse 4s cubic-bezier(0.4, 0, 0.6, 1) infinite',
            'glow-cyan': 'glowCyan 2s infinite alternate',
            'float': 'float 3s ease-in-out infinite',
          },
          keyframes: {
            glowCyan: {
              '0%': { boxShadow: '0 0 10px rgba(6, 182, 212, 0.3)' },
              '100%': { boxShadow: '0 0 25px rgba(6, 182, 212, 0.7), 0 0 40px rgba(168, 85, 247, 0.4)' }
            },
            float: {
              '0%, 100%': { transform: 'translateY(0px)' },
              '50%': { transform: 'translateY(-8px)' }
            }
          }
        }
      }
    }
  </script>

  <style>
    * {
      font-family: 'Prompt', sans-serif;
    }
    body {
      background-color: #04060a;
      color: #f1f5f9;
      overflow-x: hidden;
    }
    
    /* Dynamic Canvas Background */
    #bg-canvas {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      z-index: 0;
      pointer-events: none;
    }

    /* Glassmorphism Styles */
    .glass-panel {
      background: rgba(10, 15, 28, 0.7);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border: 1px solid rgba(255, 255, 255, 0.08);
    }

    .glass-card {
      background: linear-gradient(135deg, rgba(15, 23, 42, 0.8) 0%, rgba(10, 15, 28, 0.9) 100%);
      backdrop-filter: blur(12px);
      border: 1px solid rgba(6, 182, 212, 0.15);
      transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    }

    .glass-card:hover {
      border-color: rgba(6, 182, 212, 0.6);
      transform: translateY(-4px);
      box-shadow: 0 12px 30px -10px rgba(6, 182, 212, 0.3), 0 0 20px -5px rgba(168, 85, 247, 0.2);
    }

    .text-gradient {
      background: linear-gradient(135deg, #38bdf8 0%, #818cf8 50%, #c084fc 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
    }

    .text-glow {
      text-shadow: 0 0 12px rgba(6, 182, 212, 0.6);
    }

    .custom-scrollbar::-webkit-scrollbar {
      width: 6px;
    }
    .custom-scrollbar::-webkit-scrollbar-track {
      background: rgba(5, 7, 13, 0.5);
    }
    .custom-scrollbar::-webkit-scrollbar-thumb {
      background: rgba(6, 182, 212, 0.3);
      border-radius: 4px;
    }
    .custom-scrollbar::-webkit-scrollbar-thumb:hover {
      background: rgba(6, 182, 212, 0.7);
    }
  </style>
</head>
<body class="min-h-screen flex flex-col justify-between custom-scrollbar selection:bg-cyan-500 selection:text-black">

  <!-- Interactive Dynamic Background Canvas -->
  <canvas id="bg-canvas"></canvas>

  <!-- Toast Notification Container -->
  <div id="toast-container" class="fixed top-5 right-5 z-50 flex flex-col gap-3 pointer-events-none"></div>

  <!-- Navbar -->
  <nav class="glass-panel sticky top-0 z-40 border-b border-cyan-500/20">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 py-3.5 flex justify-between items-center">
      
      <!-- Brand Logo -->
      <a href="#" class="flex items-center gap-3 group">
        <div class="relative w-11 h-11 rounded-xl bg-gradient-to-tr from-cyan-500 via-indigo-500 to-purple-600 flex items-center justify-center text-black font-black text-2xl shadow-lg shadow-cyan-500/30 group-hover:scale-105 transition-transform duration-300">
          <i class="fa-solid fa-bolt text-slate-950"></i>
          <span class="absolute -top-1 -right-1 w-3 h-3 bg-emerald-400 rounded-full border-2 border-slate-950 animate-ping"></span>
        </div>
        <div>
          <span class="text-2xl font-black font-display tracking-wider text-gradient text-glow">BIDSHOP</span>
          <span class="block text-[9px] text-cyan-400 tracking-widest uppercase font-semibold -mt-1">Digital Marketplace</span>
        </div>
      </a>

      <!-- Right Action / User Profile -->
      <div id="auth-buttons" class="flex items-center gap-3">
        <!-- Rendered via JS -->
      </div>
    </div>
  </nav>

  <!-- Hero Banner -->
  <header class="relative z-10 py-12 sm:py-16 px-4 text-center overflow-hidden">
    <!-- Ambient Light Glow behind hero -->
    <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-96 h-96 bg-gradient-to-tr from-cyan-500/20 to-purple-600/20 rounded-full blur-3xl pointer-events-none"></div>

    <div class="relative max-w-4xl mx-auto space-y-4">
      <div class="inline-flex items-center gap-2 bg-slate-900/80 border border-cyan-500/40 text-cyan-300 text-xs px-4 py-1.5 rounded-full font-medium shadow-lg shadow-cyan-500/10 backdrop-blur-md animate-float">
        <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
        <span>ระบบส่งของอัตโนมัติ 24/7 ปลอดภัย ไร้โกง 100%</span>
      </div>
      
      <h1 class="text-4xl sm:text-6xl font-black font-display tracking-tight text-white">
        ศูนย์รวมไอดีเกมและ <span class="text-gradient">สินค้าดิจิทัล</span>
      </h1>
      
      <p class="text-slate-400 text-sm sm:text-base max-w-2xl mx-auto font-light leading-relaxed">
        ซื้อไอดีเกม ROV, Valorant, Roblox และบัตรเติมเงิน ได้ทันทีด้วยระบบการชำระเงินอัตโนมัติ รับของทันทีหลังชำระเงิน
      </p>

      <!-- Stats Bar -->
      <div class="pt-6 grid grid-cols-2 sm:grid-cols-4 gap-3 max-w-3xl mx-auto">
        <div class="glass-panel p-3 rounded-2xl border border-slate-800">
          <div class="text-cyan-400 font-bold font-display text-xl">100%</div>
          <div class="text-xs text-slate-400">อัตโนมัติ</div>
        </div>
        <div class="glass-panel p-3 rounded-2xl border border-slate-800">
          <div class="text-purple-400 font-bold font-display text-xl">&lt; 5 วิ</div>
          <div class="text-xs text-slate-400">รับของทันที</div>
        </div>
        <div class="glass-panel p-3 rounded-2xl border border-slate-800">
          <div class="text-emerald-400 font-bold font-display text-xl">24 / 7</div>
          <div class="text-xs text-slate-400">เปิดให้บริการ</div>
        </div>
        <div class="glass-panel p-3 rounded-2xl border border-slate-800">
          <div class="text-pink-400 font-bold font-display text-xl">1,000+</div>
          <div class="text-xs text-slate-400">ลูกค้าไว้วางใจ</div>
        </div>
      </div>
    </div>
  </header>

  <!-- Main Container -->
  <main class="relative z-10 max-w-7xl mx-auto px-4 sm:px-6 py-4 flex-1 w-full space-y-8">
    
    <!-- User Dashboard Card (Visible when Logged In) -->
    <div id="user-dashboard" class="hidden rounded-3xl p-6 glass-panel border border-cyan-500/30 neon-border transition-all">
      <div class="flex flex-col lg:flex-row justify-between items-start lg:items-center gap-6">
        <div class="flex items-center gap-4">
          <div class="relative">
            <div class="w-14 h-14 rounded-2xl bg-gradient-to-tr from-cyan-500 to-purple-600 flex items-center justify-center text-slate-950 font-black text-2xl shadow-lg shadow-cyan-500/30">
              <i class="fa-solid fa-user-ninja"></i>
            </div>
            <span class="absolute -bottom-1 -right-1 w-4 h-4 bg-emerald-500 border-2 border-slate-950 rounded-full"></span>
          </div>
          <div>
            <div class="text-xs text-slate-400 font-light">บัญชีผู้ใช้งาน</div>
            <div class="text-xl font-bold text-white flex items-center gap-2">
              <span id="dash-username">User</span>
              <span id="dash-role-badge" class="text-[10px] px-2.5 py-0.5 rounded-full bg-cyan-950 text-cyan-400 border border-cyan-500/30 font-medium">Member</span>
            </div>
          </div>
        </div>

        <div class="flex flex-wrap items-center gap-4 w-full lg:w-auto justify-between lg:justify-end border-t lg:border-t-0 pt-4 lg:pt-0 border-slate-800">
          <div class="bg-slate-950/80 px-5 py-2.5 rounded-2xl border border-slate-800">
            <span class="text-xs text-slate-400 block font-light">เครดิตคงเหลือ</span>
            <div class="text-2xl font-black text-emerald-400 font-display">
              <span id="dash-balance">0.00</span> <span class="text-xs text-emerald-500">THB</span>
            </div>
          </div>
          <div class="flex flex-wrap gap-2">
            <button onclick="showTopupModal()" class="bg-gradient-to-r from-cyan-500 via-teal-400 to-emerald-400 hover:from-cyan-400 hover:to-emerald-300 text-slate-950 font-bold px-5 py-3 rounded-2xl transition-all shadow-lg shadow-cyan-500/25 flex items-center gap-2 text-sm active:scale-95">
              <i class="fa-solid fa-wallet text-base"></i> เติมเงิน
            </button>
            <button onclick="showInventoryModal()" class="bg-slate-800/90 hover:bg-slate-700 text-white font-medium px-4 py-3 rounded-2xl border border-slate-700 transition-all text-sm flex items-center gap-2 active:scale-95">
              <i class="fa-solid fa-box-open text-cyan-400"></i> ประวัติสั่งซื้อ
            </button>
            <button id="admin-toggle-btn" onclick="toggleAdminView()" class="hidden bg-purple-950/80 border border-purple-500/40 text-purple-300 hover:bg-purple-900 font-medium px-4 py-3 rounded-2xl transition-all text-sm flex items-center gap-2 active:scale-95">
              <i class="fa-solid fa-sliders"></i> ระบบหลังบ้าน
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- Admin Panel Control (Hidden by default) -->
    <div id="admin-panel" class="hidden rounded-3xl p-6 glass-panel border border-purple-500/40 bg-purple-950/10 space-y-4">
      <div class="flex justify-between items-center border-b border-purple-500/20 pb-3">
        <h3 class="text-lg font-bold text-purple-300 flex items-center gap-2">
          <i class="fa-solid fa-screwdriver-wrench"></i> ระบบหลังบ้าน - เพิ่มสต็อกสินค้า (Admin Console)
        </h3>
        <span class="text-xs bg-purple-900/60 text-purple-200 px-3 py-1 rounded-full border border-purple-500/30">แอดมินโหมด</span>
      </div>
      <div class="grid grid-cols-1 md:grid-cols-4 gap-3">
        <select id="admin-product-select" class="bg-slate-950 border border-slate-800 rounded-xl p-3 text-sm text-white focus:outline-none focus:border-purple-400">
          <!-- Dynamically filled -->
        </select>
        <input id="admin-stock-input" type="text" placeholder="ระบุข้อมูลสินค้า (เช่น USER|PASS หรือ CODE)" class="md:col-span-2 bg-slate-950 border border-slate-800 rounded-xl p-3 text-sm text-white focus:outline-none focus:border-purple-400" />
        <button onclick="addStockFromAdmin()" class="bg-purple-600 hover:bg-purple-500 text-white font-bold py-3 px-4 rounded-xl transition shadow-lg shadow-purple-600/30 text-sm">
          <i class="fa-solid fa-plus mr-1"></i> เติมสต็อกสินค้า
        </button>
      </div>
    </div>

    <!-- Filter & Search Bar -->
    <div class="flex flex-col md:flex-row justify-between items-center gap-4 bg-slate-900/40 p-3 rounded-2xl border border-slate-800/80 backdrop-blur-md">
      <!-- Search Input -->
      <div class="relative w-full md:w-80">
        <i class="fa-solid fa-magnifying-glass absolute left-4 top-1/2 -translate-y-1/2 text-slate-500"></i>
        <input id="search-input" oninput="renderProducts()" type="text" placeholder="ค้นหาไอดีเกม, โค้ดสินค้า..." class="w-full bg-slate-950/80 border border-slate-800 rounded-xl pl-11 pr-4 py-2.5 text-sm text-white focus:outline-none focus:border-cyan-500 transition" />
      </div>

      <!-- Categories Filter Tabs -->
      <div class="flex items-center gap-2 overflow-x-auto w-full md:w-auto pb-1 md:pb-0 custom-scrollbar">
        <button onclick="setCategory('all')" id="cat-all" class="cat-btn bg-cyan-500 text-slate-950 font-bold px-4 py-2 rounded-xl text-xs whitespace-nowrap transition">ทั้งหมด</button>
        <button onclick="setCategory('game')" id="cat-game" class="cat-btn bg-slate-950 text-slate-400 hover:text-white px-4 py-2 rounded-xl text-xs whitespace-nowrap border border-slate-800 transition">ไอดีเกม</button>
        <button onclick="setCategory('card')" id="cat-card" class="cat-btn bg-slate-950 text-slate-400 hover:text-white px-4 py-2 rounded-xl text-xs whitespace-nowrap border border-slate-800 transition">บัตรเติมเงิน</button>
        <button onclick="setCategory('app')" id="cat-app" class="cat-btn bg-slate-950 text-slate-400 hover:text-white px-4 py-2 rounded-xl text-xs whitespace-nowrap border border-slate-800 transition">แอปพรีเมียม</button>
      </div>
    </div>

    <!-- Product Grid -->
    <div id="product-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
      <!-- Dynamic Products Rendered Here -->
    </div>
  </main>

  <!-- Footer -->
  <footer class="relative z-10 bg-slate-950/90 border-t border-slate-900 py-10 text-center text-slate-500 text-sm mt-16 backdrop-blur-md">
    <div class="max-w-7xl mx-auto px-4 space-y-4">
      <div class="flex justify-center items-center gap-2">
        <div class="w-8 h-8 rounded-lg bg-gradient-to-tr from-cyan-500 to-purple-600 text-slate-950 flex items-center justify-center font-bold text-sm">B</div>
        <span class="text-white font-black tracking-wider text-lg font-display">BIDSHOP</span>
      </div>
      <p class="text-xs text-slate-500 max-w-md mx-auto">
        ระบบร้านค้าจำหน่ายสินค้าดิจิทัล 24 ชั่วโมง พร้อมระบบส่งมอบสินค้าอัตโนมัติ ออกแบบรองรับการแสดงผลบน GitHub Pages
      </p>
      <div class="flex justify-center gap-6 text-xs text-slate-400 pt-2">
        <a href="#" class="hover:text-cyan-400 transition"><i class="fa-solid fa-shield-halved mr-1"></i> นโยบายความเป็นส่วนตัว</a>
        <a href="#" class="hover:text-cyan-400 transition"><i class="fa-solid fa-file-contract mr-1"></i> ข้อกำหนดการใช้งาน</a>
        <a href="#" class="hover:text-cyan-400 transition"><i class="fa-solid fa-headset mr-1"></i> ติดต่อทีมงาน</a>
      </div>
      <p class="text-[11px] text-slate-600 pt-4 border-t border-slate-900/60">&copy; 2026 BIDSHOP. All rights reserved.</p>
    </div>
  </footer>

  <!-- Modal Backdrop Framework -->
  <div id="modal-backdrop" class="fixed inset-0 bg-slate-950/80 backdrop-blur-md hidden z-50 flex items-center justify-center p-4 transition-all duration-300">
    <div id="modal-box" class="glass-panel border border-cyan-500/30 w-full max-w-md rounded-3xl p-6 relative shadow-2xl neon-border transform transition-all scale-95 opacity-0">
      <button onclick="closeModal()" class="absolute top-4 right-4 text-slate-400 hover:text-white w-9 h-9 rounded-full bg-slate-800/80 border border-slate-700 flex items-center justify-center transition">&times;</button>
      <div id="modal-content"></div>
    </div>
  </div>

  <!-- Client-side JavaScript -->
  <script>
    /* ==========================================================================
       1. INTERACTIVE CANVAS PARTICLE BACKGROUND ENGINE
       ========================================================================== */
    const canvas = document.getElementById('bg-canvas');
    const ctx = canvas.getContext('2d');
    let particles = [];
    let mouse = { x: null, y: null, radius: 150 };

    function resizeCanvas() {
      canvas.width = window.innerWidth;
      canvas.height = window.innerHeight;
    }
    window.addEventListener('resize', resizeCanvas);
    resizeCanvas();

    window.addEventListener('mousemove', (e) => {
      mouse.x = e.x;
      mouse.y = e.y;
    });

    class Particle {
      constructor() {
        this.x = Math.random() * canvas.width;
        this.y = Math.random() * canvas.height;
        this.size = Math.random() * 2 + 1;
        this.baseX = this.x;
        this.baseY = this.y;
        this.vx = (Math.random() - 0.5) * 0.6;
        this.vy = (Math.random() - 0.5) * 0.6;
        this.color = Math.random() > 0.5 ? '#06b6d4' : '#a855f7';
      }

      draw() {
        ctx.beginPath();
        ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
        ctx.fillStyle = this.color;
        ctx.shadowBlur = 10;
        ctx.shadowColor = this.color;
        ctx.fill();
        ctx.shadowBlur = 0;
      }

      update() {
        this.x += this.vx;
        this.y += this.vy;

        if (this.x < 0 || this.x > canvas.width) this.vx *= -1;
        if (this.y < 0 || this.y > canvas.height) this.vy *= -1;

        // Interaction with mouse
        if (mouse.x && mouse.y) {
          let dx = mouse.x - this.x;
          let dy = mouse.y - this.y;
          let distance = Math.sqrt(dx * dx + dy * dy);
          if (distance < mouse.radius) {
            let force = (mouse.radius - distance) / mouse.radius;
            let directionX = dx / distance;
            let directionY = dy / distance;
            this.x -= directionX * force * 3;
            this.y -= directionY * force * 3;
          }
        }
      }
    }

    function initParticles() {
      particles = [];
      const particleCount = Math.floor((canvas.width * canvas.height) / 12000);
      for (let i = 0; i < particleCount; i++) {
        particles.push(new Particle());
      }
    }
    initParticles();

    function connectParticles() {
      for (let a = 0; a < particles.length; a++) {
        for (let b = a; b < particles.length; b++) {
          let dx = particles[a].x - particles[b].x;
          let dy = particles[a].y - particles[b].y;
          let distance = Math.sqrt(dx * dx + dy * dy);

          if (distance < 110) {
            let opacity = 1 - (distance / 110);
            ctx.strokeStyle = `rgba(6, 182, 212, ${opacity * 0.15})`;
            ctx.lineWidth = 1;
            ctx.beginPath();
            ctx.moveTo(particles[a].x, particles[a].y);
            ctx.lineTo(particles[b].x, particles[b].y);
            ctx.stroke();
          }
        }
      }
    }

    function animateCanvas() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      particles.forEach(p => {
        p.update();
        p.draw();
      });
      connectParticles();
      requestAnimationFrame(animateCanvas);
    }
    animateCanvas();


    /* ==========================================================================
       2. MOCK DATABASE & APPLICATION LOGIC (LocalStorage)
       ========================================================================== */
    const defaultProducts = [
      {
        id: 1,
        category: 'game',
        name: 'ไอดี Valorant | Prime Vandal + Karambit VIP',
        price: 150,
        image: 'https://placehold.co/600x350/090d16/06b6d4?text=Valorant+Prime+VIP',
        stock: [
          'USER: val_seller01 | PASS: PassValorant99#',
          'USER: val_seller02 | PASS: ValSecret2026!'
        ]
      },
      {
        id: 2,
        category: 'game',
        name: 'ไอดี ROV | ฮีโร่ 105 ตัว สกินเลเจนด์เพียบ',
        price: 290,
        image: 'https://placehold.co/600x350/090d16/3b82f6?text=ROV+Pro+Account',
        stock: [
          'USER: rov_master01 | PASS: RovPass_8899'
        ]
      },
      {
        id: 3,
        category: 'card',
        name: 'บัตรเติมเงิน TrueMoney 100 บาท',
        price: 100,
        image: 'https://placehold.co/600x350/090d16/10b981?text=TrueMoney+100+THB',
        stock: [
          'CODE: TM-100-8849-2041-9920',
          'CODE: TM-100-5512-8841-0034'
        ]
      },
      {
        id: 4,
        category: 'game',
        name: 'ไอดี Roblox | ติด Robux 1,500 R$ มีผลบล็อกแท้',
        price: 200,
        image: 'https://placehold.co/600x350/090d16/f59e0b?text=Roblox+BloxFruit+VIP',
        stock: [
          'USER: rblx_king99 | PASS: BloxPass2026'
        ]
      },
      {
        id: 5,
        category: 'app',
        name: 'YouTube Premium 1 เดือน (ส่วนตัว)',
        price: 45,
        image: 'https://placehold.co/600x350/090d16/ef4444?text=YouTube+Premium+1M',
        stock: [
          'INVITE-LINK: https://g.co/ytpremium/invite/demo12345'
        ]
      }
    ];

    let currentCategory = 'all';
    let isAdminView = false;

    function initStorage() {
      if (!localStorage.getItem('bidshop_users')) {
        localStorage.setItem('bidshop_users', JSON.stringify([]));
      }
      if (!localStorage.getItem('bidshop_products')) {
        localStorage.setItem('bidshop_products', JSON.stringify(defaultProducts));
      }
    }

    function getUsers() {
      return JSON.parse(localStorage.getItem('bidshop_users')) || [];
    }
    function saveUsers(users) {
      localStorage.setItem('bidshop_users', JSON.stringify(users));
    }
    function getProducts() {
      return JSON.parse(localStorage.getItem('bidshop_products')) || [];
    }
    function saveProducts(products) {
      localStorage.setItem('bidshop_products', JSON.stringify(products));
    }
    function getCurrentSession() {
      return JSON.parse(sessionStorage.getItem('bidshop_session'));
    }
    function setSession(user) {
      sessionStorage.setItem('bidshop_session', JSON.stringify(user));
    }
    function clearSession() {
      sessionStorage.removeItem('bidshop_session');
    }

    // Toast Notification System
    function showToast(message, type = 'info') {
      const container = document.getElementById('toast-container');
      const toast = document.createElement('div');
      
      const typeStyles = {
        success: 'bg-emerald-950/90 border-emerald-500/50 text-emerald-300',
        error: 'bg-rose-950/90 border-rose-500/50 text-rose-300',
        info: 'bg-slate-900/90 border-cyan-500/50 text-cyan-300'
      };

      const typeIcons = {
        success: 'fa-circle-check',
        error: 'fa-circle-xmark',
        info: 'fa-circle-info'
      };

      toast.className = `pointer-events-auto flex items-center gap-3 px-4 py-3 rounded-2xl border backdrop-blur-md shadow-2xl transition-all duration-300 transform translate-x-10 opacity-0 ${typeStyles[type]}`;
      toast.innerHTML = `
        <i class="fa-solid ${typeIcons[type]} text-lg"></i>
        <span class="text-sm font-medium">${message}</span>
      `;

      container.appendChild(toast);
      
      // Animate in
      setTimeout(() => {
        toast.classList.remove('translate-x-10', 'opacity-0');
      }, 10);

      // Animate out
      setTimeout(() => {
        toast.classList.add('translate-x-10', 'opacity-0');
        setTimeout(() => toast.remove(), 300);
      }, 3500);
    }

    // Category Filter & Search
    function setCategory(cat) {
      currentCategory = cat;
      document.querySelectorAll('.cat-btn').forEach(btn => {
        btn.className = 'cat-btn bg-slate-950 text-slate-400 hover:text-white px-4 py-2 rounded-xl text-xs whitespace-nowrap border border-slate-800 transition';
      });
      document.getElementById(`cat-${cat}`).className = 'cat-btn bg-gradient-to-r from-cyan-500 to-blue-600 text-slate-950 font-bold px-4 py-2 rounded-xl text-xs whitespace-nowrap transition shadow-lg shadow-cyan-500/20';
      renderProducts();
    }

    function renderProducts() {
      const products = getProducts();
      const searchQuery = document.getElementById('search-input').value.toLowerCase();
      const grid = document.getElementById('product-grid');

      const filtered = products.filter(p => {
        const matchesCategory = (currentCategory === 'all' || p.category === currentCategory);
        const matchesSearch = p.name.toLowerCase().includes(searchQuery);
        return matchesCategory && matchesSearch;
      });

      if (filtered.length === 0) {
        grid.innerHTML = `
          <div class="col-span-full py-16 text-center space-y-3">
            <i class="fa-solid fa-box-open text-4xl text-slate-600"></i>
            <p class="text-slate-400 text-sm">ไม่พบรายการสินค้าที่ค้นหา</p>
          </div>
        `;
        return;
      }

      grid.innerHTML = filtered.map(p => {
        const stockCount = p.stock.length;
        return `
          <div class="glass-card rounded-3xl overflow-hidden flex flex-col justify-between group">
            <div>
              <div class="relative overflow-hidden">
                <img src="${p.image}" alt="${p.name}" class="w-full h-44 object-cover group-hover:scale-105 transition-transform duration-500" />
                <div class="absolute inset-0 bg-gradient-to-t from-slate-950 via-transparent to-transparent opacity-80"></div>
                
                <!-- Category Badge -->
                <span class="absolute top-3 left-3 text-[10px] font-bold px-2.5 py-1 rounded-full bg-slate-900/80 text-cyan-300 border border-cyan-500/30 backdrop-blur-md uppercase">
                  ${p.category}
                </span>

                <!-- Stock Badge -->
                <span class="absolute top-3 right-3 text-[10px] font-bold px-2.5 py-1 rounded-full ${stockCount > 0 ? 'bg-emerald-950/90 text-emerald-300 border border-emerald-500/40' : 'bg-rose-950/90 text-rose-300 border border-rose-500/40'} backdrop-blur-md">
                  ${stockCount > 0 ? `พร้อมส่ง (${stockCount})` : 'สินค้าหมด'}
                </span>
              </div>

              <div class="p-5">
                <h3 class="font-bold text-base text-white line-clamp-2 mb-3 group-hover:text-cyan-300 transition-colors leading-snug">${p.name}</h3>
                <div class="flex items-baseline gap-1">
                  <span class="text-2xl font-black text-cyan-400 font-display">${p.price}</span>
                  <span class="text-xs text-slate-400">THB</span>
                </div>
              </div>
            </div>

            <div class="px-5 pb-5">
              <button onclick="buyProduct(${p.id})" ${stockCount === 0 ? 'disabled' : ''} class="w-full ${stockCount > 0 ? 'bg-gradient-to-r from-cyan-500 via-teal-400 to-blue-500 hover:from-cyan-400 hover:to-blue-400 text-slate-950 shadow-lg shadow-cyan-500/20 active:scale-95' : 'bg-slate-800/80 text-slate-500 cursor-not-allowed'} font-bold py-2.5 rounded-2xl transition-all flex items-center justify-center gap-2 text-sm">
                <i class="fa-solid fa-cart-shopping"></i> ${stockCount > 0 ? 'สั่งซื้อทันที' : 'สินค้าหมด'}
              </button>
            </div>
          </div>
        `;
      }).join('');

      // Render Admin Dropdown options
      const adminSelect = document.getElementById('admin-product-select');
      adminSelect.innerHTML = products.map(p => `<option value="${p.id}">${p.name} (คงเหลือ: ${p.stock.length})</option>`).join('');
    }

    // Modal Manager
    function showModal(html) {
      const backdrop = document.getElementById('modal-backdrop');
      const box = document.getElementById('modal-box');
      document.getElementById('modal-content').innerHTML = html;
      
      backdrop.classList.remove('hidden');
      setTimeout(() => {
        box.classList.remove('scale-95', 'opacity-0');
        box.classList.add('scale-100', 'opacity-100');
      }, 10);
    }

    function closeModal() {
      const backdrop = document.getElementById('modal-backdrop');
      const box = document.getElementById('modal-box');
      
      box.classList.remove('scale-100', 'opacity-100');
      box.classList.add('scale-95', 'opacity-0');
      
      setTimeout(() => {
        backdrop.classList.add('hidden');
      }, 200);
    }

    // User State & Load Data
    function loadData() {
      initStorage();
      const sessionUser = getCurrentSession();
      const authDiv = document.getElementById('auth-buttons');
      const dashDiv = document.getElementById('user-dashboard');

      if (sessionUser) {
        const users = getUsers();
        const freshUser = users.find(u => u.username === sessionUser.username) || sessionUser;
        
        dashDiv.classList.remove('hidden');
        document.getElementById('dash-username').innerText = freshUser.username;
        document.getElementById('dash-balance').innerText = freshUser.balance.toFixed(2);
        
        // Check if Admin
        if (freshUser.username.toLowerCase() === 'admin') {
          document.getElementById('admin-toggle-btn').classList.remove('hidden');
          document.getElementById('dash-role-badge').innerText = 'Administrator';
          document.getElementById('dash-role-badge').className = 'text-[10px] px-2.5 py-0.5 rounded-full bg-purple-950 text-purple-300 border border-purple-500/40 font-medium';
        }

        authDiv.innerHTML = `
          <button onclick="logout()" class="bg-rose-500/10 text-rose-400 border border-rose-500/30 hover:bg-rose-500 hover:text-white px-4 py-2 rounded-2xl text-xs font-semibold transition active:scale-95 flex items-center gap-1.5">
            <i class="fa-solid fa-right-from-bracket"></i> ออกจากระบบ
          </button>
        `;
      } else {
        dashDiv.classList.add('hidden');
        authDiv.innerHTML = `
          <button onclick="showLoginModal()" class="bg-slate-900/80 text-cyan-400 border border-slate-700 hover:border-cyan-500 px-4 py-2 rounded-2xl text-xs font-semibold transition active:scale-95">เข้าสู่ระบบ</button>
          <button onclick="showRegisterModal()" class="bg-gradient-to-r from-cyan-500 to-blue-600 hover:from-cyan-400 hover:to-blue-500 text-slate-950 font-bold px-4 py-2 rounded-2xl text-xs transition shadow-lg shadow-cyan-500/20 active:scale-95">สมัครสมาชิก</button>
        `;
      }

      renderProducts();
    }

    // Auth Actions
    function showLoginModal() {
      showModal(`
        <h3 class="text-xl font-bold mb-4 text-white flex items-center gap-2">
          <i class="fa-solid fa-shield-halved text-cyan-400"></i> เข้าสู่ระบบ BIDSHOP
        </h3>
        <div class="space-y-4">
          <div>
            <label class="text-xs text-slate-400 block mb-1.5">ชื่อผู้ใช้งาน</label>
            <input id="l-user" type="text" placeholder="พิมพ์ชื่อผู้ใช้งาน" class="w-full bg-slate-950 border border-slate-800 rounded-xl p-3 text-sm text-white focus:outline-none focus:border-cyan-400 transition" />
          </div>
          <div>
            <label class="text-xs text-slate-400 block mb-1.5">รหัสผ่าน</label>
            <input id="l-pass" type="password" placeholder="พิมพ์รหัสผ่าน" class="w-full bg-slate-950 border border-slate-800 rounded-xl p-3 text-sm text-white focus:outline-none focus:border-cyan-400 transition" />
          </div>
          <button onclick="login()" class="w-full bg-gradient-to-r from-cyan-500 to-blue-600 hover:from-cyan-400 hover:to-blue-500 text-slate-950 font-bold py-3 rounded-xl transition shadow-lg shadow-cyan-500/25 active:scale-95 mt-2">
            ยืนยันเข้าสู่ระบบ
          </button>
        </div>
      `);
    }

    function showRegisterModal() {
      showModal(`
        <h3 class="text-xl font-bold mb-4 text-white flex items-center gap-2">
          <i class="fa-solid fa-user-plus text-cyan-400"></i> สมัครสมาชิกใหม่
        </h3>
        <div class="space-y-4">
          <div>
            <label class="text-xs text-slate-400 block mb-1.5">ตั้งชื่อผู้ใช้งาน (พิมพ์ admin เพื่อลองโหมดแอดมิน)</label>
            <input id="r-user" type="text" placeholder="ระบุชื่อผู้ใช้งาน" class="w-full bg-slate-950 border border-slate-800 rounded-xl p-3 text-sm text-white focus:outline-none focus:border-cyan-400 transition" />
          </div>
          <div>
            <label class="text-xs text-slate-400 block mb-1.5">ตั้งรหัสผ่าน</label>
            <input id="r-pass" type="password" placeholder="ระบุรหัสผ่าน" class="w-full bg-slate-950 border border-slate-800 rounded-xl p-3 text-sm text-white focus:outline-none focus:border-cyan-400 transition" />
          </div>
          <button onclick="register()" class="w-full bg-gradient-to-r from-cyan-500 via-teal-400 to-emerald-400 hover:from-cyan-400 hover:to-emerald-300 text-slate-950 font-bold py-3 rounded-xl transition shadow-lg shadow-cyan-500/25 active:scale-95 mt-2">
            สมัครสมาชิกทันที
          </button>
        </div>
      `);
    }

    function register() {
      const uInput = document.getElementById('r-user').value.trim();
      const pInput = document.getElementById('r-pass').value.trim();

      if (!uInput || !pInput) return showToast('กรุณากรอกข้อมูลให้ครบถ้วน', 'error');

      const users = getUsers();
      if (users.find(u => u.username === uInput)) {
        return showToast('ชื่อผู้ใช้นี้มีในระบบแล้ว', 'error');
      }

      const newUser = {
        username: uInput,
        password: pInput,
        balance: 0,
        inventory: []
      };

      users.push(newUser);
      saveUsers(users);
      setSession(newUser);
      
      closeModal();
      showToast(`สมัครสมาชิกสำเร็จ! ยินดีต้อนรับ ${uInput}`, 'success');
      loadData();
    }

    function login() {
      const uInput = document.getElementById('l-user').value.trim();
      const pInput = document.getElementById('l-pass').value.trim();

      const users = getUsers();
      const user = users.find(u => u.username === uInput && u.password === pInput);

      if (!user) {
        return showToast('ชื่อผู้ใช้หรือรหัสผ่านไม่ถูกต้อง', 'error');
      }

      setSession(user);
      closeModal();
      showToast(`เข้าสู่ระบบสำเร็จ ยินดีต้อนรับ ${user.username}`, 'success');
      loadData();
    }

    function logout() {
      clearSession();
      showToast('ออกจากระบบเรียบร้อยแล้ว', 'info');
      loadData();
    }

    // Topup Modal & Action
    function showTopupModal() {
      showModal(`
        <h3 class="text-xl font-bold mb-1 text-white flex items-center gap-2">
          <i class="fa-solid fa-qrcode text-cyan-400"></i> เติมเงินผ่าน QR Code
        </h3>
        <p class="text-xs text-slate-400 mb-4">สแกน QR Code แล้วกรอกจำนวนเงินที่โอนเพื่อปรับยอดจำลอง</p>
        
        <div class="bg-white p-4 rounded-2xl text-center max-w-[200px] mx-auto mb-4 shadow-xl">
          <img src="https://api.qrserver.com/v1/create-qr-code/?size=180x180&data=BIDSHOP_SIMULATE_PAYMENT" alt="PromptPay QR" class="w-full h-auto" />
          <span class="text-[10px] text-slate-800 font-bold block mt-1 tracking-wider">PROMPTPAY AUTOMATIC</span>
        </div>

        <div class="space-y-4">
          <div>
            <label class="text-xs text-slate-400 block mb-1">จำนวนเงินที่โอน (บาท)</label>
            <input id="t-amount" type="number" value="100" class="w-full bg-slate-950 border border-slate-800 rounded-xl p-3 text-center text-xl font-black text-emerald-400 font-display focus:outline-none focus:border-cyan-400 transition" />
          </div>
          <button onclick="topup()" class="w-full bg-gradient-to-r from-emerald-500 to-teal-400 hover:from-emerald-400 hover:to-teal-300 text-slate-950 font-bold py-3 rounded-xl transition shadow-lg shadow-emerald-500/20 active:scale-95">
            ยืนยันการแจ้งชำระเงิน
          </button>
        </div>
      `);
    }

    function topup() {
      const amount = parseFloat(document.getElementById('t-amount').value);
      if (isNaN(amount) || amount <= 0) return showToast('จำนวนเงินไม่ถูกต้อง', 'error');

      const sessionUser = getCurrentSession();
      const users = getUsers();
      const user = users.find(u => u.username === sessionUser.username);

      user.balance += amount;
      saveUsers(users);
      setSession(user);

      showToast(`เติมเงินสำเร็จ +${amount.toFixed(2)} THB`, 'success');
      closeModal();
      loadData();
    }

    // Purchase Logic
    function buyProduct(productId) {
      const sessionUser = getCurrentSession();
      if (!sessionUser) return showLoginModal();

      const products = getProducts();
      const product = products.find(p => p.id === productId);

      if (!product || product.stock.length === 0) {
        return showToast('ขออภัย สินค้าชิ้นนี้หมดแล้ว', 'error');
      }

      const users = getUsers();
      const user = users.find(u => u.username === sessionUser.username);

      if (user.balance < product.price) {
        return showToast('ยอดเงินของคุณไม่พอ กรุณาเติมเงินก่อนสั่งซื้อ', 'error');
      }

      // Execute Purchase
      user.balance -= product.price;
      const itemData = product.stock.shift();
      
      user.inventory.push({
        productName: product.name,
        data: itemData,
        date: new Date().toLocaleString('th-TH')
      });

      saveUsers(users);
      saveProducts(products);
      setSession(user);

      showModal(`
        <div class="text-center py-2">
          <div class="w-16 h-16 bg-emerald-950/90 text-emerald-400 border border-emerald-500/40 rounded-full flex items-center justify-center text-3xl mx-auto mb-3 shadow-lg shadow-emerald-500/30 animate-bounce">
            <i class="fa-solid fa-check"></i>
          </div>
          <h3 class="text-xl font-bold text-white mb-1">สั่งซื้อสำเร็จ!</h3>
          <p class="text-xs text-slate-400 mb-4">ระบบได้จัดส่งข้อมูลสินค้าให้ท่านแล้วเรียบร้อย</p>
          
          <div class="bg-slate-950 p-4 rounded-2xl border border-cyan-500/40 text-emerald-400 font-mono text-sm font-bold break-all mb-4 select-all shadow-inner">
            ${itemData}
          </div>
          
          <button onclick="closeModal()" class="w-full bg-cyan-500 hover:bg-cyan-400 text-slate-950 font-bold py-3 rounded-xl transition active:scale-95">
            ตกลง
          </button>
        </div>
      `);

      showToast('สั่งซื้อสำเร็จ! รับสินค้าผ่านหน้าจอทันที', 'success');
      loadData();
    }

    // Inventory Modal
    function showInventoryModal() {
      const sessionUser = getCurrentSession();
      if (!sessionUser) return;
      const users = getUsers();
      const user = users.find(u => u.username === sessionUser.username);
      const inventory = user.inventory || [];

      showModal(`
        <h3 class="text-xl font-bold mb-4 text-white flex items-center gap-2">
          <i class="fa-solid fa-box-open text-cyan-400"></i> ประวัติการสั่งซื้อของคุณ
        </h3>
        <div class="max-h-80 overflow-y-auto space-y-3 pr-1 custom-scrollbar">
          ${inventory.length === 0 ? '<p class="text-slate-500 text-center py-8 text-sm">ยังไม่มีรายการสั่งซื้อ</p>' : inventory.slice().reverse().map(item => `
            <div class="bg-slate-950 p-4 rounded-2xl border border-slate-800">
              <div class="text-xs font-bold text-cyan-400 mb-1">${item.productName}</div>
              <div class="text-[10px] text-slate-500 mb-2"><i class="fa-regular fa-clock mr-1"></i>${item.date}</div>
              <div class="bg-slate-900/90 p-3 rounded-xl border border-slate-800 text-emerald-400 font-mono text-xs break-all font-semibold select-all">
                ${item.data}
              </div>
            </div>
          `).join('')}
        </div>
      `);
    }

    // Admin Controls
    function toggleAdminView() {
      isAdminView = !isAdminView;
      const panel = document.getElementById('admin-panel');
      if (isAdminView) {
        panel.classList.remove('hidden');
        showToast('เปิดใช้งาน Admin Console', 'info');
      } else {
        panel.classList.add('hidden');
      }
    }

    function addStockFromAdmin() {
      const prodId = parseInt(document.getElementById('admin-product-select').value);
      const stockVal = document.getElementById('admin-stock-input').value.trim();

      if (!stockVal) return showToast('กรุณาระบุข้อมูลสินค้าสต็อก', 'error');

      const products = getProducts();
      const product = products.find(p => p.id === prodId);

      if (product) {
        product.stock.push(stockVal);
        saveProducts(products);
        document.getElementById('admin-stock-input').value = '';
        showToast(`เติมสต็อกให้ ${product.name} สำเร็จ`, 'success');
        renderProducts();
      }
    }

    // Initialize Page
    window.onload = function() {
      loadData();
    };
  </script>
</body>
</html>