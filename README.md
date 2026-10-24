<!DOCTYPE html>
<html lang="zh-TW">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>PROXIMITY IDLE INC. - Archive Portal</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600;800&family=Noto+Sans+TC:wght@400;500;700;900&display=swap');

    body {
      font-family: 'JetBrains Mono', 'Noto Sans TC', sans-serif;
      background-color: #f8fafc;
      color: #0f172a;
    }

    /* 網格背景 */
    .bg-grid-light {
      background-size: 24px 24px;
      background-image: 
        linear-gradient(to right, rgba(0, 0, 0, 0.05) 1px, transparent 1px),
        linear-gradient(to bottom, rgba(0, 0, 0, 0.05) 1px, transparent 1px);
    }

    /* 螢光綠強烈撞色按鈕 */
    .btn-neon {
      background-color: #10b981;
      color: #000000;
      font-weight: 800;
      transition: all 0.2s ease;
      box-shadow: 4px 4px 0px #000000;
    }

    .btn-neon:hover {
      background-color: #34d399;
      transform: translate(-2px, -2px);
      box-shadow: 6px 6px 0px #000000;
    }

    /* 卡片陰影 */
    .card-neo {
      background-color: #ffffff;
      border: 2px solid #000000;
      box-shadow: 5px 5px 0px #000000;
      transition: all 0.2s ease;
    }

    .card-neo:hover {
      transform: translate(-3px, -3px);
      box-shadow: 8px 8px 0px #10b981;
    }

    /* 臨床紅色印章 */
    .stamp-red {
      border: 3px solid #dc2626;
      color: #dc2626;
      transform: rotate(-6deg);
      font-weight: 900;
    }
  </style>
</head>
<body class="bg-grid-light min-h-screen text-slate-900 pb-16">

  <!-- 頂部 Header -->
  <header class="bg-black text-white border-b-4 border-emerald-500 py-6 px-4 mb-10">
    <div class="max-w-5xl mx-auto flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
      <div>
        <div class="flex items-center space-x-2 text-xs font-bold text-emerald-400 mb-1">
          <span class="w-2.5 h-2.5 rounded-full bg-emerald-400 animate-ping"></span>
          <span>SYSTEM RUNNING | ARCHIVE ONLINE</span>
        </div>
        <h1 class="text-2xl md:text-3xl font-black tracking-tight">PROXIMITY IDLE INC.</h1>
        <p class="text-xs text-slate-400">當代個人怠工檔案與系統診斷報告 Portal</p>
      </div>

      <div class="bg-emerald-500 text-black px-4 py-2 font-mono text-xs font-black border-2 border-white shadow-[3px_3px_0px_#ffffff]">
        OUTPUT: 0.000 KG/H
      </div>
    </div>
  </header>

  <div class="max-w-5xl mx-auto px-4">

    <!-- 1. 門戶首頁（4 位參與者） -->
    <main id="portal-view" class="space-y-6">
      <div class="border-b-2 border-black pb-3 flex justify-between items-end">
        <div>
          <h2 class="text-xl font-black text-black">代理人檔案目錄</h2>
          <p class="text-xs text-slate-600">點擊以下個案卡片，檢視專屬「怠工評估與診斷檔案」</p>
        </div>
        <span class="text-xs font-bold bg-black text-white px-2 py-1">TOTAL: 04 CASES</span>
      </div>

      <!-- 4 張卡片列表 -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6" id="cards-container">
        <!-- 由 JavaScript 生成 -->
      </div>
    </main>


    <!-- 2. 第一版臨床診斷書詳情頁（含呼吸音檔） -->
    <main id="detail-view" class="hidden space-y-6">
      
      <!-- 返回按鈕 -->
      <button onclick="showPortal()" class="btn-neon px-5 py-2.5 rounded-none text-xs flex items-center space-x-2 border-2 border-black">
        <span>←</span>
        <span>返回檔案目錄 (RETURN TO DIRECTORY)</span>
      </button>

      <!-- 診斷書卡片 -->
      <article class="card-neo p-6 md:p-10 relative space-y-8">
        
        <!-- 頂部資訊 & 印章 -->
        <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center border-b-2 border-black pb-6 gap-4">
          <div>
            <span id="detail-id" class="inline-block bg-emerald-500 text-black text-xs font-black px-2 py-0.5 mb-2 border border-black">CASE #000</span>
            <h2 id="detail-name" class="text-3xl font-black text-black">---</h2>
            <p id="detail-role" class="text-xs font-bold text-slate-600 mt-1">---</p>
          </div>

          <div class="stamp-red px-4 py-2 text-xs font-black tracking-widest uppercase">
            AUTHORIZED IDLE
          </div>
        </div>

        <!-- 照片 & 診斷數據 -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8 items-center">
          <!-- 照片 -->
          <div class="aspect-square bg-slate-100 border-2 border-black overflow-hidden relative shadow-[4px_4px_0px_#000]">
            <img id="detail-image" src="" alt="Sculpture" class="w-full h-full object-cover grayscale">
            <span class="absolute bottom-2 left-2 bg-black text-white text-[10px] px-1.5 py-0.5 font-bold">3D SCULPTURE SCAN</span>
          </div>

          <!-- 臨床數據欄 -->
          <div class="md:col-span-2 bg-slate-50 border-2 border-black p-5 space-y-3 text-xs">
            <div class="grid grid-cols-2 gap-4 border-b border-slate-300 pb-3">
              <div>
                <span class="text-slate-500 text-[10px] block">SERVICE TARGET (代理對象)</span>
                <span id="detail-target" class="font-bold text-black">---</span>
              </div>
              <div>
                <span class="text-slate-500 text-[10px] block">ANXIETY INDEX (焦慮指數)</span>
                <span id="detail-anxiety" class="font-black text-red-600">---</span>
              </div>
              <div>
                <span class="text-slate-500 text-[10px] block">RESPIRATION KPI (每日指標)</span>
                <span id="detail-kpi" class="font-bold text-black">20,160 CYCLES/DAY</span>
              </div>
              <div>
                <span class="text-slate-500 text-[10px] block">ECONOMIC OUTPUT (產出價值)</span>
                <span class="font-bold text-emerald-600">0.000 KG/H</span>
              </div>
            </div>

            <div>
              <span class="text-slate-500 text-[10px] block mb-1">SYSTEM CLAUSE (授權條款)</span>
              <p class="text-slate-700 leading-relaxed text-[11px]">
                本體因無法忍受空閒狀態產生之罪惡感，現已將「維持最低限度生物性呼吸」之權限，完全移交予代理個案執行。
              </p>
            </div>
          </div>
        </div>

        <!-- 呼吸音檔播放器區塊 -->
        <div class="bg-black text-white p-5 border-2 border-black shadow-[4px_4px_0px_#10b981] space-y-3">
          <div class="flex justify-between items-center text-xs">
            <span class="text-emerald-400 font-bold flex items-center gap-2">
              <span class="w-2 h-2 rounded-full bg-emerald-400 animate-pulse"></span>
              PNEUMATIC AUDIO MONITOR (代理呼吸音檔)
            </span>
            <span class="text-[10px] text-slate-400">48kHz / RAW RECORDING</span>
          </div>

          <audio id="breathing-audio" controls class="w-full h-10 rounded">
            <source id="audio-source" src="" type="audio/mpeg">
            您的瀏覽器不支援音訊播放。
          </audio>
        </div>

        <!-- 焦慮自白區塊 -->
        <div class="bg-emerald-50 border-2 border-black p-6 relative shadow-[4px_4px_0px_#000]">
          <span class="bg-black text-emerald-400 text-[10px] font-bold px-2 py-0.5 absolute -top-3 left-4 border border-black">STATEMENT ARCHIVE</span>
          <h3 class="text-xs font-bold text-slate-500 mb-2">【本體焦慮自白紀錄】</h3>
          <blockquote id="detail-statement" class="text-sm md:text-base font-bold text-black leading-relaxed italic">
            "---"
          </blockquote>
        </div>

      </article>
    </main>

  </div>

  <script>
    const PARTICIPANTS = [
      {
        id: "01",
        name: "張簡庭",
        role: "代理呼吸員 01 號",
        target: "張簡庭 (本體)",
        anxiety: "87.4% (極高)",
        kpi: "20,160 次/日",
        imageUrl: "https://images.unsplash.com/photo-1544005313-94ddf0286df2?auto=format&fit=crop&q=80&w=600",
        audioUrl: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3",
        statement: "我發現自己根本無法忍受純粹的放空。只要一停下來，那種『時間正被浪費』的罪惡感就會把我吞噬。我做這個替身，不是為了讓自己舒服地去休息，而是因為我停不下來——我需要一個實體掛在那裡，替我承擔什麼都不做、只剩下呼吸的死寂。"
      },
      {
        id: "02",
        name: "參與者 B",
        role: "代理呼吸員 02 號",
        target: "參與者 B (本體)",
        anxiety: "91.2% (極高)",
        kpi: "20,160 次/日",
        imageUrl: "https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?auto=format&fit=crop&q=80&w=600",
        audioUrl: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-2.mp3",
        statement: "只要超過半天沒有打開繪圖軟體或思考進度，我就會產生一種即將被同齡人徹底淘汰的恐慌。明明身體已經累到極限，但大腦還是強迫性地尋找事情做。我需要這台機器幫我把『休息』當成一項公事來認真執行。"
      },
      {
        id: "03",
        name: "參與者 C",
        role: "代理呼吸員 03 號",
        target: "參與者 C (本體)",
        anxiety: "79.8% (高)",
        kpi: "20,160 次/日",
        imageUrl: "https://images.unsplash.com/photo-1500648767791-00dcc994a43e?auto=format&fit=crop&q=80&w=600",
        audioUrl: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-3.mp3",
        statement: "休假對我來說不是放鬆，而是一場審判。躺在床上滑手機的每一分鐘，都在盤算著自己少做了多少事。如果一定要有人在那裡放空，那就讓這顆塑膠薄膜包覆的人頭替我坐牢吧。"
      },
      {
        id: "04",
        name: "參與者 D",
        role: "代理呼吸員 04 號",
        target: "參與者 D (本體)",
        anxiety: "95.0% (危險臨界)",
        kpi: "20,160 次/日",
        imageUrl: "https://images.unsplash.com/photo-1534528741775-53994a69daeb?auto=format&fit=crop&q=80&w=600",
        audioUrl: "https://www.soundhelix.com/examples/mp3/SoundHelix-Song-4.mp3",
        statement: "我連休息都想要制定一套 SOP。這種病態的強迫症讓我意識到，我已經失去了『自然停下』的能力。現在，這個雕塑成了我唯一的替身，它負責呼吸，我負責繼續焦慮。"
      }
    ];

    function renderPortal() {
      const container = document.getElementById('cards-container');
      container.innerHTML = PARTICIPANTS.map(p => `
        <div onclick="showDetail('${p.id}')" class="card-neo p-4 cursor-pointer flex flex-col justify-between space-y-4">
          <div class="space-y-3">
            <div class="aspect-square bg-slate-100 border-2 border-black overflow-hidden">
              <img src="${p.imageUrl}" alt="${p.name}" class="w-full h-full object-cover grayscale hover:scale-105 transition-transform">
            </div>
            <div>
              <span class="bg-black text-white text-[10px] font-bold px-1.5 py-0.5">CASE #${p.id}</span>
              <h3 class="text-lg font-black text-black mt-1">${p.name}</h3>
              <p class="text-xs font-bold text-slate-500">${p.role}</p>
            </div>
          </div>
          <button class="btn-neon w-full py-2 text-xs border-2 border-black">
            檢視個案檔案 →
          </button>
        </div>
      `).join('');
    }

    function showPortal() {
      document.getElementById('portal-view').classList.remove('hidden');
      document.getElementById('detail-view').classList.add('hidden');
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
      document.getElementById('detail-kpi').innerText = data.kpi;
      document.getElementById('detail-image').src = data.imageUrl;
      document.getElementById('detail-statement').innerText = `"${data.statement}"`;

      const audio = document.getElementById('breathing-audio');
      const source = document.getElementById('audio-source');
      source.src = data.audioUrl;
      audio.load();

      document.getElementById('portal-view').classList.add('hidden');
      document.getElementById('detail-view').classList.remove('hidden');
      window.scrollTo({ top: 0, behavior: 'smooth' });
    }

    window.addEventListener('DOMContentLoaded', () => {
      renderPortal();
      const urlParams = new URLSearchParams(window.location.search);
      const targetId = urlParams.get('id');
      if (targetId) showDetail(targetId);
    });
  </script>
</body>
</html>
