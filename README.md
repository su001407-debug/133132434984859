<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PROXIMITY IDLE INC. - Archive System</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:ital,wght@0,300;0,400;0,700;1,400&family=Noto+Sans+TC:wght@300;400;500;700&display=swap');
        
        body {
            font-family: 'JetBrains Mono', 'Noto Sans TC', monospace;
            background-color: #0d0d0d;
            color: #d1d5db;
        }

        .scanline {
            background: linear-gradient(
                to bottom,
                rgba(255,255,255,0),
                rgba(255,255,255,0) 50%,
                rgba(0, 0, 0, 0.3) 50%,
                rgba(0, 0, 0, 0.3)
            );
            background-size: 100% 4px;
        }

        .stamp {
            transform: rotate(-12deg);
        }

        .pulse-slow {
            animation: pulse 4s cubic-bezier(0.4, 0, 0.6, 1) infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.3; }
        }
    </style>
</head>
<body class="min-h-screen bg-black text-neutral-300 p-4 md:p-8 relative selection:bg-neutral-800 selection:text-white">
    <!-- Background Texture Scanline -->
    <div class="fixed inset-0 pointer-events-none scanline z-50 opacity-40"></div>

    <!-- Main Container / Dossier Window -->
    <div class="max-w-xl mx-auto bg-neutral-950 border border-neutral-800 rounded-none shadow-2xl relative overflow-hidden my-4">
        
        <!-- Header / Classification Bar -->
        <div class="bg-neutral-900 border-b border-neutral-800 p-4 flex justify-between items-center text-xs tracking-widest text-neutral-500 uppercase">
            <div class="flex items-center space-x-2">
                <span class="w-2 h-2 rounded-full bg-emerald-500 inline-block pulse-slow"></span>
                <span class="text-neutral-400 font-bold">SYSTEM STATUS: IDLE_ACTIVE</span>
            </div>
            <span>DOC-NO: #PROX-2026-003</span>
        </div>

        <!-- Inner Content Sheet -->
        <div class="p-6 md:p-8 space-y-6 text-sm relative">

            <!-- Confident Stamp -->
            <div class="absolute top-6 right-6 border-2 border-red-800/60 text-red-700/70 font-black px-3 py-1 text-xs uppercase tracking-wider stamp pointer-events-none select-none">
                INTERNAL USE ONLY / NON-PRODUCTIVE
            </div>

            <!-- Title Section -->
            <div class="border-b border-neutral-800 pb-4">
                <div class="text-xs text-neutral-500 uppercase tracking-wider mb-1">PROXIMITY IDLE INC. // SYSTEM DIAGNOSIS</div>
                <h1 class="text-xl font-bold text-white tracking-tight">個人怠工檔案與系統診斷報告</h1>
                <p class="text-xs text-neutral-400 mt-1">代號：代理呼吸員 03 號 (Respiratory Proxy No. 03)</p>
            </div>

            <!-- Metadata Table -->
            <div class="grid grid-cols-2 gap-4 bg-neutral-900/50 p-4 border border-neutral-800/80 text-xs">
                <div>
                    <span class="text-neutral-500 block uppercase">本體姓名 Subject</span>
                    <span class="text-neutral-200 font-semibold">張簡庭 (CHANG CHIEN TING)</span>
                </div>
                <div>
                    <span class="text-neutral-500 block uppercase">當前狀態 Status</span>
                    <span class="text-amber-500 font-semibold">強迫性心理過載 (Overload)</span>
                </div>
                <div>
                    <span class="text-neutral-500 block uppercase">核心障礙 Diagnosis</span>
                    <span class="text-neutral-300">無法承受無產出時間 (Zero-Productivity Anxiety)</span>
                </div>
                <div>
                    <span class="text-neutral-500 block uppercase">罪惡感指數 Index</span>
                    <span class="text-red-400 font-bold">94.2% (HIGH)</span>
                </div>
            </div>

            <!-- Delegation Authorization (The SOP Section) -->
            <div class="space-y-2">
                <div class="text-xs font-bold uppercase tracking-wider text-neutral-400 flex items-center">
                    <span class="text-neutral-600 mr-2">[01]</span> 代理授權條款 (DELEGATION AGREEMENT)
                </div>
                <div class="p-3 bg-neutral-900/30 border-l-2 border-neutral-700 text-xs text-neutral-400 leading-relaxed space-y-2">
                    <p>
                        鑑於本體大腦機制無法停止思考與產出，且極度抗拒純粹放空；現已正式將<b>「維持生命最低限度（氣體交換）」</b>之基礎機能，完全移交予 [代理呼吸員 03 號] 實體化執行。
                    </p>
                    <p class="text-neutral-500 italic">
                        ※ 授權生效期間，本體得以在不產生道德罪惡感之情況下，繼續進行無意義之焦慮。
                    </p>
                </div>
            </div>

            <!-- Real Confession / Self-Assessment Section -->
            <div class="space-y-2">
                <div class="text-xs font-bold uppercase tracking-wider text-neutral-400 flex items-center">
                    <span class="text-neutral-600 mr-2">[02]</span> 本體心理自白紀錄 (SUBJECT CONFESSION)
                </div>
                <div class="p-4 bg-black border border-neutral-800 relative">
                    <div class="text-neutral-600 text-2xl font-serif absolute top-1 left-2 select-none">“</div>
                    <p class="text-neutral-300 text-xs md:text-sm leading-relaxed relative z-10 px-3 py-1 font-sans">
                        我發現我根本無法忍受純粹的放空。只要一停下來，那種『時間被浪費』的罪惡感就會瞬間把我吞噬。
                        <br><br>
                        我做這個替身，不是為了讓自己舒服地去休息，而是因為我根本停不下來——我需要一個實體掛在那裡，替我承擔什麼都不做、只剩下呼吸的死寂。
                    </p>
                    <div class="text-neutral-600 text-2xl font-serif absolute bottom-1 right-2 select-none">”</div>
                </div>
            </div>

            <!-- Live Output Statistics -->
            <div class="space-y-2">
                <div class="text-xs font-bold uppercase tracking-wider text-neutral-400 flex items-center">
                    <span class="text-neutral-600 mr-2">[03]</span> 即時運作指標 (PERFORMANCE METRICS)
                </div>
                <div class="grid grid-cols-3 gap-2 text-center text-xs">
                    <div class="p-3 bg-neutral-900/50 border border-neutral-800">
                        <div class="text-neutral-500 text-[10px]">今日呼吸次數</div>
                        <div class="text-white font-mono font-bold mt-1 text-sm">18,420</div>
                        <div class="text-[9px] text-neutral-600">TIMES / DAY</div>
                    </div>
                    <div class="p-3 bg-neutral-900/50 border border-neutral-800">
                        <div class="text-neutral-500 text-[10px]">累計怠工時數</div>
                        <div class="text-white font-mono font-bold mt-1 text-sm">482.5</div>
                        <div class="text-[9px] text-neutral-600">HOURS</div>
                    </div>
                    <div class="p-3 bg-neutral-900/50 border border-neutral-800">
                        <div class="text-neutral-500 text-[10px]">經濟價值產出</div>
                        <div class="text-emerald-500 font-mono font-bold mt-1 text-sm">0.000</div>
                        <div class="text-[9px] text-neutral-600">TWD / KG</div>
                    </div>
                </div>
            </div>

            <!-- Footer / Verification Signature -->
            <div class="border-t border-neutral-800 pt-4 flex justify-between items-end text-[10px] text-neutral-500 font-mono">
                <div>
                    <div>SYSTEM: V3.2_STABLE</div>
                    <div>ENCRYPTION: AES-256-IDLE</div>
                </div>
                <div class="text-right">
                    <div class="border-b border-neutral-700 pb-1 mb-1 text-neutral-400 font-serif italic">Chien-Ting Chang</div>
                    <div>AUTHORIZED SIGNATURE</div>
                </div>
            </div>

        </div>

        <!-- Bottom Status Line -->
        <div class="bg-neutral-900/80 border-t border-neutral-800 px-6 py-2 text-[10px] text-neutral-500 flex justify-between items-center">
            <span>PROXIMITY IDLE INC. ALL RIGHTS RESERVED.</span>
            <span class="text-neutral-400">NO VALUE GENERATED</span>
        </div>

    </div>
</body>
</html>
