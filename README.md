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
            font-family
