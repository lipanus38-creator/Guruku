<!DOCTYPE html>
<html lang="id" class="h-full">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Sistem Manajemen Pembelajaran Guru</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <script src="/_sdk/data_sdk.js"></script>
  <script src="/_sdk/element_sdk.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
  <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
  <style>
    body {
      box-sizing: border-box;
      font-family: 'Plus Jakarta Sans', sans-serif;
    }
    
    @keyframes marquee {
      0% { transform: translateX(100%); }
      100% { transform: translateX(-100%); }
    }
    
    .marquee-text {
      animation: marquee 20s linear infinite;
    }
    
    .marquee-container:hover .marquee-text {
      animation-play-state: paused;
    }
    
    @keyframes float {
      0%, 100% { transform: translateY(0); }
      50% { transform: translateY(-10px); }
    }
    
    .floating-btn {
      animation: float 3s ease-in-out infinite;
    }
    
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }
    
    .fade-in {
      animation: fadeIn 0.5s ease-out forwards;
    }
    
    .card-hover {
      transition: all 0.3s ease;
    }
    
    .card-hover:hover {
      transform: translateY(-5px);
      box-shadow: 0 20px 40px rgba(59, 130, 246, 0.15);
    }
    
    .gradient-bg {
      background: linear-gradient(135deg, #1e40af 0%, #3b82f6 50%, #60a5fa 100%);
    }
    
    .glass-effect {
      background: rgba(255, 255, 255, 0.95);
      backdrop-filter: blur(10px);
    }
    
    .nav-item {
      position: relative;
    }
    
    .nav-item::after {
      content: '';
      position: absolute;
      bottom: -2px;
      left: 50%;
      width: 0;
      height: 2px;
      background: #3b82f6;
      transition: all 0.3s ease;
      transform: translateX(-50%);
    }
    
    .nav-item:hover::after,
    .nav-item.active::after {
      width: 100%;
    }
    
    .modal-overlay {
      background: rgba(0, 0, 0, 0.5);
      backdrop-filter: blur(4px);
    }
    
    .table-container {
      overflow-x: auto;
    }
    
    .table-container::-webkit-scrollbar {
      height: 6px;
    }
    
    .table-container::-webkit-scrollbar-track {
      background: #f1f5f9;
      border-radius: 3px;
    }
    
    .table-container::-webkit-scrollbar-thumb {
      background: #cbd5e1;
      border-radius: 3px;
    }
    
    .table-container::-webkit-scrollbar-thumb:hover {
      background: #94a3b8;
    }
    
    input:focus, select:focus, textarea:focus {
      outline: none;
      ring: 2px;
      ring-color: #3b82f6;
    }

    .icon-card {
      font-size: 3rem;
      line-height: 1;
    }

    .profile-card {
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    }

    .assessment-icon-pink { background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%); }
    .assessment-icon-blue { background: linear-gradient(135deg, #4facfe 0%, #00f2fe 100%); }
    .assessment-icon-purple { background: linear-gradient(135deg, #43e97b 0%, #38f9d7 100%); }
    .assessment-icon-orange { background: linear-gradient(135deg, #fa709a 0%, #fee140 100%); }
    .assessment-icon-green { background: linear-gradient(135deg, #30cfd0 0%, #330867 100%); }
    .assessment-icon-red { background: linear-gradient(135deg, #ff6b6b 0%, #ee5a6f 100%); }
    .assessment-icon-yellow { background: linear-gradient(135deg, #ffa751 0%, #ffe259 100%); }

    @media print {
      body { margin: 0; padding: 0; }
      .no-print { display: none !important; }
    }
  </style>
</head>
<body class="h-full bg-slate-50 text-slate-800">
  <div id="app" class="h-full overflow-auto">
    
    <!-- Running Text Announcement -->
    <div id="announcement-bar" class="gradient-bg text-white py-2 overflow-hidden">
      <div class="marquee-container relative">
        <div id="marquee-content" class="marquee-text whitespace-nowrap text-sm font-medium">
          📢 Selamat datang di Sistem Manajemen Pembelajaran Guru | Silakan cek pengumuman terbaru!
        </div>
      </div>
    </div>
    
    <!-- Header -->
    <header class="glass-effect sticky top-0 z-40 shadow-lg border-b border-slate-200">
      <div class="max-w-7xl mx-auto px-4">
        <div class="flex items-center justify-between py-4">
          <!-- Logo & Title -->
          <div class="flex items-center gap-3">
            <div class="w-12 h-12 gradient-bg rounded-xl flex items-center justify-center shadow-lg">
              <svg class="w-7 h-7 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253"/>
              </svg>
            </div>
            <div>
              <h1 id="site-title" class="text-xl font-bold text-slate-800">Sistem Pembelajaran</h1>
              <p id="school-name" class="text-xs text-slate-500">Portal Manajemen Guru</p>
            </div>
          </div>
          
          <!-- Social Media Icons -->
          <div id="social-icons" class="hidden md:flex items-center gap-3">
            <a id="instagram-link" href="#" target="_blank" rel="noopener noreferrer" class="w-9 h-9 bg-gradient-to-br from-purple-500 to-pink-500 rounded-lg flex items-center justify-center text-white hover:scale-110 transition-transform shadow-md" title="Instagram">
              <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/></svg>
            </a>
            <a id="youtube-link" href="#" target="_blank" rel="noopener noreferrer" class="w-9 h-9 bg-red-600 rounded-lg flex items-center justify-center text-white hover:scale-110 transition-transform shadow-md" title="YouTube">
              <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M23.498 6.186a3.016 3.016 0 0 0-2.122-2.136C19.505 3.545 12 3.545 12 3.545s-7.505 0-9.377.505A3.017 3.017 0 0 0 .502 6.186C0 8.07 0 12 0 12s0 3.93.502 5.814a3.016 3.016 0 0 0 2.122 2.136c1.871.505 9.376.505 9.376.505s7.505 0 9.377-.505a3.015 3.015 0 0 0 2.122-2.136C24 15.93 24 12 24 12s0-3.93-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z"/></svg>
            </a>
            <a id="tiktok-link" href="#" target="_blank" rel="noopener noreferrer" class="w-9 h-9 bg-black rounded-lg flex items-center justify-center text-white hover:scale-110 transition-transform shadow-md" title="TikTok">
              <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M12.525.02c1.31-.02 2.61-.01 3.91-.02.08 1.53.63 3.09 1.75 4.17 1.12 1.11 2.7 1.62 4.24 1.79v4.03c-1.44-.05-2.89-.35-4.2-.97-.57-.26-1.1-.59-1.62-.93-.01 2.92.01 5.84-.02 8.75-.08 1.4-.54 2.79-1.35 3.94-1.31 1.92-3.58 3.17-5.91 3.21-1.43.08-2.86-.31-4.08-1.03-2.02-1.19-3.44-3.37-3.65-5.71-.02-.5-.03-1-.01-1.49.18-1.9 1.12-3.72 2.58-4.96 1.66-1.44 3.98-2.13 6.15-1.72.02 1.48-.04 2.96-.04 4.44-.99-.32-2.15-.23-3.02.37-.63.41-1.11 1.04-1.36 1.75-.21.51-.15 1.07-.14 1.61.24 1.64 1.82 3.02 3.5 2.87 1.12-.01 2.19-.66 2.77-1.61.19-.33.4-.67.41-1.06.1-1.79.06-3.57.07-5.36.01-4.03-.01-8.05.02-12.07z"/></svg>
            </a>
            <a id="facebook-link" href="#" target="_blank" rel="noopener noreferrer" class="w-9 h-9 bg-blue-600 rounded-lg flex items-center justify-center text-white hover:scale-110 transition-transform shadow-md" title="Facebook">
              <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/></svg>
            </a>
          </div>
          
          <!-- Auth Button -->
          <div id="auth-section" class="flex items-center gap-2">
            <button id="login-btn" onclick="showLoginModal()" class="px-5 py-2.5 bg-blue-600 text-white rounded-xl font-semibold hover:bg-blue-700 transition-all shadow-md hover:shadow-lg text-sm">
              Login Guru
            </button>
            <div id="logged-in-section" class="hidden flex items-center gap-2">
              <span id="user-greeting" class="text-sm font-medium text-slate-600 hidden md:block">Halo, Guru!</span>
              <button onclick="showDashboard()" class="px-4 py-2.5 bg-emerald-600 text-white rounded-xl font-semibold hover:bg-emerald-700 transition-all shadow-md text-sm">
                Dashboard
              </button>
              <button onclick="logout()" class="px-4 py-2.5 bg-slate-200 text-slate-700 rounded-xl font-semibold hover:bg-slate-300 transition-all text-sm">
                Logout
              </button>
            </div>
          </div>
        </div>
        
        <!-- Navigation -->
        <nav class="flex items-center gap-1 pb-3 overflow-x-auto" id="main-nav">
          <button onclick="navigateTo('home')" class="nav-item px-4 py-2 text-sm font-medium text-slate-600 hover:text-blue-600 rounded-lg hover:bg-blue-50 transition-all whitespace-nowrap" data-page="home">Home</button>
          <button onclick="navigateTo('materi')" class="nav-item px-4 py-2 text-sm font-medium text-slate-600 hover:text-blue-600 rounded-lg hover:bg-blue-50 transition-all whitespace-nowrap" data-page="materi">Materi</button>
          <button onclick="navigateTo('bank-soal')" class="nav-item px-4 py-2 text-sm font-medium text-slate-600 hover:text-blue-600 rounded-lg hover:bg-blue-50 transition-all whitespace-nowrap" data-page="bank-soal">Bank Soal</button>
          <button onclick="navigateTo('asesmen')" class="nav-item px-4 py-2 text-sm font-medium text-slate-600 hover:text-blue-600 rounded-lg hover:bg-blue-50 transition-all whitespace-nowrap" data-page="asesmen">Asesmen</button>
          <button onclick="navigateTo('nilai')" class="nav-item px-4 py-2 text-sm font-medium text-slate-600 hover:text-blue-600 rounded-lg hover:bg-blue-50 transition-all whitespace-nowrap" data-page="nilai">Nilai</button>
          <button onclick="navigateTo('kehadiran')" class="nav-item px-4 py-2 text-sm font-medium text-slate-600 hover:text-blue-600 rounded-lg hover:bg-blue-50 transition-all whitespace-nowrap" data-page="kehadiran">Kehadiran</button>
          <button onclick="navigateTo('publikasi')" class="nav-item px-4 py-2 text-sm font-medium text-slate-600 hover:text-blue-600 rounded-lg hover:bg-blue-50 transition-all whitespace-nowrap" data-page="publikasi">Publikasi</button>
          <button onclick="navigateTo('download')" class="nav-item px-4 py-2 text-sm font-medium text-slate-600 hover:text-blue-600 rounded-lg hover:bg-blue-50 transition-all whitespace-nowrap" data-page="download">Download</button>
          <button onclick="navigateTo('akademik')" class="nav-item px-4 py-2 text-sm font-medium text-slate-600 hover:text-blue-600 rounded-lg hover:bg-blue-50 transition-all whitespace-nowrap" data-page="akademik">Akademik</button>
        </nav>
      </div>
    </header>
    
    <!-- Main Content Area -->
    <main id="main-content" class="max-w-7xl mx-auto px-4 py-8 h-full">
      <!-- Content will be dynamically loaded here -->
    </main>
    
    <!-- Floating Action Buttons -->
    <div class="no-print fixed bottom-6 right-6 flex flex-col gap-3 z-50">
      <!-- WhatsApp Button -->
      <a href="https://wa.me/6285651222693" target="_blank" rel="noopener noreferrer" class="floating-btn w-14 h-14 bg-green-500 rounded-full flex items-center justify-center text-white shadow-xl hover:bg-green-600 transition-all hover:scale-110" title="Chat WhatsApp">
        <svg class="w-7 h-7" fill="currentColor" viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
      </a>
      
      <!-- Chat Button -->
      <button onclick="showChatModal()" class="floating-btn w-14 h-14 bg-blue-600 rounded-full flex items-center justify-center text-white shadow-xl hover:bg-blue-700 transition-all hover:scale-110" title="Chat">
        <svg class="w-7 h-7" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z"/></svg>
      </button>
    </div>
    
    <!-- Login Modal -->
    <div id="login-modal" class="no-print fixed inset-0 z-50 hidden">
      <div class="modal-overlay absolute inset-0" onclick="hideLoginModal()"></div>
      <div class="absolute inset-0 flex items-center justify-center p-4">
        <div class="bg-white rounded-2xl shadow-2xl w-full max-w-md p-8 relative fade-in">
          <button onclick="hideLoginModal()" class="absolute top-4 right-4 w-8 h-8 flex items-center justify-center rounded-full hover:bg-slate-100 transition-colors">
            <svg class="w-5 h-5 text-slate-500" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/></svg>
          </button>
          
          <div class="text-center mb-6">
            <div class="w-16 h-16 gradient-bg rounded-2xl flex items-center justify-center mx-auto mb-4 shadow-lg">
              <svg class="w-8 h-8 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z"/></svg>
            </div>
            <h2 class="text-2xl font-bold text-slate-800">Login Guru</h2>
            <p class="text-slate-500 text-sm mt-1">Masuk untuk mengelola pembelajaran</p>
          </div>
          
          <form id="login-form" onsubmit="handleLogin(event)">
            <div class="space-y-4">
              <div>
                <label for="username" class="block text-sm font-medium text-slate-700 mb-1">Username</label>
                <input type="text" id="username" name="username" required class="w-full px-4 py-3 border border-slate-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-all" placeholder="Masukkan username">
              </div>
              <div>
                <label for="password" class="block text-sm font-medium text-slate-700 mb-1">Password</label>
                <input type="password" id="password" name="password" required class="w-full px-4 py-3 border border-slate-300 rounded-xl focus:ring-2 focus:ring-blue-500 focus:border-blue-500 transition-all" placeholder="Masukkan password">
              </div>
            </div>
            
            <div id="login-error" class="hidden mt-4 p-3 bg-red-50 border border-red-200 rounded-xl text-red-600 text-sm"></div>
            
            <button type="submit" class="w-full mt-6 px-6 py-3 bg-blue-600 text-white rounded-xl font-semibold hover:bg-blue-700 transition-all shadow-lg hover:shadow-xl">
              Masuk
            </button>
            
            <p class="text-center text-xs text-slate-500 mt-4">
              Default: admin / admin123
            </p>
          </form>
        </div>
      </div>
    </div>
    
    <!-- Data Modal (Add/Edit) -->
    <div id="data-modal" class="no-print fixed inset-0 z-50 hidden">
      <div class="modal-overlay absolute inset-0" onclick="hideDataModal()"></div>
      <div class="absolute inset-0 flex items-center justify-center p-4 overflow-y-auto">
        <div class="bg-white rounded-2xl shadow-2xl w-full max-w-2xl p-8 relative fade-in my-8">
          <button onclick="hideDataModal()" class="absolute top-4 right-4 w-8 h-8 flex items-center justify-center rounded-full hover:bg-slate-100 transition-colors">
            <svg class="w-5 h-5 text-slate-500" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/></svg>
          </button>
          
          <h2 id="modal-title" class="text-2xl font-bold text-slate-800 mb-6">Tambah Data</h2>
          
          <form id="data-form" onsubmit="handleDataSubmit(event)">
            <div id="form-fields" class="space-y-4">
              <!-- Dynamic form fields will be inserted here -->
            </div>
            
            <div class="flex gap-3 mt-6">
              <button type="button" onclick="hideDataModal()" class="flex-1 px-6 py-3 bg-slate-200 text-slate-700 rounded-xl font-semibold hover:bg-slate-300 transition-all">
                Batal
              </button>
              <button type="submit" id="submit-btn" class="flex-1 px-6 py-3 bg-blue-600 text-white rounded-xl font-semibold hover:bg-blue-700 transition-all shadow-lg">
                Simpan
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
    
    <!-- Delete Confirmation Modal -->
    <div id="delete-modal" class="no-print fixed inset-0 z-50 hidden">
      <div class="modal-overlay absolute inset-0" onclick="hideDeleteModal()"></div>
      <div class="absolute inset-0 flex items-center justify-center p-4">
        <div class="bg-white rounded-2xl shadow-2xl w-full max-w-md p-8 relative fade-in">
          <div class="text-center">
            <div class="w-16 h-16 bg-red-100 rounded-full flex items-center justify-center mx-auto mb-4">
              <svg class="w-8 h-8 text-red-600" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/></svg>
            </div>
            <h2 class="text-2xl font-bold text-slate-800 mb-2">Hapus Data?</h2>
            <p class="text-slate-500">Data yang dihapus tidak dapat dikembalikan.</p>
          </div>
          
          <div class="flex gap-3 mt-6">
            <button onclick="hideDeleteModal()" class="flex-1 px-6 py-3 bg-slate-200 text-slate-700 rounded-xl font-semibold hover:bg-slate-300 transition-all">
              Batal
            </button>
            <button onclick="confirmDelete()" class="flex-1 px-6 py-3 bg-red-600 text-white rounded-xl font-semibold hover:bg-red-700 transition-all shadow-lg">
              Hapus
            </button>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Chat Modal -->
    <div id="chat-modal" class="no-print fixed inset-0 z-50 hidden">
      <div class="modal-overlay absolute inset-0" onclick="hideChatModal()"></div>
      <div class="absolute inset-0 flex items-center justify-center p-4">
        <div class="bg-white rounded-2xl shadow-2xl w-full max-w-md p-6 relative fade-in">
          <button onclick="hideChatModal()" class="absolute top-4 right-4 w-8 h-8 flex items-center justify-center rounded-full hover:bg-slate-100 transition-colors">
            <svg class="w-5 h-5 text-slate-500" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/></svg>
          </button>
          
          <div class="text-center">
            <div class="w-16 h-16 bg-blue-100 rounded-full flex items-center justify-center mx-auto mb-4">
              <svg class="w-8 h-8 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z"/></svg>
            </div>
            <h2 class="text-xl font-bold text-slate-800 mb-2">Fitur Chat</h2>
            <p class="text-slate-500 text-sm mb-4">Fitur chat internal akan segera tersedia. Untuk saat ini, silakan hubungi melalui WhatsApp.</p>
            
            <a href="https://wa.me/6285651222693" target="_blank" rel="noopener noreferrer" class="inline-flex items-center gap-2 px-6 py-3 bg-green-500 text-white rounded-xl font-semibold hover:bg-green-600 transition-all shadow-lg">
              <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/></svg>
              Chat via WhatsApp
            </a>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Dashboard Modal -->
    <div id="dashboard-modal" class="no-print fixed inset-0 z-50 hidden">
      <div class="modal-overlay absolute inset-0" onclick="hideDashboard()"></div>
      <div class="absolute inset-0 flex items-center justify-center p-4 overflow-y-auto">
        <div class="bg-white rounded-2xl shadow-2xl w-full max-w-4xl p-8 relative fade-in my-8">
          <button onclick="hideDashboard()" class="absolute top-4 right-4 w-8 h-8 flex items-center justify-center rounded-full hover:bg-slate-100 transition-colors">
            <svg class="w-5 h-5 text-slate-500" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"/></svg>
          </button>
          
          <h2 class="text-2xl font-bold text-slate-800 mb-6">Dashboard Admin</h2>
          
          <div class="grid grid-cols-2 md:grid-cols-4 gap-4 mb-8">
            <div class="bg-gradient-to-br from-blue-500 to-blue-600 rounded-xl p-4 text-white">
              <div class="text-3xl font-bold" id="stat-materi">0</div>
              <div class="text-sm opacity-90">Materi</div>
            </div>
            <div class="bg-gradient-to-br from-emerald-500 to-emerald-600 rounded-xl p-4 text-white">
              <div class="text-3xl font-bold" id="stat-soal">0</div>
              <div class="text-sm opacity-90">Bank Soal</div>
            </div>
            <div class="bg-gradient-to-br from-purple-500 to-purple-600 rounded-xl p-4 text-white">
              <div class="text-3xl font-bold" id="stat-asesmen">0</div>
              <div class="text-sm opacity-90">Asesmen</div>
            </div>
            <div class="bg-gradient-to-br from-orange-500 to-orange-600 rounded-xl p-4 text-white">
              <div class="text-3xl font-bold" id="stat-siswa">0</div>
              <div class="text-sm opacity-90">Data Nilai</div>
            </div>
          </div>
          
          <!-- Quick Actions -->
          <div>
            <h3 class="text-lg font-bold text-slate-800 mb-4">Aksi Cepat</h3>
            <div class="grid grid-cols-2 md:grid-cols-4 gap-3">
              <button onclick="hideDashboard(); navigateTo('home'); setTimeout(() => showAddModal('announcement'), 300)" class="p-4 bg-slate-100 rounded-xl hover:bg-slate-200 transition-all text-center">
                <div class="text-2xl mb-1">📢</div>
                <div class="text-sm font-medium text-slate-700">Pengumuman</div>
              </button>
              <button onclick="hideDashboard(); navigateTo('materi'); setTimeout(() => showAddModal('materi'), 300)" class="p-4 bg-slate-100 rounded-xl hover:bg-slate-200 transition-all text-center">
                <div class="text-2xl mb-1">📚</div>
                <div class="text-sm font-medium text-slate-700">Materi</div>
              </button>
              <button onclick="hideDashboard(); navigateTo('nilai'); setTimeout(() => showAddModal('nilai'), 300)" class="p-4 bg-slate-100 rounded-xl hover:bg-slate-200 transition-all text-center">
                <div class="text-2xl mb-1">📊</div>
                <div class="text-sm font-medium text-slate-700">Nilai</div>
              </button>
              <button onclick="hideDashboard(); navigateTo('kehadiran'); setTimeout(() => showAddModal('kehadiran'), 300)" class="p-4 bg-slate-100 rounded-xl hover:bg-slate-200 transition-all text-center">
                <div class="text-2xl mb-1">✅</div>
                <div class="text-sm font-medium text-slate-700">Kehadiran</div>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <!-- Toast Notification -->
    <div id="toast" class="fixed bottom-24 left-1/2 -translate-x-1/2 z-50 hidden">
      <div class="bg-slate-800 text-white px-6 py-3 rounded-xl shadow-xl flex items-center gap-3">
        <span id="toast-message">Berhasil!</span>
      </div>
    </div>
  </div>

  <script>
    // Application State
    let isLoggedIn = false;
    let currentPage = 'home';
    let allData = [];
    let currentEditId = null;
    let currentDeleteId = null;
    let currentModalType = null;
    
    // Default Config
    const defaultConfig = {
      site_title: 'Sistem Pembelajaran',
      school_name: 'Portal Manajemen Guru',
      teacher_name: 'Guru',
      guru_deskripsi: 'Guru berpengalaman dengan dedikasi tinggi dalam mengajar',
      sistem_deskripsi: 'Platform pembelajaran terintegrasi untuk mengelola materi, soal, asesmen, dan nilai siswa secara terpusat',
      visi: 'Menciptakan generasi pelajar yang kompeten dan berkarakter',
      misi: 'Memberikan pendidikan berkualitas dengan metode pembelajaran interaktif',
      tujuan_pembelajaran: 'Mengembangkan kompetensi siswa sesuai standar kurikulum nasional',
      kontak: '085651222693'
    };
    
    let config = { ...defaultConfig };
    
    // Data Types Configuration
    const dataTypes = {
      announcement: {
        label: 'Pengumuman',
        fields: [
          { name: 'title', label: 'Judul', type: 'text', required: true },
          { name: 'content', label: 'Isi Pengumuman', type: 'textarea', required: true },
          { name: 'is_active', label: 'Status Aktif', type: 'checkbox' }
        ]
      },
      materi: {
        label: 'Materi',
        fields: [
          { name: 'title', label: 'Judul Materi', type: 'text', required: true },
          { name: 'subject', label: 'Mata Pelajaran', type: 'select', options: ['Fisika', 'Bahasa Inggris'], required: true },
          { name: 'class_name', label: 'Kelas', type: 'select', options: ['X', 'XI', 'XII'], required: true },
          { name: 'content', label: 'Deskripsi', type: 'textarea', required: true },
          { name: 'file_url', label: 'Link File/Video', type: 'url' }
        ]
      },
      'bank-soal': {
        label: 'Bank Soal',
        fields: [
          { name: 'title', label: 'Judul Paket Soal', type: 'text', required: true },
          { name: 'subject', label: 'Mata Pelajaran', type: 'select', options: ['Fisika', 'Bahasa Inggris'], required: true },
          { name: 'class_name', label: 'Kelas', type: 'select', options: ['X', 'XI', 'XII'], required: true },
          { name: 'category', label: 'Kategori Soal', type: 'text', placeholder: 'PG / Essay / Campuran' },
          { name: 'content', label: 'Deskripsi Paket', type: 'textarea' },
          { name: 'file_url', label: 'Link Paket Soal', type: 'url', required: true }
        ]
      },
      asesmen: {
        label: 'Asesmen',
        fields: [
          { name: 'assessment_type', label: 'Jenis Asesmen', type: 'select', options: ['Diagnostik', 'Formatif', 'Sumatif', 'Proyek', 'UH', 'PTS', 'PAS'], required: true },
          { name: 'subject', label: 'Mata Pelajaran', type: 'select', options: ['Fisika', 'Bahasa Inggris'], required: true },
          { name: 'class_name', label: 'Kelas', type: 'select', options: ['X', 'XI', 'XII'], required: true },
          { name: 'title', label: 'Judul Asesmen', type: 'text', required: true },
          { name: 'content', label: 'Deskripsi', type: 'textarea' },
          { name: 'date', label: 'Tanggal Pelaksanaan', type: 'date' },
          { name: 'file_url', label: 'Link Asesmen', type: 'url' }
        ]
      },
      nilai: {
        label: 'Data Nilai',
        fields: [
          { name: 'student_name', label: 'Nama Siswa', type: 'text', required: true },
          { name: 'class_name', label: 'Kelas', type: 'select', options: ['X', 'XI', 'XII'], required: true },
          { name: 'subject', label: 'Mata Pelajaran', type: 'select', options: ['Fisika', 'Bahasa Inggris'], required: true },
          { name: 'tp', label: 'Tujuan Pembelajaran (TP)', type: 'select', options: ['TP1', 'TP2', 'TP3', 'TP4', 'TP5', 'TP6', 'TP7'], required: true },
          { name: 'nilai_tugas', label: 'Nilai Tugas', type: 'number', required: true },
          { name: 'nilai_psas', label: 'Nilai PSAS', type: 'number', required: true },
          { name: 'date', label: 'Tanggal', type: 'date', required: true }
        ]
      },
      kehadiran: {
        label: 'Kehadiran',
        fields: [
          { name: 'student_name', label: 'Nama Siswa', type: 'text', required: true },
          { name: 'class_name', label: 'Kelas', type: 'text', required: true },
          { name: 'date', label: 'Tanggal', type: 'date', required: true },
          { name: 'attendance_status', label: 'Status (Hadir/Izin/Sakit/Alpha)', type: 'select', options: ['Hadir', 'Izin', 'Sakit', 'Alpha'], required: true }
        ]
      },
      publikasi: {
        label: 'Publikasi',
        fields: [
          { name: 'title', label: 'Judul', type: 'text', required: true },
          { name: 'category', label: 'Kategori', type: 'text', required: true },
          { name: 'content', label: 'Isi', type: 'textarea', required: true },
          { name: 'file_url', label: 'Link/URL', type: 'url' }
        ]
      },
      download: {
        label: 'File Download',
        fields: [
          { name: 'title', label: 'Nama File', type: 'text', required: true },
          { name: 'category', label: 'Kategori', type: 'text', required: true },
          { name: 'content', label: 'Deskripsi', type: 'textarea' },
          { name: 'file_url', label: 'Link Download', type: 'url', required: true }
        ]
      },
      akademik: {
        label: 'Info Akademik',
        fields: [
          { name: 'title', label: 'Judul', type: 'text', required: true },
          { name: 'category', label: 'Kategori (Kalender/Jadwal/dll)', type: 'text', required: true },
          { name: 'content', label: 'Isi', type: 'textarea', required: true },
          { name: 'date', label: 'Tanggal', type: 'date' }
        ]
      },
      social: {
        label: 'Media Sosial',
        fields: [
          { name: 'title', label: 'Platform', type: 'text', required: true },
          { name: 'link_url', label: 'URL', type: 'url', required: true }
        ]
      }
    };
    
    // Initialize Data SDK
    const dataHandler = {
      onDataChanged(data) {
        allData = data;
        updateUI();
      }
    };
    
    // Element SDK Initialization
    async function initApp() {
      // Initialize Element SDK
      if (window.elementSdk) {
        await window.elementSdk.init({
          defaultConfig,
          onConfigChange: async (newConfig) => {
            config = { ...defaultConfig, ...newConfig };
            applyConfig();
          },
          mapToCapabilities: (cfg) => ({
            recolorables: [],
            borderables: [],
            fontEditable: undefined,
            fontSizeable: undefined
          }),
          mapToEditPanelValues: (cfg) => new Map([
            ['site_title', cfg.site_title || defaultConfig.site_title],
            ['school_name', cfg.school_name || defaultConfig.school_name],
            ['teacher_name', cfg.teacher_name || defaultConfig.teacher_name],
            ['guru_deskripsi', cfg.guru_deskripsi || defaultConfig.guru_deskripsi],
            ['sistem_deskripsi', cfg.sistem_deskripsi || defaultConfig.sistem_deskripsi],
            ['visi', cfg.visi || defaultConfig.visi],
            ['misi', cfg.misi || defaultConfig.misi],
            ['tujuan_pembelajaran', cfg.tujuan_pembelajaran || defaultConfig.tujuan_pembelajaran],
            ['kontak', cfg.kontak || defaultConfig.kontak]
          ])
        });
      }
      
      // Initialize Data SDK
      if (window.dataSdk) {
        const result = await window.dataSdk.init(dataHandler);
        if (!result.isOk) {
          console.error('Failed to initialize data SDK');
        }
      }
      
      // Initial render
      navigateTo('home');
    }
    
    function applyConfig() {
      const siteTitle = document.getElementById('site-title');
      const schoolName = document.getElementById('school-name');
      const userGreeting = document.getElementById('user-greeting');
      
      if (siteTitle) siteTitle.textContent = config.site_title || defaultConfig.site_title;
      if (schoolName) schoolName.textContent = config.school_name || defaultConfig.school_name;
      if (userGreeting) userGreeting.textContent = `Halo, ${config.teacher_name || defaultConfig.teacher_name}!`;
    }
    
    // Update UI based on data
    function updateUI() {
      updateAnnouncements();
      updateSocialLinks();
      updateStats();
      renderCurrentPage();
    }
    
    function updateAnnouncements() {
      const announcements = allData.filter(d => d.type === 'announcement' && d.is_active);
      const marqueeContent = document.getElementById('marquee-content');
      
      if (announcements.length > 0) {
        const text = announcements.map(a => `📢 ${a.title}: ${a.content}`).join(' | ');
        marqueeContent.textContent = text;
      } else {
        marqueeContent.textContent = '📢 Selamat datang di Sistem Manajemen Pembelajaran Guru | Silakan cek pengumuman terbaru!';
      }
    }
    
    function updateSocialLinks() {
      const socials = allData.filter(d => d.type === 'social');
      
      socials.forEach(s => {
        const platform = s.title?.toLowerCase();
        let linkEl = null;
        
        if (platform?.includes('instagram')) linkEl = document.getElementById('instagram-link');
        else if (platform?.includes('youtube')) linkEl = document.getElementById('youtube-link');
        else if (platform?.includes('tiktok')) linkEl = document.getElementById('tiktok-link');
        else if (platform?.includes('facebook')) linkEl = document.getElementById('facebook-link');
        
        if (linkEl && s.link_url) {
          linkEl.href = s.link_url;
        }
      });
    }
    
    function updateStats() {
      const statMateri = document.getElementById('stat-materi');
      const statSoal = document.getElementById('stat-soal');
      const statAsesmen = document.getElementById('stat-asesmen');
      const statSiswa = document.getElementById('stat-siswa');
      
      if (statMateri) statMateri.textContent = allData.filter(d => d.type === 'materi').length;
      if (statSoal) statSoal.textContent = allData.filter(d => d.type === 'bank-soal').length;
      if (statAsesmen) statAsesmen.textContent = allData.filter(d => d.type === 'asesmen').length;
      if (statSiswa) statSiswa.textContent = allData.filter(d => d.type === 'nilai').length;
    }
    
    // Navigation
    function navigateTo(page) {
      currentPage = page;
      
      // Update nav active state
      document.querySelectorAll('.nav-item').forEach(item => {
        item.classList.remove('active', 'text-blue-600');
        item.classList.add('text-slate-600');
        if (item.dataset.page === page) {
          item.classList.add('active', 'text-blue-600');
          item.classList.remove('text-slate-600');
        }
      });
      
      renderCurrentPage();
    }
    
    function renderCurrentPage() {
      const mainContent = document.getElementById('main-content');
      
      switch(currentPage) {
        case 'home':
          renderHomePage(mainContent);
          break;
        case 'materi':
          renderMateriPage(mainContent);
          break;
        case 'bank-soal':
          renderBankSoalPage(mainContent);
          break;
        case 'asesmen':
          renderAsesmenPage(mainContent);
          break;
        case 'nilai':
          renderNilaiPage(mainContent);
          break;
        case 'kehadiran':
          renderTablePage(mainContent, 'kehadiran', 'Data Kehadiran', '✅');
          break;
        case 'publikasi':
          renderDataPage(mainContent, 'publikasi', 'Publikasi', '📰');
          break;
        case 'download':
          renderDataPage(mainContent, 'download', 'File Download', '📥');
          break;
        case 'akademik':
          renderDataPage(mainContent, 'akademik', 'Info Akademik', '🎓');
          break;
        default:
          renderHomePage(mainContent);
      }
    }
    
    function renderHomePage(container) {
      const announcements = allData.filter(d => d.type === 'announcement');
      const latestMateri = allData.filter(d => d.type === 'materi').slice(0, 4);
      const latestAsesmen = allData.filter(d => d.type === 'asesmen').slice(0, 3);
      
      container.innerHTML = `
        <div class="fade-in space-y-8">
          <!-- Hero Section -->
          <div class="gradient-bg rounded-3xl p-8 md:p-12 text-white mb-8 relative overflow-hidden">
            <div class="absolute inset-0 opacity-10">
              <svg class="w-full h-full" viewBox="0 0 100 100" preserveAspectRatio="none">
                <circle cx="80" cy="20" r="30" fill="white"/>
                <circle cx="10" cy="80" r="20" fill="white"/>
              </svg>
            </div>
            <div class="relative z-10">
              <h1 class="text-3xl md:text-4xl font-bold mb-4">Selamat Datang di Portal Pembelajaran</h1>
              <p class="text-lg opacity-90 max-w-2xl">Akses materi, soal, asesmen, dan informasi akademik dengan mudah. Platform terintegrasi untuk mendukung proses belajar mengajar.</p>
              
              <!-- Social Media Links in Hero -->
              <div class="flex items-center gap-3 mt-6">
                <span class="text-sm opacity-75">Ikuti kami:</span>
                <a id="hero-ig" href="#" target="_blank" rel="noopener noreferrer" class="w-10 h-10 bg-white/20 rounded-full flex items-center justify-center hover:bg-white/30 transition-all">
                  <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/></svg>
                </a>
                <a id="hero-yt" href="#" target="_blank" rel="noopener noreferrer" class="w-10 h-10 bg-white/20 rounded-full flex items-center justify-center hover:bg-white/30 transition-all">
                  <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M23.498 6.186a3.016 3.016 0 0 0-2.122-2.136C19.505 3.545 12 3.545 12 3.545s-7.505 0-9.377.505A3.017 3.017 0 0 0 .502 6.186C0 8.07 0 12 0 12s0 3.93.502 5.814a3.016 3.016 0 0 0 2.122 2.136c1.871.505 9.376.505 9.376.505s7.505 0 9.377-.505a3.015 3.015 0 0 0 2.122-2.136C24 15.93 24 12 24 12s0-3.93-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z"/></svg>
                </a>
                <a id="hero-tt" href="#" target="_blank" rel="noopener noreferrer" class="w-10 h-10 bg-white/20 rounded-full flex items-center justify-center hover:bg-white/30 transition-all">
                  <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M12.525.02c1.31-.02 2.61-.01 3.91-.02.08 1.53.63 3.09 1.75 4.17 1.12 1.11 2.7 1.62 4.24 1.79v4.03c-1.44-.05-2.89-.35-4.2-.97-.57-.26-1.1-.59-1.62-.93-.01 2.92.01 5.84-.02 8.75-.08 1.4-.54 2.79-1.35 3.94-1.31 1.92-3.58 3.17-5.91 3.21-1.43.08-2.86-.31-4.08-1.03-2.02-1.19-3.44-3.37-3.65-5.71-.02-.5-.03-1-.01-1.49.18-1.9 1.12-3.72 2.58-4.96 1.66-1.44 3.98-2.13 6.15-1.72.02 1.48-.04 2.96-.04 4.44-.99-.32-2.15-.23-3.02.37-.63.41-1.11 1.04-1.36 1.75-.21.51-.15 1.07-.14 1.61.24 1.64 1.82 3.02 3.5 2.87 1.12-.01 2.19-.66 2.77-1.61.19-.33.4-.67.41-1.06.1-1.79.06-3.57.07-5.36.01-4.03-.01-8.05.02-12.07z"/></svg>
                </a>
                <a id="hero-fb" href="#" target="_blank" rel="noopener noreferrer" class="w-10 h-10 bg-white/20 rounded-full flex items-center justify-center hover:bg-white/30 transition-all">
                  <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"/></svg>
                </a>
              </div>
            </div>
          </div>

          <!-- Profile Section -->
          <div class="grid grid-cols-1 lg:grid-cols-3 gap-6 mb-8">
            <!-- Teacher Profile -->
            <div class="lg:col-span-2">
              <div class="bg-white rounded-2xl p-6 shadow-lg border border-slate-100">
                <div class="flex items-start gap-4">
                  <div class="w-20 h-20 bg-gradient-to-br from-purple-400 to-pink-400 rounded-2xl flex items-center justify-center text-3xl flex-shrink-0">
                    👨‍🏫
                  </div>
                  <div class="flex-1">
                    <h2 class="text-2xl font-bold text-slate-800 mb-1">${escapeHtml(config.teacher_name || defaultConfig.teacher_name)}</h2>
                    <p class="text-slate-600 mb-3">${escapeHtml(config.guru_deskripsi || defaultConfig.guru_deskripsi)}</p>
                    <div class="flex items-center gap-2 text-sm">
                      <svg class="w-4 h-4 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 00.948-.684l1.498-4.493a1 1 0 011.502 0l1.498 4.493a1 1 0 00.948.684H17a2 2 0 012 2v2H3V5z"/></svg>
                      <span class="text-slate-600">${escapeHtml(config.kontak || defaultConfig.kontak)}</span>
                    </div>
                  </div>
                </div>
                ${isLoggedIn ? `
                  <div class="mt-4 pt-4 border-t border-slate-200">
                    <button onclick="showAddModal('announcement')" class="px-4 py-2 bg-blue-600 text-white rounded-lg text-sm font-semibold hover:bg-blue-700 transition-all">
                      Kelola Pengumuman
                    </button>
                  </div>
                ` : ''}
              </div>
            </div>

            <!-- System Info -->
            <div class="bg-white rounded-2xl p-6 shadow-lg border border-slate-100">
              <div class="space-y-4">
                <div>
                  <h3 class="text-sm font-bold text-slate-600 uppercase tracking-wider mb-2">Tentang Sistem</h3>
                  <p class="text-sm text-slate-600 leading-relaxed">${escapeHtml(config.sistem_deskripsi || defaultConfig.sistem_deskripsi)}</p>
                </div>
                <div class="pt-4 border-t border-slate-200">
                  <div class="flex items-center justify-between mb-2">
                    <span class="text-xs font-medium text-slate-500 uppercase">Status</span>
                    <span class="px-2 py-1 bg-green-100 text-green-700 rounded-full text-xs font-semibold">Aktif</span>
                  </div>
                </div>
              </div>
            </div>
          </div>

          <!-- Learning Objectives -->
          <div class="grid grid-cols-1 md:grid-cols-3 gap-6 mb-8">
            <!-- Visi -->
            <div class="bg-gradient-to-br from-blue-50 to-blue-100 rounded-2xl p-6 border border-blue-200 shadow-lg">
              <div class="text-4xl mb-3">🎯</div>
              <h3 class="text-lg font-bold text-slate-800 mb-2">Visi</h3>
              <p class="text-sm text-slate-600 leading-relaxed">${escapeHtml(config.visi || defaultConfig.visi)}</p>
            </div>

            <!-- Misi -->
            <div class="bg-gradient-to-br from-emerald-50 to-emerald-100 rounded-2xl p-6 border border-emerald-200 shadow-lg">
              <div class="text-4xl mb-3">📋</div>
              <h3 class="text-lg font-bold text-slate-800 mb-2">Misi</h3>
              <p class="text-sm text-slate-600 leading-relaxed">${escapeHtml(config.misi || defaultConfig.misi)}</p>
            </div>

            <!-- Tujuan Pembelajaran -->
            <div class="bg-gradient-to-br from-purple-50 to-purple-100 rounded-2xl p-6 border border-purple-200 shadow-lg">
              <div class="text-4xl mb-3">🏆</div>
              <h3 class="text-lg font-bold text-slate-800 mb-2">Tujuan</h3>
              <p class="text-sm text-slate-600 leading-relaxed">${escapeHtml(config.tujuan_pembelajaran || defaultConfig.tujuan_pembelajaran)}</p>
            </div>
          </div>
          
          <!-- Announcements Section -->
          <div>
            <div class="flex items-center justify-between mb-4">
              <h2 class="text-xl font-bold text-slate-800 flex items-center gap-2">
                <span class="text-2xl">📢</span> Pengumuman Terbaru
              </h2>
              ${isLoggedIn ? `
                <button onclick="showAddModal('announcement')" class="px-4 py-2 bg-blue-600 text-white rounded-xl text-sm font-semibold hover:bg-blue-700 transition-all flex items-center gap-2">
                  <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/></svg>
                  Tambah
                </button>
              ` : ''}
            </div>
            
            ${announcements.length > 0 ? `
              <div class="grid gap-4">
                ${announcements.slice(0, 3).map(a => `
                  <div class="bg-white rounded-xl p-5 shadow-md border border-slate-100 card-hover">
                    <div class="flex items-start justify-between">
                      <div class="flex-1">
                        <div class="flex items-center gap-2 mb-2">
                          <h3 class="font-bold text-slate-800">${escapeHtml(a.title)}</h3>
                          ${a.is_active ? '<span class="px-2 py-0.5 bg-green-100 text-green-700 rounded-full text-xs font-medium">Aktif</span>' : '<span class="px-2 py-0.5 bg-slate-100 text-slate-500 rounded-full text-xs font-medium">Nonaktif</span>'}
                        </div>
                        <p class="text-slate-600 text-sm">${escapeHtml(a.content)}</p>
                      </div>
                      ${isLoggedIn ? `
                        <div class="flex gap-2 ml-4">
                          <button onclick="editItem('${a.__backendId}')" class="w-8 h-8 bg-blue-100 text-blue-600 rounded-lg flex items-center justify-center hover:bg-blue-200 transition-all">
                            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"/></svg>
                          </button>
                          <button onclick="deleteItem('${a.__backendId}')" class="w-8 h-8 bg-red-100 text-red-600 rounded-lg flex items-center justify-center hover:bg-red-200 transition-all">
                            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/></svg>
                          </button>
                        </div>
                      ` : ''}
                    </div>
                  </div>
                `).join('')}
              </div>
            ` : `
              <div class="bg-white rounded-xl p-8 text-center border border-slate-100">
                <div class="text-4xl mb-2">📭</div>
                <p class="text-slate-500">Belum ada pengumuman</p>
              </div>
            `}
          </div>
          
          <!-- Latest Materials -->
          <div>
            <div class="flex items-center justify-between mb-4">
              <h2 class="text-xl font-bold text-slate-800 flex items-center gap-2">
                <span class="text-2xl">📚</span> Materi Terbaru
              </h2>
              <button onclick="navigateTo('materi')" class="text-blue-600 text-sm font-medium hover:underline">Lihat Semua →</button>
            </div>
            
            ${latestMateri.length > 0 ? `
              <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
                ${latestMateri.map(m => `
                  <div class="bg-white rounded-xl p-5 shadow-md border border-slate-100 card-hover">
                    <div class="w-10 h-10 bg-blue-100 rounded-lg flex items-center justify-center mb-3">
                      <svg class="w-5 h-5 text-blue-600" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 6.253v13m0-13C10.832 5.477 9.246 5 7.5 5S4.168 5.477 3 6.253v13C4.168 18.477 5.754 18 7.5 18s3.332.477 4.5 1.253m0-13C13.168 5.477 14.754 5 16.5 5c1.747 0 3.332.477 4.5 1.253v13C19.832 18.477 18.247 18 16.5 18c-1.746 0-3.332.477-4.5 1.253"/></svg>
                    </div>
                    <h3 class="font-bold text-slate-800 mb-1 line-clamp-1">${escapeHtml(m.title)}</h3>
                    <p class="text-xs text-slate-500 mb-2">${escapeHtml(m.subject)} • ${escapeHtml(m.class_name)}</p>
                    <p class="text-sm text-slate-600 line-clamp-2">${escapeHtml(m.content)}</p>
                  </div>
                `).join('')}
              </div>
            ` : `
              <div class="bg-white rounded-xl p-8 text-center border border-slate-100">
                <div class="text-4xl mb-2">📚</div>
                <p class="text-slate-500">Belum ada materi</p>
              </div>
            `}
          </div>
          
          <!-- Latest Assessments -->
          <div>
            <div class="flex items-center justify-between mb-4">
              <h2 class="text-xl font-bold text-slate-800 flex items-center gap-2">
                <span class="text-2xl">📋</span> Asesmen Mendatang
              </h2>
              <button onclick="navigateTo('asesmen')" class="text-blue-600 text-sm font-medium hover:underline">Lihat Semua →</button>
            </div>
            
            ${latestAsesmen.length > 0 ? `
              <div class="grid gap-4">
                ${latestAsesmen.map(a => `
                  <div class="bg-white rounded-xl p-5 shadow-md border border-slate-100 card-hover flex items-center gap-4">
                    <div class="w-14 h-14 bg-purple-100 rounded-xl flex flex-col items-center justify-center text-purple-600">
                      <span class="text-lg font-bold">${a.date ? new Date(a.date).getDate() : '-'}</span>
                      <span class="text-xs">${a.date ? new Date(a.date).toLocaleDateString('id-ID', { month: 'short' }) : ''}</span>
                    </div>
                    <div class="flex-1">
                      <h3 class="font-bold text-slate-800">${escapeHtml(a.title)}</h3>
                      <p class="text-sm text-slate-500">${escapeHtml(a.subject)} • ${escapeHtml(a.class_name)} • ${escapeHtml(a.assessment_type || '')}</p>
                    </div>
                    ${a.file_url ? `
                      <a href="${escapeHtml(a.file_url)}" target="_blank" rel="noopener noreferrer" class="px-4 py-2 bg-purple-600 text-white rounded-lg text-sm font-medium hover:bg-purple-700 transition-all">
                        Buka
                      </a>
                    ` : ''}
                  </div>
                `).join('')}
              </div>
            ` : `
              <div class="bg-white rounded-xl p-8 text-center border border-slate-100">
                <div class="text-4xl mb-2">📋</div>
                <p class="text-slate-500">Belum ada asesmen</p>
              </div>
            `}
          </div>
        </div>
      `;
      
      // Update hero social links
      const socials = allData.filter(d => d.type === 'social');
      socials.forEach(s => {
        const platform = s.title?.toLowerCase();
        let linkEl = null;
        
        if (platform?.includes('instagram')) linkEl = document.getElementById('hero-ig');
        else if (platform?.includes('youtube')) linkEl = document.getElementById('hero-yt');
        else if (platform?.includes('tiktok')) linkEl = document.getElementById('hero-tt');
        else if (platform?.includes('facebook')) linkEl = document.getElementById('hero-fb');
        
        if (linkEl && s.link_url) {
          linkEl.href = s.link_url;
        }
      });
    }
    
    function renderMateriPage(container) {
      const items = allData.filter(d => d.type === 'materi');
      const colors = ['from-blue-400 to-blue-600', 'from-emerald-400 to-emerald-600', 'from-purple-400 to-purple-600', 'from-orange-400 to-orange-600', 'from-pink-400 to-pink-600', 'from-cyan-400 to-cyan-600'];
      
      container.innerHTML = `
        <div class="fade-in">
          <div class="flex items-center justify-between mb-6">
            <h1 class="text-2xl font-bold text-slate-800 flex items-center gap-3">
              <span class="text-3xl">📚</span> Materi Pembelajaran
            </h1>
            ${isLoggedIn ? `
              <button onclick="showAddModal('materi')" class="px-5 py-2.5 bg-blue-600 text-white rounded-xl font-semibold hover:bg-blue-700 transition-all flex items-center gap-2 shadow-lg">
                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"/></svg>
                Tambah Materi
              </button>
            ` : ''}
          </div>
          
          ${items.length > 0 ? `
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
              ${items.map((item, idx) => `
                <div class="bg-white rounded-2xl shadow-lg border border-slate-100 card-hover overflow-hidden">
                  <!-- Card Header with Gradient -->
                  <div class="h-32 bg-gradient-to-br ${colors[idx % colors.length]} relative overflow-hidden">
                    <div class="absolute inset-0 flex items-center justify-center text-6xl opacity-20">📄</div>
                    <div class="absolute top-3 right-3 flex gap-1">
                      ${isLoggedIn ? `
                        <button onclick="editItem('${item.__backendId}')" class="w-8 h-8 bg-white/90 text-blue-600 rounded-lg flex items-center justify-center hover:bg-white transition-all shadow-md">
                          <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"/></svg>
                        </button>
                        <button onclick="deleteItem('${item.__backendId}')" class="w-8 h-8 bg-white/90 text-red-600 rounded-lg flex items-center justify-center hover:bg-white transition-all shadow-md">
                          <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/></svg>
                        </button>
                      ` : ''}
                    </div>
                  </div>
                  
                  <!-- Card Content -->
                  <div class="p-5">
                    <div class="flex items-center gap-2 mb-2">
                      <span class="px-3 py-1 bg-blue-100 text-blue-700 rounded-full text-xs font-semibold">${escapeHtml(item.subject)}</span>
                      <span class="px-3 py-1 bg-slate-100 text-slate-600 rounded-full text-xs font-semibold">Kelas ${escapeHtml(item.class_name)}</span>
                    </div>
                    <h3 class="font-bold text-slate-800 mb-2 text-lg">${escapeHtml(item.title)}</h3>
                    <p class="text-sm text-slate-600 line-clamp-3 mb-4">${escapeHtml(item.content)}</p>
                    
                    ${item.file_url ? `
                      <a href="${escapeHtml(item.file_url)}" target="_blank" rel="noopener noreferrer" class="inline-flex items-center gap-2 px-4 py-2.5 bg-blue-600 text-white rounded-lg text-sm font-semibold hover:bg-blue-700 transition-all w-full justify-center">
                        <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"/></svg>
                        Buka Materi
                      </a>
                    ` : ''}
                  </div>
                </div>
              `).join('')}
            </div>
          ` : `
            <div class="bg-white rounded-xl p-12 text-center border border-slate-100">
              <div class="text-5xl mb-4">📚</div>
              <h3 class="text-lg font-semibold text-slate-700 mb-2">Belum Ada Materi</h3>
              <p class="text-slate-500 text-sm">Materi akan muncul di sini setelah ditambahkan.</p>
            </div>
          `}
        </div>
      `;
    }
    
    function renderBankSoalPage(container) {
      const items = allData.filter(d => d.type === 'bank-soal');
      const colors = ['from-purple-400 to-purple-600', 'from-blue-400 to-blue-600', 'from-emerald-400 to-emerald-600', 'from-orange-400 to-orange-600', 'from-pink-400 to-pink-600', 'from-red-400 to-red-600'];
      
      container.innerHTML = `
        <div class="fade-in">
          <div class="flex items-center justify-between mb-6">
            <h1 class="text-2xl font-bold text
