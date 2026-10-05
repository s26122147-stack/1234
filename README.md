# 1234
<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SHOWA DEV - 昭和像素闖關作品集</title>
    <!-- Google Pixel Font -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Noto+Sans+TC:wght@500;700;900&display=swap" rel="stylesheet">
    
    <style>
        :root {
            --bg-color: #0d0b18;
            --card-bg: #1a1528;
            --border-primary: #ff3366;
            --border-secondary: #ffd700;
            --text-main: #f8f9fa;
            --text-accent: #00ffcc;
            --text-dim: #7a7393;
            --btn-active-bg: #2b1f40;
            --btn-active-hover: #ff0055;
            --btn-locked-bg: #120e1c;
            --pixel-shadow: 4px 4px 0px #000;
            --pixel-shadow-lg: 6px 6px 0px #000;
        }

        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            user-select: none;
        }

        body {
            background-color: var(--bg-color);
            color: var(--text-main);
            font-family: 'Noto Sans TC', 'Press Start 2P', monospace, sans-serif;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            position: relative;
            overflow-x: hidden;
            /* 昭和電視噪點微紋理背景 */
            background-image: 
                radial-gradient(circle at 50% 50%, #221a36 0%, #0a0813 100%),
                linear-gradient(rgba(255, 255, 255, 0.03) 1px, transparent 1px),
                linear-gradient(90deg, rgba(255, 255, 255, 0.03) 1px, transparent 1px);
            background-size: 100% 100%, 20px 20px, 20px 20px;
        }

        /* CRT 復古電視掃描線效果 */
        .crt-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            background: linear-gradient(
                rgba(18, 16, 16, 0) 50%, 
                rgba(0, 0, 0, 0.35) 50%
            );
            background-size: 100% 4px;
            z-index: 99;
            pointer-events: none;
            opacity: 0.8;
        }

        /* 畫面螢光閃爍特效 */
        @keyframes crt-flicker {
            0% { opacity: 0.97; }
            50% { opacity: 1; }
            100% { opacity: 0.98; }
        }

        .main-container {
            animation: crt-flicker 0.15s infinite;
            max-width: 960px;
            width: 100%;
            margin: 0 auto;
            position: relative;
            z-index: 10;
        }

        /* 昭和電玩風格標題與個人卡 */
        .header-section {
            background-color: var(--card-bg);
            border: 4px solid var(--border-primary);
            box-shadow: var(--pixel-shadow-lg), inset -4px -4px 0px #0a0813, inset 4px 4px 0px #3d2f5c;
            border-radius: 8px;
            padding: 24px 20px;
            text-align: center;
            margin-bottom: 28px;
            position: relative;
        }

        .header-title {
            font-family: 'Press Start 2P', cursive;
            color: var(--border-secondary);
            font-size: 1.4rem;
            text-shadow: 3px 3px 0px #ff0055, 6px 6px 0px #000;
            margin-bottom: 18px;
            letter-spacing: 1px;
        }

        .avatar-container {
            position: relative;
            width: 100px;
            height: 100px;
            margin: 0 auto 16px auto;
        }

        .avatar-img {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            border: 4px solid var(--text-accent);
            box-shadow: 0 0 15px rgba(0, 255, 204, 0.5), var(--pixel-shadow);
            object-fit: cover;
            background-color: #100b1e;
            image-rendering: pixelated;
        }

        .avatar-badge {
            position: absolute;
            bottom: -5px;
            right: -5px;
            background: #ff0055;
            color: #fff;
            font-size: 0.7rem;
            font-weight: bold;
            padding: 2px 6px;
            border: 2px solid #000;
            font-family: 'Press Start 2P', cursive;
        }

        .player-name {
            font-size: 1.4rem;
            font-weight: 900;
            color: var(--text-main);
            letter-spacing: 2px;
            text-shadow: 2px 2px 0px #000;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        .player-title {
            color: var(--text-accent);
            font-size: 0.9rem;
            margin-top: 4px;
            font-weight: bold;
        }

        /* 遊戲通關進度條 */
        .progress-box {
            margin-top: 18px;
            background: #0d0a17;
            border: 2px solid var(--border-secondary);
            padding: 10px 14px;
            border-radius: 4px;
            display: inline-block;
            max-width: 100%;
        }

        .progress-text {
            font-family: 'Press Start 2P', cursive;
            font-size: 0.75rem;
            color: var(--border-secondary);
            margin-bottom: 6px;
        }

        .progress-bar-bg {
            width: 240px;
            max-width: 100%;
            height: 14px;
            background: #251d38;
            border: 2px solid #000;
            margin: 0 auto;
            position: relative;
            overflow: hidden;
        }

        .progress-bar-fill {
            width: 12.5%; /* 2/16 = 12.5% */
            height: 100%;
            background: linear-gradient(90deg, #00ffcc, #00ff66);
            box-shadow: 0 0 8px #00ffcc;
        }

        /* 16 關卡選擇網格 */
        .stage-grid {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 16px;
        }

        .stage-card {
            background-color: var(--btn-active-bg);
            border: 3px solid var(--text-accent);
            border-radius: 6px;
            padding: 14px 10px;
            text-decoration: none;
            color: var(--text-main);
            display: flex;
            flex-direction: column;
            justify-content: space-between;
            min-height: 105px;
            position: relative;
            box-shadow: var(--pixel-shadow), inset -2px -2px 0px #120b24, inset 2px 2px 0px #4d3a73;
            transition: all 0.15s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            cursor: pointer;
        }

        .stage-number {
            font-family: 'Press Start 2P', cursive;
            font-size: 0.65rem;
            color: var(--border-secondary);
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .stage-status-tag {
            font-size: 0.65rem;
            background: #00ffcc;
            color: #000;
            padding: 1px 4px;
            font-weight: bold;
            border-radius: 2px;
        }

        .stage-title {
            font-size: 0.95rem;
            font-weight: bold;
            margin-top: 8px;
            line-height: 1.3;
            color: #fff;
            word-break: break-word;
        }

        /* 已解鎖關卡的酷炫 Hover 動畫 */
        .stage-card.unlocked:hover {
            transform: translateY(-5px) scale(1.03);
            background-color: var(--btn-active-hover);
            border-color: #fff;
            box-shadow: 0 0 15px rgba(255, 0, 85, 0.8), 6px 6px 0px #000;
        }

        .stage-card.unlocked:hover .stage-title {
            color: #ffff00;
            text-shadow: 1px 1px 0px #000;
        }

        .stage-card.unlocked:active {
            transform: translateY(2px) scale(0.98);
            box-shadow: 2px 2px 0px #000;
        }

        /* 未解鎖關卡 (灰色鎖定狀態) */
        .stage-card.locked {
            background-color: var(--btn-locked-bg);
            border-color: #38304d;
            box-shadow: 2px 2px 0px #000;
            cursor: not-allowed;
            opacity: 0.65;
        }

        .stage-card.locked .stage-number {
            color: var(--text-dim);
        }

        .stage-card.locked .stage-title {
            color: var(--text-dim);
        }

        /* 未解鎖關卡的鎖頭與 Shake 效果 */
        .lock-icon {
            font-size: 1.1rem;
            margin-right: 4px;
            filter: grayscale(80%);
        }

        @keyframes lock-shake {
            0% { transform: translateX(0); }
            20% { transform: translateX(-4px) rotate(-3deg); }
            40% { transform: translateX(4px) rotate(3deg); }
            60% { transform: translateX(-3px) rotate(-2deg); }
            80% { transform: translateX(3px) rotate(2deg); }
            100% { transform: translateX(0); }
        }

        .stage-card.locked:hover {
            animation: lock-shake 0.35s ease-in-out;
            border-color: #ff3333;
            opacity: 0.85;
        }

        .stage-card.locked:hover .lock-icon {
            filter: grayscale(0%);
        }

        .footer-note {
            text-align: center;
            margin-top: 28px;
            font-size: 0.75rem;
            color: var(--text-dim);
            font-family: 'Press Start 2P', cursive;
            letter-spacing: 1px;
        }

        /* 響應式微調 (RWD) */
        @media (max-width: 860px) {
            .stage-grid {
                grid-template-columns: repeat(3, 1fr);
            }
        }

        @media (max-width: 600px) {
            .stage-grid {
                grid-template-columns: repeat(2, 1fr);
                gap: 12px;
            }
            .header-title {
                font-size: 1.1rem;
            }
            .player-name {
                font-size: 1.2rem;
            }
            .stage-card {
                min-height: 95px;
                padding: 10px;
            }
            .stage-title {
                font-size: 0.85rem;
            }
        }

        @media (max-width: 380px) {
            .stage-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>

    <!-- CRT 螢幕掃描線視覺層 -->
    <div class="crt-overlay"></div>

    <div class="main-container">
        <!-- 頂部資訊區：個人資料與頭像 -->
        <header class="header-section">
            <h1 class="header-title">★ PORTFOLIO SELECT ★</h1>
            
            <div class="avatar-container">
                <!-- 復古像素頭像預設圖 -->
                <svg class="avatar-img" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
                    <rect width="100" height="100" fill="#1b1233"/>
                    <!-- 像素臉孔 -->
                    <rect x="30" y="30" width="40" height="40" fill="#ffcd94"/>
                    <!-- 眼睛 -->
                    <rect x="38" y="42" width="6" height="10" fill="#000"/>
                    <rect x="56" y="42" width="6" height="10" fill="#000"/>
                    <rect x="40" y="44" width="2" height="3" fill="#fff"/>
                    <rect x="58" y="44" width="2" height="3" fill="#fff"/>
                    <!-- 昭和風格復古眼鏡框 -->
                    <rect x="34" y="38" width="14" height="16" fill="none" stroke="#ff0055" stroke-width="3"/>
                    <rect x="52" y="38" width="14" height="16" fill="none" stroke="#ff0055" stroke-width="3"/>
                    <rect x="48" y="44" width="4" height="3" fill="#ff0055"/>
                    <!-- 嘴巴微笑 -->
                    <rect x="42" y="58" width="16" height="4" fill="#d93838"/>
                    <!-- 帽子/頭髮 -->
                    <rect x="25" y="18" width="50" height="16" fill="#00ffcc"/>
                    <rect x="20" y="30" width="60" height="6" fill="#00ffcc"/>
                </svg>
                <span class="avatar-badge">LV.1</span>
            </div>

            <div class="player-name">
                SHOWA DEV
            </div>
            <div class="player-title">昭和開發者 / 網頁前端練習生</div>

            <!-- 進度條區塊 -->
            <div class="progress-box">
                <div class="progress-text">STAGE CLEAR: 2 / 16</div>
                <div class="progress-bar-bg">
                    <div class="progress-bar-fill"></div>
                </div>
            </div>
        </header>

        <!-- 16 個關卡按鈕網格區塊 -->
        <main class="stage-grid">
            
            <!-- STAGE 1: 已解鎖 -->
            <a href="w1/index.html" class="stage-card unlocked">
                <div class="stage-number">
                    <span>STAGE 01</span>
                    <span class="stage-status-tag">OPEN</span>
                </div>
                <div class="stage-title">Week 1 - 數位名片</div>
            </a>

            <!-- STAGE 2: 已解鎖 -->
            <a href="w2/index.html" class="stage-card unlocked">
                <div class="stage-number">
                    <span>STAGE 02</span>
                    <span class="stage-status-tag">OPEN</span>
                </div>
                <div class="stage-title">Week 2 - 今天吃甚麼?</div>
            </a>

            <!-- STAGE 3 ~ 16: 未解鎖灰色鎖定狀態 -->
            <!-- STAGE 03 -->
            <div class="stage-card locked" onclick="playLockFeedback(event)">
                <div class="stage-number">
                    <span>STAGE 03</span>
                    <span class="lock-icon">🔒</span>
                </div>
                <div class="stage-title">Week 3 - 尚未解鎖</div>
            </div>

            <!-- STAGE 04 -->
            <div class="stage-card locked" onclick="playLockFeedback(event)">
                <div class="stage-number">
                    <span>STAGE 04</span>
                    <span class="lock-icon">🔒</span>
                </div>
                <div class="stage-title">Week 4 - 尚未解鎖</div>
            </div>

            <!-- STAGE 05 -->
            <div class="stage-card locked" onclick="playLockFeedback(event)">
                <div class="stage-number">
                    <span>STAGE 05</span>
                    <span class="lock-icon">🔒</span>
                </div>
                <div class="stage-title">Week 5 - 尚未解鎖</div>
            </div>

            <!-- STAGE 06 -->
            <div class="stage-card locked" onclick="playLockFeedback(event)">
                <div class="stage-number">
                    <span>STAGE 06</span>
                    <span class="lock-icon">🔒</span>
                </div>
                <div class="stage-title">Week 6 - 尚未解鎖</div>
            </div>

            <!-- STAGE 07 -->
            <div class="stage-card locked" onclick="playLockFeedback(event)">
                <div class="stage-number">
                    <span>STAGE 07</span>
                    <span class="lock-icon">🔒</span>
                </div>
                <div class="stage-title">Week 7 - 尚未解鎖</div>
            </div>

            <!-- STAGE 08 -->
            <div class="stage-card locked" onclick="playLockFeedback(event)">
                <div class="stage-number">
                    <span>STAGE 08</span>
                    <span class="lock-icon">🔒</span>
                </div>
                <div class="stage-title">Week 8 - 尚未解鎖</div>
            </div>

            <!-- STAGE 09 -->
            <div class="stage-card locked" onclick="playLockFeedback(event)">
                <div class="stage-number">
                    <span>STAGE 09</span>
                    <span class="lock-icon">🔒</span>
                </div>
                <div class="stage-title">Week 9 - 尚未解鎖</div>
            </div>

            <!-- STAGE 10 -->
            <div class="stage-card locked" onclick="playLockFeedback(event)">
                <div class="stage-number">
                    <span>STAGE 10</span>
                    <span class="lock-icon">🔒</span>
                </div>
                <div class="stage-title">Week 10 - 尚未解鎖</div>
            </div>

            <!-- STAGE 11 -->
            <div class="stage-card locked" onclick="playLockFeedback(event)">
                <div class="stage-number">
                    <span>STAGE 11</span>
                    <span class="lock-icon">🔒</span>
                </div>
                <div class="stage-title">Week 11 - 尚未解鎖</div>
            </div>

            <!-- STAGE 12 -->
            <div class="stage-card locked" onclick="playLockFeedback(event)">
                <div class="stage-number">
                    <span>STAGE 12</span>
                    <span class="lock-icon">🔒</span>
                </div>
                <div class="stage-title">Week 12 - 尚未解鎖</div>
            </div>

            <!-- STAGE 13 -->
            <div class="stage-card locked" onclick="playLockFeedback(event)">
                <div class="stage-number">
                    <span>STAGE 13</span>
                    <span class="lock-icon">🔒</span>
                </div>
                <div class="stage-title">Week 13 - 尚未解鎖</div>
            </div>

            <!-- STAGE 14 -->
            <div class="stage-card locked" onclick="playLockFeedback(event)">
                <div class="stage-number">
                    <span>STAGE 14</span>
                    <span class="lock-icon">🔒</span>
                </div>
                <div class="stage-title">Week 14 - 尚未解鎖</div>
            </div>

            <!-- STAGE 15 -->
            <div class="stage-card locked" onclick="playLockFeedback(event)">
                <div class="stage-number">
                    <span>STAGE 15</span>
                    <span class="lock-icon">🔒</span>
                </div>
                <div class="stage-title">Week 15 - 尚未解鎖</div>
            </div>

            <!-- STAGE 16 -->
            <div class="stage-card locked" onclick="playLockFeedback(event)">
                <div class="stage-number">
                    <span>STAGE 16</span>
                    <span class="lock-icon">🔒</span>
                </div>
                <div class="stage-title">Week 16 - 最終關卡</div>
            </div>

        </main>

        <footer class="footer-note">
            INSERT COIN TO CONTINUE • 2026 WEB CLASS
        </footer>
    </div>

    <script>
        /* 未解鎖關卡點擊時的輕微 Shake 效果視覺反饋 */
        function playLockFeedback(e) {
            const card = e.currentTarget;
            card.style.borderColor = '#ff0055';
            setTimeout(() => {
                card.style.borderColor = '#38304d';
            }, 400);
        }
    </script>
</body>
</html>
