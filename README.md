<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>理想狀態 - Archive Portal</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:ital,wght@0,300;0,400;0,600;0,800;1,400&family=Noto+Sans+TC:wght@300;400;500;700;900&display=swap');

    body {
      font-family: 'JetBrains Mono', 'Noto Sans TC', monospace;
      background-color: #08090a;
      color: #d1d5db;
    }

    .bg-grid-dark {
      background-size: 32px 32px;
      background-image: 
        linear-gradient(to right, rgba(255, 255, 255, 0.03) 1px, transparent 1px),
        linear-gradient(to bottom, rgba(255, 255, 255, 0.03) 1px, transparent 1px);
    }

    .glass-card {
      background: rgba(15, 18, 22, 0.85);
      backdrop-filter: blur(16px);
      border: 1px solid rgba(255, 255, 255, 0.08);
      transition: all 0.35s cubic-bezier(0.16, 1, 0.3, 1);
    }

    .glass-card:hover {
      border-color: rgba(16, 185, 129, 0.4);
      transform: translateY(-4px);
      box-shadow: 0 16px 36px -10px rgba(0, 0, 0, 0.9), 0 0 24px 0 rgba(16, 185, 129, 0.08);
    }

    /* 獨自保留卡片按鈕為極光螢光綠 */
    .btn-neon {
      background-color: #39FF14;
      color: #000000;
      font-weight: 800;
      border: none;
      transition: all 0.2s ease;
    }

    .btn-neon:hover {
      background-color: #55FF33;
      box-shadow: 0 0 20px rgba(57, 255, 20, 0.6);
    }

    .stamp-red {
      border: 2px solid #ef4444;
      color: #ef4444;
      transform: rotate(-6deg);
      letter-spacing: 0.15em;
      text-shadow: 0 0 10px rgba(239, 68, 68, 0.3);
      box-shadow: inset 0 0 12px rgba(239, 68, 68, 0.12), 0 0 8px rgba(239, 68, 68, 0.2);
    }

    /* 呼吸計數器跳動動畫（翡翠綠） */
    @keyframes pulse-emerald {
      0%, 100% { color: #10b981; opacity: 1; }
      50% { color: #6ee7b7; opacity: 0.7; }
    }
    .breath-counter-active {
      animation: pulse-emerald 2s infinite;
    }
  </style>
</head>
<body class="bg-grid-dark min-h-screen text-gray-300 relative selection:bg-emerald-500 selection:text-black">

  <!-- 頂部氛圍光學光暈 -->
  <div class="fixed top-0 left-1/2 -translate-x-1/2 w-full max-w-6xl h-80 bg-emerald-950/20 blur-[130px] pointer-events-none rounded-full"></div>

  <div class="max-w-5xl mx-auto px-4 py-8 md:py-14 relative z-10">

    <header class="flex flex-col md:flex-row justify-between items-start md:items-center border-b border-gray-800 pb-6 mb-10 gap-4">
      <div>
        <div class="flex items-center space-x-2 text-xs tracking-widest text-emerald-400 font-mono mb-1">
          <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
          <span>SYSTEM RUNNING | CLINICAL ARCHIVE PORTAL</span>
        </div>
        <h1 class="text-2xl md:text-3xl font-extrabold tracking-tight text-white font-mono">
          理想狀態
        </h1>
        <p class="text-xs text-gray-500 tracking-wider mt-0.5">當代個人怠工檔案與系統診斷報告 Archive Portal</p>
      </div>

      <div class="text-right font-mono text-xs text-gray-400 bg-gray-950/80 px-4 py-2.5 rounded border border-gray-800/80 w-full md:w-auto flex justify-between md:block">
        <span class="text-gray-500 mr-2">VALUABLE OUTPUT:</span>
        <span class="text-emerald-400 font-bold">0.000 KG/H</span>
      </div>
    </header>

    <!-- 1. 門戶首頁 -->
    <main id="portal-view" class="space-y-8">
      <div class="flex justify-between items-end border-b border-gray-800/60 pb-3">
        <div>
          <h2 class="text-lg font-bold text-white tracking-wide">代理人檔案目錄</h2>
          <p class="text-xs text-gray-500">點擊個案卡片，檢視完整「臨床診斷報告與生命累積呼吸數據」</p>
        </div>
        <span class="text-xs text-gray-600 font-mono">TOTAL: 04 CASES</span>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6" id="cards-container">
      </div>
    </main>

    <!-- 2. 診斷檔案詳情頁 -->
    <main id="detail-view" class="hidden space-y-6">
      
      <button onclick="showPortal()" class="inline-flex items-center space-x-2 text-xs text-gray-300 hover:text-white transition-colors bg-gray-900/90 hover:bg-gray-800 px-4 py-2 rounded border border-gray-700">
        <span>←</span>
        <span>返回檔案目錄 (RETURN TO DIRECTORY)</span>
      </button>

      <article class="glass-card rounded-xl p-6 md:p-10 relative space-y-8">
        
        <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center border-b border-gray-800 pb-6 gap-4">
          <div>
            <span id="detail-id" class="inline-block text-white text-xs font-mono mb-2">CASE #000</span>
            <h2 id="detail-name" class="text-2xl md:text-3xl font-bold text-white">---</h2>
            <p id="detail-role" class="text-xs font-mono text-gray-400 mt-1">---</p>
          </div>

          <div class="stamp-red px-4 py-1.5 rounded text-xs font-bold font-mono tracking-widest uppercase">
            AUTHORIZED IDLE
          </div>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-3 gap-8 items-center">
          <!-- 照片區域 (3:4 比例) -->
          <div id="detail-image-container" class="aspect-[3/4] bg-gray-950 rounded-lg overflow-hidden border border-gray-800 relative group flex items-center justify-center">
            <div id="detail-placeholder" class="hidden w-full h-full flex flex-col items-center justify-center bg-gray-900/50 text-gray-600 space-y-2 p-4 text-center">
              <svg class="w-12 h-12 stroke-emerald-500/40" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
              </svg>
              <span class="text-[10px] font-mono text-gray-500">3D MODEL NO DATA</span>
            </div>
            <img id="detail-image" src="" alt="Sculpture Scan" class="w-full h-full object-cover grayscale contrast-125 group-hover:scale-105 transition-transform duration-500">
            <span class="absolute bottom-2.5 left-2.5 text-[10px] font-mono text-gray-400 bg-black/70 backdrop-blur px-1.5 py-0.5 rounded border border-gray-800">3D SCULPTURE SCAN</span>
          </div>

          <div class="md:col-span-2 bg-gray-950/80 rounded-lg p-5 border border-gray-800/80 space-y-4 font-mono text-xs overflow-hidden">
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 border-b border-gray-800/80 pb-4">
              <div>
                <span class="text-gray-500 text-[10px] block">SERVICE TARGET (代理對象)</span>
                <span id="detail-target" class="font-bold text-gray-200">---</span>
              </div>
              <div>
                <span class="text-gray-500 text-[10px] block">ANXIETY INDEX (焦慮指數)</span>
                <span id="detail-anxiety" class="font-bold text-red-400">---</span>
              </div>
              
              <!-- 呼吸計數器區塊 -->
              <div class="sm:col-span-2 bg-emerald-950/20 p-3.5 rounded border border-emerald-500/20 w-full overflow-hidden">
                <div class="flex justify-between items-center mb-1.5 gap-2">
                  <span class="text-emerald-400 text-[10px] font-bold tracking-wider break-words leading-tight">
                    LIFETIME CUMULATIVE RESPIRATION (出生至今生命累積總呼吸數)
                  </span>
                  <span class="w-1.5 h-1.5 rounded-full bg-emerald-400 animate-ping shrink-0"></span>
                </div>
                <div class="flex flex-wrap items-baseline gap-x-2 gap-y-1 my-1">
                  <span id="detail-breath-counter" class="text-lg sm:text-xl md:text-2xl font-black text-emerald-400 breath-counter-active tracking-wider break-all">
                    0
                  </span>
                  <span class="text-[11px] text-gray-400 shrink-0">CYCLES (次)</span>
                </div>
                <p id="detail-birth-info" class="text-[10px] text-gray-500 mt-1 leading-normal break-words">
                  自出生日期起算，依成人平靜狀態每分鐘 15 次呼吸即時動態估算
                </p>
              </div>

              <div>
                <span class="text-gray-500 text-[10px] block">ECONOMIC OUTPUT (產出價值)</span>
                <span class="font-bold text-emerald-400">0.000 KG/H (NULL)</span>
              </div>
            </div>

            <div>
              <span class="text-gray-500 text-[10px] block mb-1">SYSTEM CLAUSE (授權條款)</span>
              <p class="text-gray-400 leading-relaxed text-[11px] font-sans">
                本體因無法忍受空閒狀態產生之罪惡感，現已將「維持最低限度生物性呼吸」之權限，完全移交予代理個案執行。
              </p>
            </div>
          </div>
        </div>

        <div class="bg-gray-950/90 rounded-lg p-5 border border-gray-800 space-y-3 font-mono">
          <div class="flex justify-between items-center text-xs">
            <span class="text-emerald-400 font-bold flex items-center gap-2">
              <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
              PNEUMATIC AUDIO MONITOR (代理呼吸音檔監控)
            </span>
            <span class="text-[10px] text-gray-500">48kHz / RAW RECORDING</span>
          </div>

          <audio id="breathing-audio" controls class="w-full h-10 rounded opacity-90 hover:opacity-100 transition-opacity">
            <source id="audio-source" src="" type="audio/mpeg">
            您的瀏覽器不支援音訊播放。
          </audio>
        </div>

        <div class="bg-gray-950/90 rounded-lg p-6 border border-gray-800/80 relative">
          <span class="text-[10px] font-mono text-gray-500 tracking-widest absolute top-3 right-4">STATEMENT ARCHIVE</span>
          <h3 class="text-xs font-mono text-gray-400 tracking-wider mb-3">【本體焦慮自白紀錄】</h3>
          <blockquote id="detail-statement" class="text-sm md:text-base text-gray-200 leading-relaxed font-sans italic border-l-2 border-emerald-500/60 pl-4 py-1">
            "---"
          </blockquote>
        </div>

      </article>
    </main>

    <!-- 頁尾 -->
    <footer class="border-t border-gray-800/60 mt-16 pt-6 text-center md:flex justify-between items-center text-xs text-gray-600 font-mono">
      <p>© SHAOQI SU. ALL RIGHTS RESERVED.</p>
      <p class="mt-2 md:mt-0">ARTWORK BY ANDREW SU </p>
    </footer>

  </div>

  <script>
    const PARTICIPANTS = [
      {
        id: "01",
        name: "蘇Ｏ齊",
        role: "代理呼吸員 01 號",
        target: "蘇Ｏ齊 (本體)",
        anxiety: "87.4% (極高)",
        birthDate: "2005-02-26",
        imageUrl: "https://cdn.phototourl.com/member/2026-10-25-96d3b302-64c7-4d0a-92c3-dae869f734ea.jpg",
        audioUrl: "breath01.mp3",
        statement: "我發現自己根本無法忍受純粹的放空。只要一停下來，那種『時間正被浪費』的罪惡感就會把我吞噬。我做這個替身，不是為了讓自己舒服地去休息，而是因為我停不下來——我需要一個實體掛在那裡，替我承擔什麼都不做、只剩下呼吸的死寂。"
      },
      {
        id: "02",
        name: "張Ｏ禎",
        role: "代理呼吸員 02 號",
        target: "張Ｏ禎 (本體)",
        anxiety: "91.2% (極高)",
        birthDate: "2005-07-10",
        imageUrl: "https://cdn.phototourl.com/member/2026-10-25-09d06678-a47a-49da-b2bb-c6197ce8a8ea.jpg",
        audioUrl: "breath02.mp3",
        statement: "只要超過半天沒有打開繪圖軟體或思考進度，我就會產生一種即將被同齡人徹底淘汰的恐慌。明明身體已經累到極限，但大腦還是強迫性地尋找事情做。我需要這台機器幫我把『休息』當成一項公事來認真執行。"
      },
      {
        id: "03",
        name: "林Ｏ岑",
        role: "代理呼吸員 03 號",
        target: "林Ｏ岑 (本體)",
        anxiety: "79.8% (高)",
        birthDate: "2005-06-09",
        imageUrl: "https://cdn.phototourl.com/member/2026-10-25-b70cd799-0bbf-4737-a890-d4c0962fe741.jpg",
        audioUrl: "breath03.mp3",
        statement: "休假對我來說不是放鬆，而是一場審判。躺在床上滑手機的每一分鐘，都在盤算著自己少做了多少事。如果一定要有人在那裡放空，那就讓這顆塑膠薄膜包覆的人頭替我坐牢吧。"
      },
      {
        id: "04",
        name: "陳Ｏ騏",
        role: "代理呼吸員 04 號",
        target: "陳Ｏ騏 (本體)",
        anxiety: "95.0% (準備中)",
        birthDate: "2005-01-01",
        imageUrl: "",
        audioUrl: "breath04.mp3",
        statement: "檔案建立中，等待資料輸入..."
      }
    ];

    let breathTimer = null;

    function calculateLifetimeBreaths(birthDateStr) {
      const birthDate = new Date(birthDateStr);
      const now = new Date();
      const diffInSeconds = (now - birthDate) / 1000;
      return Math.floor(diffInSeconds * 0.25);
    }

    function startBreathCounter(birthDateStr) {
      if (breathTimer) clearInterval(breathTimer);
      
      let currentBreaths = calculateLifetimeBreaths(birthDateStr);
      const counterEl = document.getElementById('detail-breath-counter');
      counterEl.innerText = currentBreaths.toLocaleString();

      breathTimer = setInterval(() => {
        currentBreaths += 1;
        counterEl.innerText = currentBreaths.toLocaleString();
      }, 4000);
    }

    function renderPortalCards() {
      const container = document.getElementById('cards-container');
      container.innerHTML = PARTICIPANTS.map(p => {
        const imgSrc = p.imageUrl ? `${p.imageUrl}?v=${Date.now()}` : '';
        return `
        <div onclick="showDetail('${p.id}')" class="glass-card rounded-xl overflow-hidden cursor-pointer flex flex-col justify-between relative group">
          <!-- 滿版 3:4 照片容器 -->
          <div class="aspect-[3/4] w-full bg-gray-950 relative overflow-hidden flex items-center justify-center">
            ${p.imageUrl ? `<img src="${imgSrc}" class="w-full h-full object-cover grayscale contrast-125 group-hover:scale-105 transition-transform duration-500">` : `
              <div class="flex flex-col items-center space-y-2 text-gray-700">
                <svg class="w-12 h-12 stroke-gray-700" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
                </svg>
                <span class="text-[10px] font-mono text-gray-600">NO SCAN DATA</span>
              </div>
            `}
            
            <!-- 漸層黑色遮罩 -->
            <div class="absolute inset-0 bg-gradient-to-t from-black/90 via-black/30 to-transparent"></div>

            <!-- 卡片頂部白色編號（無邊框） -->
            <div class="absolute top-3 left-3">
              <span class="text-xs font-mono text-white tracking-wider font-bold">CASE #${p.id}</span>
            </div>

            <!-- 卡片下半部文字資訊 -->
            <div class="absolute bottom-14 left-4 right-4 space-y-0.5">
              <h3 class="text-lg font-bold text-white tracking-wide">${p.name}</h3>
              <p class="text-xs text-gray-300 font-mono">${p.role}</p>
            </div>

            <!-- 覆蓋在照片下方的極光螢光綠按鈕（無邊框） -->
            <div class="absolute bottom-3 left-3 right-3">
              <button class="btn-neon w-full py-2 text-xs rounded shadow-lg flex items-center justify-center space-x-1">
                <span>檢視個案診斷</span>
                <span>→</span>
              </button>
            </div>
          </div>
        </div>
      `}).join('');
    }

    function showPortal() {
      document.getElementById('portal-view').classList.remove('hidden');
      document.getElementById('detail-view').classList.add('hidden');
      if (breathTimer) clearInterval(breathTimer);
      const audio = document.getElementById('breathing-audio');
      audio.pause();
    }

    function showDetail(id) {
      const data = PARTICIPANTS.find(p => p.id === id) || PARTICIPANTS[0];
      
      document.getElementById('detail-id').innerText = `CASE #${data.id}`;
      document.getElementById('detail-name').innerText = data.name;
      document.getElementById('detail-role').innerText = data.role;
      document.getElementById('detail-target').innerText = data.target;
      document.getElementById('detail-anxiety').innerText = data.anxiety;
      document.getElementById('detail-statement').innerText = `"${data.statement}"`;
      document.getElementById('detail-birth-info').innerText = `自出生日期 ${data.birthDate} 起算，依成人平靜狀態每分鐘 15 次呼吸即時動態估算`;

      const imgEl = document.getElementById('detail-image');
      const placeholderEl = document.getElementById('detail-placeholder');
      
      if (data.imageUrl) {
        placeholderEl.classList.add('hidden');
        imgEl.classList.remove('hidden');
        imgEl.src = `${data.imageUrl}?v=${Date.now()}`;
      } else {
        imgEl.classList.add('hidden');
        placeholderEl.classList.remove('hidden');
      }

      const audio = document.getElementById('breathing-audio');
      const source = document.getElementById('audio-source');
      source.src = data.audioUrl;
      audio.load();

      startBreathCounter(data.birthDate);

      document.getElementById('portal-view').classList.add('hidden');
      document.getElementById('detail-view').classList.remove('hidden');
      window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    window.addEventListener('DOMContentLoaded', () => {
      renderPortalCards();
      const urlParams = new URLSearchParams(window.location.search);
      const targetId = urlParams.get('id');
      if (targetId) showDetail(targetId);
    });
  </script>
</body>
</html>
