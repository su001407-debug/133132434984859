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

    /* 螢光綠首頁按鈕樣式 */
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

    /* 對比標籤：一般綠色高亮燈號 */
    .badge-emerald-active {
      background-color: rgba(16, 185, 129, 0.2) !important;
      color: #10b981 !important;
      font-weight: 700 !important;
      border: 1px solid rgba(16, 185, 129, 0.5) !important;
      box-shadow: 0 0 12px rgba(16, 185, 129, 0.25);
    }

    .badge-inactive {
      background-color: rgba(15, 18, 22, 0.85) !important;
      color: #6b7280 !important;
      font-weight: 500 !important;
      border: 1px solid rgba(255, 255, 255, 0.1) !important;
      box-shadow: none !important;
    }

    .stamp-red {
      border: 2px solid #ef4444;
      color: #ef4444;
      transform: rotate(-6deg);
      letter-spacing: 0.15em;
      text-shadow: 0 0 10px rgba(239, 68, 68, 0.3);
      box-shadow: inset 0 0 12px rgba(239, 68, 68, 0.12), 0 0 8px rgba(239, 68, 68, 0.2);
    }

    @keyframes pulse-emerald {
      0%, 100% { color: #10b981; opacity: 1; }
      50% { color: #6ee7b7; opacity: 0.7; }
    }
    .breath-counter-active {
      animation: pulse-emerald 2s infinite;
    }

    @keyframes mobileFade {
      0%, 45% { opacity: 0; }
      55%, 95% { opacity: 1; }
      100% { opacity: 0; }
    }
    @media (hover: none) {
      .mobile-auto-fade {
        animation: mobileFade 6s infinite ease-in-out;
      }
      .mobile-auto-bg-fade {
        animation: mobileBgFade 6s infinite ease-in-out;
      }
    }

    @keyframes mobileBgFade {
      0%, 45% { background-color: rgba(0,0,0,0.7); backdrop-filter: blur(6px); }
      55%, 95% { background-color: transparent; backdrop-filter: none; }
      100% { background-color: rgba(0,0,0,0.7); backdrop-filter: blur(6px); }
    }

    /* 防止觸控拖曳拉條時捲動頁面 */
    #comparison-slider {
      touch-action: none;
    }
  </style>
</head>
<body class="bg-grid-dark min-h-screen text-gray-300 relative selection:bg-emerald-500 selection:text-black">

  <div class="fixed top-0 left-1/2 -translate-x-1/2 w-full max-w-6xl h-80 bg-emerald-950/20 blur-[130px] pointer-events-none rounded-full"></div>

  <div class="max-w-5xl mx-auto px-4 py-8 md:py-14 relative z-10">

    <!-- Header 頂部欄位 -->
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

      <div class="flex flex-col sm:flex-row items-stretch sm:items-center gap-3 w-full md:w-auto">
        <!-- 作品理念按鈕：螢光綠樣式 -->
        <button onclick="openConceptModal()" class="btn-neon inline-flex items-center justify-center space-x-2 text-xs px-4 py-2.5 rounded shadow-lg font-mono">
          <span>ⓘ</span>
          <span>作品理念 (CONCEPT)</span>
        </button>

        <div class="text-right font-mono text-xs text-gray-400 bg-gray-950/80 px-4 py-2.5 rounded border border-gray-800/80 flex justify-between sm:block">
          <span class="text-gray-500 mr-2">VALUABLE OUTPUT:</span>
          <span id="header-output-counter" class="text-emerald-400 font-bold">0.000 KG/H</span>
        </div>
      </div>
    </header>

    <!-- 1. 門戶首頁 -->
    <main id="portal-view" class="space-y-8">
      <div class="flex justify-between items-end border-b border-gray-800/60 pb-3">
        <div>
          <h2 class="text-lg font-bold text-white tracking-wide">委託人檔案目錄</h2>
          <p class="text-xs text-gray-500">點擊個案卡片，檢視完整「臨床診斷報告與生命累積呼吸數據」</p>
        </div>
        <span class="text-xs text-gray-600 font-mono">TOTAL: 04 CASES</span>
      </div>

      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6" id="cards-container">
      </div>
    </main>

    <!-- 2. 診斷檔案詳情頁 -->
    <main id="detail-view" class="hidden space-y-6">
      
      <!-- 返回檔案目錄按鈕 -->
      <button onclick="showPortal()" class="inline-flex items-center space-x-2 text-xs text-gray-300 hover:text-white transition-colors bg-gray-900/90 hover:bg-gray-800 px-4 py-2 rounded border border-gray-700">
        <span>←</span>
        <span>返回檔案目錄 (RETURN TO DIRECTORY)</span>
      </button>

      <article class="glass-card rounded-xl p-6 md:p-10 relative space-y-6">
        
        <!-- 個案 Header + 緊貼於橫線正上方的系統說明文字 -->
        <div class="border-b border-gray-800 pb-2 space-y-1">
          <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 mb-2">
            <div>
              <span id="detail-id" class="inline-block text-white text-xs font-mono mb-2">CASE #000</span>
              <h2 id="detail-name" class="text-2xl md:text-3xl font-bold text-white">---</h2>
              <p id="detail-role" class="text-xs font-mono text-gray-400 mt-1">---</p>
            </div>

            <div class="stamp-red px-4 py-1.5 rounded text-xs font-bold font-mono tracking-widest uppercase shrink-0">
              AUTHORIZED IDLE
            </div>
          </div>

          <!-- 說明文字緊貼橫線之上 -->
          <p class="text-[10px] font-mono text-gray-400 tracking-wide pb-1">
            [SYSTEM NOTE] 個人特徵（髮型/皮肉）已於代理化過程中剝離，僅保留骨架結構與氣動呼吸腔體。
          </p>
        </div>

        <!-- 照片對比與數據面板區域 -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6 items-stretch">
          
          <!-- 左側：照片對比區 -->
          <div id="detail-slider-container" class="w-full h-full min-h-[360px] md:min-h-full bg-gray-950 rounded-lg overflow-hidden border border-gray-800 relative select-none group">
            
            <!-- 底圖：代理裝置照片 (PROXY DEVICE) -->
            <img id="detail-device-img" src="" alt="Proxy Device" class="w-full h-full object-cover grayscale contrast-125 absolute inset-0 pointer-events-none z-0">
            
            <!-- 上圖：本體照片 (PRINCIPAL PHOTO) -->
            <div id="slider-clip-wrapper" class="absolute inset-0 overflow-hidden w-1/2 border-r-2 border-emerald-500 z-10">
              <img id="detail-principal-img" src="" alt="Principal" class="w-full h-full object-cover grayscale contrast-125 pointer-events-none" style="max-width: none;">
            </div>

            <!-- 可拖曳之原生 Range Slider -->
            <input type="range" min="0" max="100" value="50" id="comparison-slider" class="absolute inset-0 w-full h-full opacity-0 cursor-ew-resize z-30">

            <!-- 垂直指示線與一般綠色圓形拖曳圖示 -->
            <div id="slider-line" class="absolute top-0 bottom-0 w-0.5 bg-emerald-500 pointer-events-none z-20 left-1/2 -translate-x-1/2 shadow-[0_0_8px_rgba(16,185,129,0.5)]">
              <div class="w-6 h-6 rounded-full bg-emerald-500 text-black font-extrabold text-[10px] flex items-center justify-center absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 shadow-lg">
                ◄►
              </div>
            </div>

            <!-- 左右動態對比標籤 -->
            <span id="badge-principal" class="absolute bottom-2.5 left-2.5 text-[9px] font-mono backdrop-blur px-2.5 py-1 rounded transition-all duration-300 z-20 pointer-events-none badge-inactive">
              本體 PRINCIPAL
            </span>
            <span id="badge-device" class="absolute bottom-2.5 right-2.5 text-[9px] font-mono backdrop-blur px-2.5 py-1 rounded transition-all duration-300 z-20 pointer-events-none badge-inactive">
              裝置 PROXY DEVICE
            </span>
          </div>

          <!-- 右側：數據面板 -->
          <div class="md:col-span-2 bg-gray-950/80 rounded-lg p-5 border border-gray-800/80 flex flex-col justify-between space-y-4 font-mono text-xs overflow-hidden">
            <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 border-b border-gray-800/80 pb-4">
              <div>
                <span class="text-gray-500 text-[10px] block">SERVICE TARGET (代理對象)</span>
                <span id="detail-target" class="font-bold text-gray-200">---</span>
              </div>
              <div>
                <span class="text-gray-500 text-[10px] block">ANXIETY INDEX (焦慮指數)</span>
                <span id="detail-anxiety" class="font-bold text-red-400">---</span>
              </div>
              
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
                <span id="detail-output-counter" class="font-bold text-emerald-400">0.000 KG/H (NULL)</span>
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

    <!-- 3. 作品理念 彈出視窗（創作者「我」第一人稱視角） -->
    <div id="concept-modal" class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/80 backdrop-blur-md hidden transition-opacity duration-300">
      <div class="bg-gray-950 max-w-2xl w-full max-h-[85vh] rounded-xl border border-gray-800/80 p-6 md:p-8 overflow-y-auto space-y-6 text-sm relative shadow-2xl">
        
        <div class="flex justify-between items-center border-b border-gray-800 pb-4">
          <div>
            <span class="text-[10px] font-mono text-emerald-500 tracking-widest block">CURATORIAL STATEMENT</span>
            <h2 class="text-xl font-bold text-white font-mono">《理想狀態》作品理念</h2>
          </div>
          <button onclick="closeConceptModal()" class="text-gray-400 hover:text-white font-mono text-lg px-2">✕</button>
        </div>

        <div class="space-y-5 text-gray-300 font-sans leading-relaxed text-xs md:text-sm">
          
          <section class="space-y-1.5">
            <h3 class="text-emerald-500 font-mono font-bold text-xs">01. 創作發想：當代異化與假期的罪惡感</h3>
            <p class="text-gray-400">
              在這個高度追求效率與生產力的當代社會中，「空閒」對我而言逐漸轉化為一種罪惡感的來源。這件作品源自於我在假期中的一段空閒時間，當時我意識到，在這段毫無自我價值提升的時光裡，我的內心竟不斷萌生出一種「時間正被浪費」的焦慮與罪惡感。這樣的狀態迫使我開始思考：「我們是不是習慣用產出與結果，來證明一個人的價值？」「如果一個人做某件事卻沒有產出任何價值，它的存在是否仍值得被承認？」
            </p>
          </section>

          <section class="space-y-1.5">
            <h3 class="text-emerald-500 font-mono font-bold text-xs">02. 核心概念：生產一件代替我停止生產的作品</h3>
            <p class="text-gray-400">
              對我而言，創作原本是一種創造價值與實現自我的方式。然而在過往的經驗中，當我沒有持續創作或完成任何事情時，便極易陷入生產力恐慌。於是我產生了一個想法：既然創作對我來說是一種創造價值的行為，那麼，我是否能「生產一件代替我休息、只是在呼吸而沒有實際產出的作品」？我試圖透過這樣的矛盾，讓作品暫時代替我完成一次真正的「休息」。它不需要完成任何事情，也不以產出任何結果為目的，只是不斷地呼吸，將原本被我視為缺乏價值的空白時間，轉化為作品本身的一部分。
            </p>
          </section>

          <section class="space-y-1.5">
            <h3 class="text-emerald-500 font-mono font-bold text-xs">03. 氣動代理與無結果的過程</h3>
            <p class="text-gray-400">
              作品由四件單獨固定於牆上的頭部雕塑組成。並將參與者的個人特徵（皮肉與頭髮）剝離，僅留存五官結構。為了將「呼吸」視覺化，我採用自製氣動裝置搭配塑膠薄膜包裹雕塑，利用裝置抽氣與放氣的特性，模擬人頭套著塑膠袋呼吸時的膨脹與收縮，進而製造雕塑正在呼吸的錯覺。我希望讓這件作品暫時代替我停止生產，也邀請觀者一同觀看一個沒有結果的過程。在這段只剩下呼吸與時間流動的狀態中，重新思考一個沒有產出的行為，是否仍然具有存在的價值。
            </p>
          </section>

        </div>

        <!-- 一般深灰色關閉按鈕 -->
        <div class="border-t border-gray-800 pt-4 flex justify-end">
          <button onclick="closeConceptModal()" class="px-5 py-2 text-xs font-mono text-gray-300 hover:text-white bg-gray-900 hover:bg-gray-800 rounded border border-gray-700">
            關閉視窗 (CLOSE)
          </button>
        </div>

      </div>
    </div>

    <footer class="border-t border-gray-800/60 mt-16 pt-6 text-center md:flex justify-between items-center text-xs text-gray-600 font-mono">
      <p>© SHAOQI SU. ALL RIGHTS RESERVED.</p>
      <p class="mt-2 md:mt-0">ARTWORK BY SHAOQI SU</p>
    </footer>

  </div>

  <script>
    // 個案參與者資料庫
    const PARTICIPANTS = [
      {
        id: "01",
        name: "蘇Ｏ齊",
        role: "代理呼吸員 01 號",
        target: "蘇Ｏ齊 (本體)",
        anxiety: "87.4% (極高)",
        birthDate: "2005-02-26",
        imageUrl: "https://cdn.phototourl.com/member/2026-10-25-96d3b302-64c7-4d0a-92c3-dae869f734ea.jpg",
        deviceImageUrl: "https://cdn.phototourl.com/member/2026-10-25-32f03bb8-e07f-4f01-97b6-a7cdcd3b1edd.jpg",
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
        deviceImageUrl: "https://cdn.phototourl.com/member/2026-10-25-9afd07b5-083e-4c4d-a816-f5d9519e8f92.jpg",
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
        deviceImageUrl: "https://cdn.phototourl.com/member/2026-10-25-b70cd799-0bbf-4737-a890-d4c0962fe741.jpg",
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
        deviceImageUrl: "",
        audioUrl: "breath04.mp3",
        statement: "檔案建立中，等待資料輸入..."
      }
    ];

    let breathTimer = null;

    // 作品理念 Modal 開關控制
    function openConceptModal() {
      document.getElementById('concept-modal').classList.remove('hidden');
    }

    function closeConceptModal() {
      document.getElementById('concept-modal').classList.add('hidden');
    }

    // 點擊 Modal 背景關閉視窗
    document.getElementById('concept-modal')?.addEventListener('click', function(e) {
      if (e.target === this) closeConceptModal();
    });

    // 1. 高速跳動與 0.5 秒凍結歸零邏輯
    function startOutputFluctuationWithPause() {
      const headerOutputEl = document.getElementById('header-output-counter');
      const detailOutputEl = document.getElementById('detail-output-counter');
      let isPaused = false;

      function updateCounter() {
        if (isPaused) return;

        if (Math.random() < 0.15) {
          isPaused = true;
          const zeroVal = "0.000";
          if (headerOutputEl) headerOutputEl.innerText = `${zeroVal} KG/H`;
          if (detailOutputEl) detailOutputEl.innerText = `${zeroVal} KG/H (NULL)`;

          setTimeout(() => {
            isPaused = false;
          }, 500);
        } else {
          const d1 = Math.floor(Math.random() * 10);
          const d2 = Math.floor(Math.random() * 10);
          const d3 = Math.floor(Math.random() * 10);
          const d4 = Math.floor(Math.random() * 10);
          
          const randomVal = `${d1}.${d2}${d3}${d4}`;

          if (headerOutputEl) headerOutputEl.innerText = `${randomVal} KG/H`;
          if (detailOutputEl) detailOutputEl.innerText = `${randomVal} KG/H (NULL)`;
        }
      }

      setInterval(updateCounter, 80);
    }

    // 2. 出生至今呼吸次數估算
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

    // 3. 左右圖片對比拉條與標籤動態高亮
    function updateImgDimensions() {
      const sliderContainer = document.getElementById('detail-slider-container');
      const principalImg = document.getElementById('detail-principal-img');
      if (sliderContainer && principalImg) {
        const width = sliderContainer.clientWidth;
        const height = sliderContainer.clientHeight;
        principalImg.style.width = `${width}px`;
        principalImg.style.height = `${height}px`;
      }
    }

    function initComparisonSlider() {
      const slider = document.getElementById('comparison-slider');
      const clipWrapper = document.getElementById('slider-clip-wrapper');
      const sliderLine = document.getElementById('slider-line');
      const badgePrincipal = document.getElementById('badge-principal');
      const badgeDevice = document.getElementById('badge-device');

      function updateSlider(val) {
        clipWrapper.style.width = `${val}%`;
        sliderLine.style.left = `${val}%`;

        // 數值判斷：> 55 高亮本體，< 45 高亮裝置，45~55 居中時兩者都不亮
        if (val > 55) {
          badgePrincipal.className = "absolute bottom-2.5 left-2.5 text-[9px] font-mono backdrop-blur px-2.5 py-1 rounded transition-all duration-300 z-20 pointer-events-none badge-emerald-active";
          badgeDevice.className = "absolute bottom-2.5 right-2.5 text-[9px] font-mono backdrop-blur px-2.5 py-1 rounded transition-all duration-300 z-20 pointer-events-none badge-inactive";
        } else if (val < 45) {
          badgePrincipal.className = "absolute bottom-2.5 left-2.5 text-[9px] font-mono backdrop-blur px-2.5 py-1 rounded transition-all duration-300 z-20 pointer-events-none badge-inactive";
          badgeDevice.className = "absolute bottom-2.5 right-2.5 text-[9px] font-mono backdrop-blur px-2.5 py-1 rounded transition-all duration-300 z-20 pointer-events-none badge-emerald-active";
        } else {
          // 45 ~ 55 中間區域：兩者皆不亮
          badgePrincipal.className = "absolute bottom-2.5 left-2.5 text-[9px] font-mono backdrop-blur px-2.5 py-1 rounded transition-all duration-300 z-20 pointer-events-none badge-inactive";
          badgeDevice.className = "absolute bottom-2.5 right-2.5 text-[9px] font-mono backdrop-blur px-2.5 py-1 rounded transition-all duration-300 z-20 pointer-events-none badge-inactive";
        }
      }

      slider.addEventListener('input', (e) => {
        updateSlider(e.target.value);
      });

      window.addEventListener('resize', updateImgDimensions);
      updateImgDimensions();
    }

    // 4. 首頁卡片渲染（切換第二張圖時，只讓黑底與毛玻璃消失，CASE 文字保留）
    function renderPortalCards() {
      const container = document.getElementById('cards-container');
      container.innerHTML = PARTICIPANTS.map(p => {
        const imgSrc = p.imageUrl ? `${p.imageUrl}?v=${Date.now()}` : '';
        const deviceImgSrc = (p.deviceImageUrl || p.imageUrl) ? `${(p.deviceImageUrl || p.imageUrl)}?v=${Date.now()}` : '';
        
        return `
        <div onclick="showDetail('${p.id}')" class="glass-card rounded-xl overflow-hidden cursor-pointer flex flex-col justify-between relative group">
          <div class="aspect-[3/4] w-full bg-gray-950 relative overflow-hidden flex items-center justify-center">
            
            <!-- CASE #XX 左上角：切換到第二張圖時，僅黑底/毛玻璃消失，文字留存 -->
            <div class="absolute top-3 left-3 pointer-events-none z-30">
              <span class="text-xs font-mono text-white tracking-wider font-bold bg-black/70 backdrop-blur-md px-2.5 py-1 rounded shadow-lg inline-block transition-all duration-300 group-hover:bg-transparent group-hover:backdrop-blur-none group-hover:shadow-none mobile-auto-bg-fade">
                CASE #${p.id}
              </span>
            </div>

            ${p.imageUrl ? `
              <img src="${imgSrc}" class="w-full h-full object-cover grayscale contrast-125 group-hover:scale-105 transition-all duration-500 absolute inset-0 z-0">
              <img src="${deviceImgSrc}" class="w-full h-full object-cover grayscale contrast-125 opacity-0 group-hover:opacity-100 mobile-auto-fade group-hover:scale-105 transition-all duration-500 absolute inset-0 z-10">
            ` : `
              <div class="flex flex-col items-center space-y-2 text-gray-700">
                <svg class="w-12 h-12 stroke-gray-700" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
                </svg>
                <span class="text-[10px] font-mono text-gray-600">NO SCAN DATA</span>
              </div>
            `}
            
            <div class="absolute inset-0 bg-gradient-to-t from-black/90 via-black/30 to-transparent pointer-events-none z-20"></div>

            <div class="absolute bottom-14 left-4 right-4 space-y-0.5 pointer-events-none z-30">
              <h3 class="text-lg font-bold text-white tracking-wide">${p.name}</h3>
              <p class="text-xs text-gray-300 font-mono">${p.role}</p>
            </div>

            <div class="absolute bottom-3 left-3 right-3 z-30">
              <button class="btn-neon w-full py-2 text-xs rounded shadow-lg flex items-center justify-center space-x-1">
                <span>檢視個案診斷</span>
                <span>→</span>
              </button>
            </div>
          </div>
        </div>
      `}).join('');
    }

    // 5. 檢視切換控制
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

      const principalImg = document.getElementById('detail-principal-img');
      const deviceImg = document.getElementById('detail-device-img');
      
      const pUrl = data.imageUrl ? `${data.imageUrl}?v=${Date.now()}` : '';
      const dUrl = data.deviceImageUrl ? `${data.deviceImageUrl}?v=${Date.now()}` : pUrl;

      principalImg.src = pUrl;
      deviceImg.src = dUrl;

      // 重設 Slider 到 50% 位置
      document.getElementById('comparison-slider').value = 50;
      document.getElementById('slider-clip-wrapper').style.width = '50%';
      document.getElementById('slider-line').style.left = '50%';

      // 預設 50% 時兩者皆不亮
      document.getElementById('badge-principal').className = "absolute bottom-2.5 left-2.5 text-[9px] font-mono backdrop-blur px-2.5 py-1 rounded transition-all duration-300 z-20 pointer-events-none badge-inactive";
      document.getElementById('badge-device').className = "absolute bottom-2.5 right-2.5 text-[9px] font-mono backdrop-blur px-2.5 py-1 rounded transition-all duration-300 z-20 pointer-events-none badge-inactive";

      const audio = document.getElementById('breathing-audio');
      const source = document.getElementById('audio-source');
      source.src = data.audioUrl;
      audio.load();

      startBreathCounter(data.birthDate);

      document.getElementById('portal-view').classList.add('hidden');
      document.getElementById('detail-view').classList.remove('hidden');
      window.scrollTo({ top: 0, behavior: 'smooth' });

      // 確保圖片在 Viewport 展開後更新絕對寬度
      setTimeout(updateImgDimensions, 60);
    }

    // DOM 載入後初始化
    window.addEventListener('DOMContentLoaded', () => {
      renderPortalCards();
      initComparisonSlider();
      startOutputFluctuationWithPause();

      const urlParams = new URLSearchParams(window.location.search);
      const targetId = urlParams.get('id');
      if (targetId) showDetail(targetId);
    });
  </script>
</body>
</html>
