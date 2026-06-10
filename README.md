<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>半周年礼物 · 星空之书</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            user-select: none; /* 避免拖动时误选，不影响文本复制 */
        }

        body {
            min-height: 100vh;
            background: radial-gradient(circle at 30% 20%, #0a0f2a, #030617);
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: "Segoe UI", "Microsoft YaHei", "PingFang SC", "Georgia", serif;
            overflow: hidden;
            position: relative;
            padding: 20px;
        }

        /* ---------- 动态闪烁星星 ---------- */
        .star {
            position: absolute;
            background-color: #ffffff;
            border-radius: 50%;
            box-shadow: 0 0 6px rgba(255, 255, 255, 0.8);
            animation: twinkle 2.5s infinite alternate ease-in-out;
            pointer-events: none;
            z-index: 0;
        }

        @keyframes twinkle {
            0% { opacity: 0.2; transform: scale(0.6); }
            100% { opacity: 1; transform: scale(1.2); }
        }

        /* ---------- 书本整体容器 ---------- */
        .book-world {
            position: relative;
            width: 1200px;
            max-width: 90vw;
            height: 680px;
            max-height: 80vh;
            z-index: 10;
            perspective: 2000px;
        }

        /* 封面样式 (合上的书) */
        .closed-cover {
            position: relative;
            width: 100%;
            height: 100%;
            transform-style: preserve-3d;
            transition: transform 0.8s cubic-bezier(0.2, 0.9, 0.4, 1.1), opacity 0.5s;
            cursor: pointer;
            border-radius: 18px;
            box-shadow: 0 30px 40px rgba(0, 0, 0, 0.5);
        }

        .cover-front {
            position: absolute;
            width: 100%;
            height: 100%;
            background: linear-gradient(145deg, #2c1a0c, #4d2e18);
            border-radius: 18px;
            box-shadow: inset 0 0 0 2px rgba(255, 215, 150, 0.6), 0 10px 25px rgba(0,0,0,0.3);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            backface-visibility: hidden;
            transform: rotateY(0deg);
            text-align: center;
            padding: 30px;
        }

        /* 封面装饰压纹 */
        .cover-front::before {
            content: "";
            position: absolute;
            top: 20px;
            left: 20px;
            right: 20px;
            bottom: 20px;
            border: 2px solid rgba(255, 210, 120, 0.4);
            border-radius: 12px;
            pointer-events: none;
        }

        .cover-title {
            font-size: 3.5rem;
            font-weight: bold;
            color: #ffefcf;
            text-shadow: 0 4px 12px #b45a1a, 0 0 8px #ffc285;
            letter-spacing: 4px;
            margin-bottom: 20px;
            font-family: 'Georgia', serif;
        }

        .cover-sub {
            font-size: 1.4rem;
            color: #fad98b;
            border-top: 2px solid #ffd58c;
            padding-top: 15px;
            width: 70%;
        }

        .open-hint {
            position: absolute;
            bottom: 40px;
            font-size: 1rem;
            color: #ffdd99;
            background: rgba(0,0,0,0.4);
            padding: 8px 20px;
            border-radius: 40px;
            backdrop-filter: blur(4px);
            animation: bounce 1.8s infinite;
        }

        @keyframes bounce {
            0%,100%{ transform: translateY(0); }
            50%{ transform: translateY(8px); }
        }

        /* 书脊装饰 */
        .cover-spine {
            position: absolute;
            left: -12px;
            top: 15px;
            width: 24px;
            height: calc(100% - 30px);
            background: #8b5a2b;
            border-radius: 6px 2px 2px 6px;
            box-shadow: inset -1px 0 4px rgba(0,0,0,0.3);
            z-index: 2;
        }

        /* 打开后的内页容器 (初始隐藏) */
        .opened-book {
            width: 100%;
            height: 100%;
            position: relative;
            display: none;
            opacity: 0;
            transition: opacity 0.5s;
            perspective: 2000px;
        }

        .book-inner {
            width: 100%;
            height: 100%;
            position: relative;
            transition: transform 0.3s ease-out;
            border-radius: 16px;
        }

        /* 跨页双屏 (不透明书页) */
        .spread {
            width: 100%;
            height: 100%;
            background: #fffcf0;
            border-radius: 16px;
            box-shadow: 0 25px 45px rgba(0, 0, 0, 0.5), inset 0 0 0 1px rgba(255, 245, 215, 0.9);
            display: flex;
            overflow: hidden;
            transition: opacity 0.25s ease, transform 0.3s ease;
        }

        .left-page, .right-page {
            flex: 1;
            padding: 22px 20px;
            display: flex;
            flex-direction: column;
            justify-content: flex-start;
            background: #fffcf0;
            overflow-y: auto;
            scrollbar-width: thin;
        }

        .left-page {
            border-right: 2px solid #e6dcc6;
        }
        .right-page {
            border-left: 2px solid #f1e8d4;
        }

        /* 滚动条 */
        .left-page::-webkit-scrollbar, .right-page::-webkit-scrollbar {
            width: 5px;
        }
        .left-page::-webkit-scrollbar-track {
            background: #f0e7d6;
            border-radius: 8px;
        }
        .left-page::-webkit-scrollbar-thumb {
            background: #c0a87a;
            border-radius: 8px;
        }

        /* 内页标题 */
        .greeting-title {
            font-size: 1.7rem;
            font-weight: 700;
            background: linear-gradient(135deg, #b85c1a, #7b3e10);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 12px;
            border-left: 5px solid #ffb347;
            padding-left: 16px;
        }

        .message-text {
            font-size: 0.95rem;
            line-height: 1.65;
            color: #2c3e2f;
            background: rgba(248, 240, 218, 0.7);
            padding: 14px 16px;
            border-radius: 28px;
            margin: 12px 0;
            font-weight: 500;
            box-shadow: inset 0 0 0 1px #fff9ef, 0 4px 10px rgba(0, 0, 0, 0.04);
        }

        .video-box {
            background: #1e1b14;
            border-radius: 20px;
            overflow: hidden;
            margin: 12px 0 8px;
            box-shadow: 0 10px 18px rgba(0, 0, 0, 0.2);
            aspect-ratio: 16 / 9;
            width: 100%;
        }
        .video-box video {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: block;
        }
        .caption {
            font-size: 0.8rem;
            text-align: center;
            margin-top: 6px;
            color: #a37242;
            font-weight: 500;
        }

        .deco-line {
            height: 2px;
            background: linear-gradient(90deg, #f7d98c, #c8a86b, #f7d98c);
            width: 60px;
            margin: 6px 0 8px;
        }

        /* 底部导航 */
        .nav-controls {
            position: absolute;
            bottom: -70px;
            left: 0;
            width: 100%;
            display: flex;
            justify-content: center;
            gap: 24px;
            align-items: center;
            z-index: 20;
        }
        .nav-btn {
            background: rgba(25, 20, 35, 0.8);
            backdrop-filter: blur(8px);
            border: 1px solid rgba(255, 215, 150, 0.7);
            color: #ffefcf;
            font-size: 1.2rem;
            padding: 6px 24px;
            border-radius: 48px;
            cursor: pointer;
            transition: all 0.2s;
            font-weight: bold;
        }
        .nav-btn:hover {
            background: #b87c3e;
            color: white;
            transform: scale(1.02);
        }
        .dot-group {
            display: flex;
            gap: 12px;
            align-items: center;
            background: rgba(0,0,0,0.3);
            backdrop-filter: blur(4px);
            padding: 6px 20px;
            border-radius: 60px;
        }
        .dot {
            width: 10px;
            height: 10px;
            border-radius: 50%;
            background: #b9a077;
            transition: all 0.2s;
            cursor: pointer;
        }
        .dot.active {
            background: #ffc485;
            transform: scale(1.3);
            box-shadow: 0 0 8px #ffbc6e;
        }

        /* 响应式 */
        @media (max-width: 800px) {
            .book-world { height: 580px; }
            .left-page, .right-page { padding: 16px 12px; }
            .greeting-title { font-size: 1.2rem; }
            .message-text { font-size: 0.8rem; }
            .cover-title { font-size: 2.2rem; }
            .cover-sub { font-size: 1rem; }
        }

        /* 打开书本动画 */
        .closed-cover.hide-cover {
            transform: rotateY(-150deg) scale(0.9);
            opacity: 0;
            pointer-events: none;
        }
        .opened-book.show-inner {
            display: block;
            opacity: 1;
        }
    </style>
</head>
<body>

    <!-- 动态星空背景容器 -->
    <div id="star-bg"></div>

    <div class="book-world">
        <!-- 合上的书本封面 -->
        <div class="closed-cover" id="closedCover">
            <div class="cover-spine"></div>
            <div class="cover-front">
                <div class="cover-title">✨ 半周年快乐 ✨</div>
                <div class="cover-sub">致 独一无二的你</div>
                <div class="open-hint">📖 点击打开这本书 📖</div>
                <!-- 小巧思：一个金色小星星环绕 -->
                <div style="position: absolute; bottom: 20px; font-size: 1.2rem; opacity: 0.7;">✧ 专属星空手账 ✧</div>
            </div>
        </div>

        <!-- 打开后的书本内页 -->
        <div class="opened-book" id="openedBook">
            <div class="book-inner" id="book3d">
                <div class="spread" id="spreadContainer">
                    <div class="left-page" id="leftPage"></div>
                    <div class="right-page" id="rightPage"></div>
                </div>
            </div>
            <!-- 底部翻页控件 (初始隐藏，打开后显示) -->
            <div class="nav-controls" id="navControls" style="display: none;">
                <button class="nav-btn" id="prevBtn">◀ 上一页</button>
                <div class="dot-group" id="dotGroup"></div>
                <button class="nav-btn" id="nextBtn">下一页 ▶</button>
            </div>
        </div>
    </div>

    <script>
        // ======================= 1. 生成动态闪烁星星 =======================
        (function initStars() {
            const starContainer = document.getElementById('star-bg');
            const starCount = 260;  // 足够繁星
            for (let i = 0; i < starCount; i++) {
                const star = document.createElement('div');
                star.classList.add('star');
                const size = Math.random() * 4 + 1.2;
                star.style.width = size + 'px';
                star.style.height = size + 'px';
                star.style.left = Math.random() * 100 + '%';
                star.style.top = Math.random() * 100 + '%';
                const duration = Math.random() * 3 + 1.5;
                star.style.animationDuration = duration + 's';
                star.style.animationDelay = Math.random() * 4 + 's';
                star.style.opacity = Math.random() * 0.8 + 0.2;
                starContainer.appendChild(star);
            }
        })();

        // ======================= 2. 视频与内容数据配置区 =======================
        // 为了方便放置25~30个视频，这里定义全局跨页数据。
        // 每个跨页包含左页和右页，每一页包含: title(标题), message(想说的话), videoSrc(视频路径), caption(视频下方小字)
        // 您可以根据实际视频数量轻松添加或删除。 下面的示例演示了6个跨页(12个视频)，您可以继续复制模式扩展至15个跨页（30个视频）
        // 💡 使用技巧：将视频文件放到项目的 "videos" 文件夹中，然后按下面格式填写路径。
        
        // 为了方便修改，此处构造一个函数来生成跨页数组。您只需要在下方 allVideos 中按顺序填入每个页面的信息(左页+右页成对出现)
        // 更直观: 定义视频项列表, 每两项组成一个跨页。
        
        // --------------------------------------------------------------
        // ************* 请在这里填入您的视频和文字 *************
        // 每个对象代表一个“页面”(左页或右页)，程序会两两配对成一个跨页。
        // 您需要保证总页面数为偶数，即视频个数为偶数（每个跨页左右各一个视频）。
        // 如果您有30个视频，那就放30个对象，系统自动每两个组成一跨页。
        const pagesData = [
            // 跨页1 (左)
            { title: "🎬 半周年特别纪念", message: "这是我们故事的开端，感谢遇见。", videoSrc: "videos/left1.mp4", caption: "✨ 初次相遇的星光" },
            // 跨页1 (右)
            { title: "💌 写给未来的你", message: "愿所有美好都奔向你，永远爱你。", videoSrc: "videos/right1.mp4", caption: "🌟 永恒的约定" },
            
            // 跨页2 (左)
            { title: "📸 珍藏片段", message: "那些一起笑的时光，像星星一样闪耀。", videoSrc: "videos/left2.mp4", caption: "💖 快乐时光" },
            // 跨页2 (右)
            { title: "🌙 晚安絮语", message: "每晚想起你，心里就亮起一颗星。", videoSrc: "videos/right2.mp4", caption: "🌠 伴你入梦" },
            
            // 跨页3 (左)
            { title: "🍃 春风与甜", message: "和你一起，平凡的日子也发光。", videoSrc: "videos/left3.mp4", caption: "🌸 温柔时刻" },
            // 跨页3 (右)
            { title: "🎁 专属礼物", message: "这份星空手账只为独一无二的你。", videoSrc: "videos/right3.mp4", caption: "✨ 半周年贺礼" },
            
            // 跨页4 (左)  继续添加 ———— 你可以按这个模式往下复制到30个视频
            { title: "🌟 星海漫游", message: "想和你去宇宙漫游，收集所有浪漫。", videoSrc: "videos/left4.mp4", caption: "🚀 星辰大海" },
            { title: "📖 手账时光", message: "每一页都是我想对你说的悄悄话。", videoSrc: "videos/right4.mp4", caption: "💫 专属回忆" },
            
            // 跨页5 (左)
            { title: "🎵 旋律记忆", message: "耳机分你一半，心跳给你全部。", videoSrc: "videos/left5.mp4", caption: "🎧 我们的歌" },
            { title: "🌈 彩色未来", message: "未来所有颜色都想和你一起涂鸦。", videoSrc: "videos/right5.mp4", caption: "🎨 永远相伴" },
            
            // 跨页6 (左) —— 共12个视频，如果需要更多，继续复制下方模式。
            { title: "🏆 半周年成就", message: "183天，每一天都感谢你在我身边。", videoSrc: "videos/left6.mp4", caption: "🏅 珍惜纪念" },
            { title: "🌌 无边星空", message: "你像星星一样点亮我的夜空，爱你。", videoSrc: "videos/right6.mp4", caption: "✨ 永恒星光" }
            
            // ========== 如果你有更多视频（直到30个），请继续添加 ==========
            // 例如下面再添加一对:
            // { title: "🌻 温暖瞬间", message: "你的笑容是每天最好的礼物。", videoSrc: "videos/left7.mp4", caption: "☀️ 治愈时刻" },
            // { title: "🍀 幸运遇见", message: "遇见你是我最幸运的事。", videoSrc: "videos/right7.mp4", caption: "🍀 小确幸" }
            // ... 一直添加到总共30个页面(15个跨页)
        ];
        
        // 自动将页面数据两两分组生成跨页数组 spreadsData
        function buildSpreadsFromPages(pages) {
            const spreads = [];
            for (let i = 0; i < pages.length; i += 2) {
                if (i + 1 < pages.length) {
                    spreads.push({
                        left: pages[i],
                        right: pages[i+1]
                    });
                } else {
                    // 如果总数为奇数，最后一个单独左侧，右侧放一个占位提示（理论上不会发生，用户保持偶数个视频）
                    spreads.push({
                        left: pages[i],
                        right: { title: "✨ 待续 ✨", message: "更多美好即将到来", videoSrc: "", caption: "敬请期待" }
                    });
                }
            }
            return spreads;
        }
        
        // 生成跨页数据 (支持25~30个视频，只要pagesData里有偶数个对象)
        let spreadsData = buildSpreadsFromPages(pagesData);
        
        // 如果用户视频数量不足，可以自动补充示例跨页达到至少 12~15跨页？但用户可根据自己实际修改pagesData即可。
        // 为了方便演示，若用户没有修改pagesData且希望展示更多跨页样式，我们不做额外强制，由用户自行在pagesData中添加。
        // 提示控制台
        console.log(`📖 已加载跨页数量: ${spreadsData.length} (每个跨页左右各一视频，共可容纳 ${spreadsData.length * 2} 个视频)`);
        
        // --------------------- 全局变量 ---------------------
        let currentIndex = 0;
        const totalSpreads = spreadsData.length;
        const leftContainer = document.getElementById('leftPage');
        const rightContainer = document.getElementById('rightPage');
        const prevBtn = document.getElementById('prevBtn');
        const nextBtn = document.getElementById('nextBtn');
        const dotGroup = document.getElementById('dotGroup');
        const spreadEl = document.getElementById('spreadContainer');
        const closedCover = document.getElementById('closedCover');
        const openedBookDiv = document.getElementById('openedBook');
        const navControls = document.getElementById('navControls');
        
        // 辅助: 创建视频元素（含优雅降级）
        function createVideoElement(videoSrc, captionText) {
            const wrapper = document.createElement('div');
            wrapper.className = 'video-box';
            
            if (!videoSrc || videoSrc === "") {
                // 没有视频时显示占位
                wrapper.style.background = "#2e2a1f";
                wrapper.style.display = "flex";
                wrapper.style.flexDirection = "column";
                wrapper.style.alignItems = "center";
                wrapper.style.justifyContent = "center";
                wrapper.innerHTML = `
                    <div style="text-align:center; color:#f5e2b0; padding:20px;">
                        ✨ 星空映像 ✨<br>
                        <span style="font-size:12px;">🎬 视频即将加载</span><br>
                        <span style="font-size:11px;">请将视频放入对应路径</span>
                    </div>
                `;
                const captionDiv = document.createElement('div');
                captionDiv.className = 'caption';
                captionDiv.innerText = captionText || '♡ 珍藏片段 ♡';
                wrapper.appendChild(captionDiv);
                return wrapper;
            }
            
            const video = document.createElement('video');
            video.controls = true;
            video.preload = "metadata";
            video.playsInline = true;
            const source = document.createElement('source');
            source.src = videoSrc;
            source.type = 'video/mp4';
            video.appendChild(source);
            
            video.onerror = () => {
                wrapper.style.background = "#2e2a1f";
                wrapper.style.display = "flex";
                wrapper.style.flexDirection = "column";
                wrapper.style.alignItems = "center";
                wrapper.style.justifyContent = "center";
                wrapper.innerHTML = `
                    <div style="text-align:center; color:#f5e2b0; padding:20px;">
                        ✨ 星空影像 ✨<br>
                        <span style="font-size:12px;">🎬 视频未找到</span><br>
                        <span style="font-size:11px;">路径: ${videoSrc}</span>
                    </div>
                `;
                const cap = document.createElement('div');
                cap.className = 'caption';
                cap.innerText = captionText || '✨ 请检查视频路径 ✨';
                wrapper.appendChild(cap);
                return;
            };
            
            wrapper.appendChild(video);
            const captionDiv = document.createElement('div');
            captionDiv.className = 'caption';
            captionDiv.innerText = captionText || '♡ 珍藏片段 ♡';
            wrapper.appendChild(captionDiv);
            return wrapper;
        }
        
        function renderPageContent(container, pageData) {
            container.innerHTML = '';
            if (!pageData) return;
            const title = document.createElement('h2');
            title.className = 'greeting-title';
            title.innerText = pageData.title || '✨ 珍藏时刻 ✨';
            container.appendChild(title);
            
            const deco = document.createElement('div');
            deco.className = 'deco-line';
            container.appendChild(deco);
            
            const msgBox = document.createElement('div');
            msgBox.className = 'message-text';
            msgBox.innerText = pageData.message || '愿所有星光奔向你。';
            container.appendChild(msgBox);
            
            // 视频区域
            if (pageData.videoSrc) {
                const videoWidget = createVideoElement(pageData.videoSrc, pageData.caption);
                container.appendChild(videoWidget);
            } else {
                const placeholder = document.createElement('div');
                placeholder.style.background = "#efe2cc";
                placeholder.style.borderRadius = "28px";
                placeholder.style.padding = "24px 12px";
                placeholder.style.textAlign = "center";
                placeholder.style.margin = "15px 0";
                placeholder.innerHTML = '⭐ 星空映像馆 ⭐<br><span style="font-size:12px;">浪漫影像即将呈现</span>';
                placeholder.style.color = "#956e3e";
                container.appendChild(placeholder);
                if (pageData.caption) {
                    const cap = document.createElement('div');
                    cap.className = 'caption';
                    cap.innerText = pageData.caption;
                    container.appendChild(cap);
                }
            }
            
            const starDust = document.createElement('div');
            starDust.style.textAlign = 'center';
            starDust.style.marginTop = '14px';
            starDust.style.fontSize = '16px';
            starDust.style.letterSpacing = '4px';
            starDust.style.opacity = '0.5';
            starDust.innerHTML = '✧  ⋆  ✦  ⋆  ✧';
            container.appendChild(starDust);
        }
        
        function renderCurrentSpread() {
            const data = spreadsData[currentIndex];
            if (!data) return;
            renderPageContent(leftContainer, data.left);
            renderPageContent(rightContainer, data.right);
            updateDots();
        }
        
        function updateDots() {
            const dots = document.querySelectorAll('.dot');
            dots.forEach((dot, idx) => {
                if (idx === currentIndex) dot.classList.add('active');
                else dot.classList.remove('active');
            });
        }
        
        function buildDots() {
            dotGroup.innerHTML = '';
            for (let i = 0; i < totalSpreads; i++) {
                const dot = document.createElement('div');
                dot.classList.add('dot');
                if (i === currentIndex) dot.classList.add('active');
                dot.addEventListener('click', () => {
                    if (i !== currentIndex) goToSpread(i);
                });
                dotGroup.appendChild(dot);
            }
        }
        
        function goToSpread(newIndex) {
            if (newIndex === currentIndex) return;
            if (newIndex < 0 || newIndex >= totalSpreads) return;
            if (spreadEl) {
                spreadEl.style.transition = 'opacity 0.2s ease, transform 0.25s';
                spreadEl.style.opacity = '0';
                spreadEl.style.transform = 'scale(0.98)';
            }
            setTimeout(() => {
                currentIndex = newIndex;
                renderCurrentSpread();
                if (spreadEl) {
                    spreadEl.style.opacity = '1';
                    spreadEl.style.transform = 'scale(1)';
                    setTimeout(() => { if(spreadEl) spreadEl.style.transition = ''; }, 280);
                }
                updateDots();
            }, 180);
        }
        
        function nextPage() {
            if (currentIndex < totalSpreads - 1) goToSpread(currentIndex + 1);
            else if (spreadEl) {
                spreadEl.style.transform = 'translateX(-5px)';
                setTimeout(() => { if(spreadEl) spreadEl.style.transform = ''; }, 200);
            }
        }
        
        function prevPage() {
            if (currentIndex > 0) goToSpread(currentIndex - 1);
            else if (spreadEl) {
                spreadEl.style.transform = 'translateX(5px)';
                setTimeout(() => { if(spreadEl) spreadEl.style.transform = ''; }, 200);
            }
        }
        
        // 打开书本动画
        function openBook() {
            closedCover.classList.add('hide-cover');
            setTimeout(() => {
                openedBookDiv.classList.add('show-inner');
                navControls.style.display = 'flex';
                // 初始化内页
                buildDots();
                renderCurrentSpread();
                // 绑定事件
                prevBtn.onclick = prevPage;
                nextBtn.onclick = nextPage;
                // 触摸滑动
                spreadEl.addEventListener('touchstart', (e) => {
                    touchStartX = e.changedTouches[0].screenX;
                }, { passive: true });
                spreadEl.addEventListener('touchend', (e) => {
                    const diff = e.changedTouches[0].screenX - touchStartX;
                    if (Math.abs(diff) > 50) diff > 0 ? prevPage() : nextPage();
                });
                // 键盘
                window.addEventListener('keydown', (e) => {
                    if (openedBookDiv.classList.contains('show-inner')) {
                        if (e.key === 'ArrowLeft') { e.preventDefault(); prevPage(); }
                        if (e.key === 'ArrowRight') { e.preventDefault(); nextPage(); }
                    }
                });
            }, 500);
        }
        
        let touchStartX = 0;
        closedCover.addEventListener('click', openBook);
        
        // 书本3D倾斜效果(内页)
        const book3d = document.getElementById('book3d');
        if (book3d) {
            book3d.addEventListener('mousemove', (e) => {
                if (!openedBookDiv.classList.contains('show-inner')) return;
                const rect = book3d.getBoundingClientRect();
                const x = (e.clientX - rect.left) / rect.width - 0.5;
                const y = (e.clientY - rect.top) / rect.height - 0.5;
                book3d.style.transform = `perspective(1800px) rotateX(${y * 1}deg) rotateY(${x * 2}deg)`;
            });
            book3d.addEventListener('mouseleave', () => { book3d.style.transform = ''; });
        }
        
        // 如果跨页数据为空则给个默认
        if (totalSpreads === 0) {
            spreadsData = [{ left: { title: "等待你的故事", message: "请在 pagesData 中添加视频数据", videoSrc: "", caption: "" }, right: { title: "❤️", message: "半周年快乐", videoSrc: "", caption: "" } }];
        }
    </script>
</body>
</html>
