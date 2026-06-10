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
        }

        body {
            min-height: 100vh;
            background: radial-gradient(circle at 30% 20%, #0a0f2a, #030617);
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: "Segoe UI", "Microsoft YaHei", "PingFang SC", Georgia, serif;
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

        /* ---------- 书本世界：固定尺寸，居中 ---------- */
        .book-world {
            position: relative;
            width: 1200px;
            max-width: 90vw;
            height: 680px;
            max-height: 80vh;
            z-index: 10;
            /* 保持居中且不变形 */
            margin: auto;
        }

        /* 封面和内页的共用容器 — 绝对定位，确保位置完全重叠 */
        .book-slot {
            position: relative;
            width: 100%;
            height: 100%;
        }

        /* 合上的封面样式 */
        .closed-cover {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            transform-style: preserve-3d;
            transition: transform 0.6s cubic-bezier(0.2, 0.9, 0.4, 1.1), opacity 0.4s;
            cursor: pointer;
            border-radius: 18px;
            box-shadow: 0 30px 40px rgba(0, 0, 0, 0.5);
            z-index: 20;
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
            text-align: center;
            padding: 30px;
        }

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
            font-size: 3rem;
            font-weight: bold;
            color: #ffefcf;
            text-shadow: 0 4px 12px #b45a1a, 0 0 8px #ffc285;
            letter-spacing: 4px;
            margin-bottom: 20px;
        }

        .cover-sub {
            font-size: 1.3rem;
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

        /* 打开后的书本内页 — 同样绝对定位，与封面完全重叠 */
        .opened-book {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            opacity: 0;
            visibility: hidden;
            transition: opacity 0.4s ease;
            z-index: 15;
        }

        .opened-book.show-inner {
            opacity: 1;
            visibility: visible;
        }

        .book-inner {
            width: 100%;
            height: 100%;
            position: relative;
            transition: transform 0.2s ease-out;
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

        /* 滚动条美观 */
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
            font-size: 1.6rem;
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

        /* 底部导航 — 放在书本外部下方，不随书本移动 */
        .nav-controls {
            position: absolute;
            bottom: -70px;
            left: 0;
            width: 100%;
            display: flex;
            justify-content: center;
            gap: 24px;
            align-items: center;
            z-index: 25;
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

        /* 响应式：保证小屏幕下字体和布局舒适，书本不溢出 */
        @media (max-width: 900px) {
            .book-world {
                height: 600px;
            }
            .greeting-title {
                font-size: 1.3rem;
            }
            .message-text {
                font-size: 0.85rem;
            }
            .cover-title {
                font-size: 2.2rem;
            }
            .cover-sub {
                font-size: 1rem;
            }
        }

        @media (max-width: 700px) {
            .book-world {
                height: 550px;
            }
            .left-page, .right-page {
                padding: 14px 12px;
            }
            .greeting-title {
                font-size: 1.1rem;
            }
            .message-text {
                font-size: 0.75rem;
                padding: 10px;
            }
            .caption {
                font-size: 0.7rem;
            }
            .nav-btn {
                font-size: 0.9rem;
                padding: 4px 16px;
            }
        }

        /* 合上封面隐藏动画 */
        .closed-cover.hide-cover {
            transform: rotateY(-150deg) scale(0.9);
            opacity: 0;
            pointer-events: none;
            transition: transform 0.5s, opacity 0.4s;
        }
    </style>
</head>
<body>

    <div id="star-bg"></div>

    <div class="book-world">
        <!-- 使用同一个槽位，封面和内页绝对定位重叠 -->
        <div class="book-slot">
            <!-- 合上的书本封面 -->
            <div class="closed-cover" id="closedCover">
                <div class="cover-spine"></div>
                <div class="cover-front">
                    <div class="cover-title">✨ 半周年快乐 ✨</div>
                    <div class="cover-sub">致 独一无二的你</div>
                    <div class="open-hint">📖 点击打开这本书 📖</div>
                    <div style="position: absolute; bottom: 20px; font-size: 1rem; opacity: 0.7;">✧ 专属星空手账 ✧</div>
                </div>
            </div>

            <!-- 打开后的书本内页（初始隐藏） -->
            <div class="opened-book" id="openedBook">
                <div class="book-inner" id="book3d">
                    <div class="spread" id="spreadContainer">
                        <div class="left-page" id="leftPage"></div>
                        <div class="right-page" id="rightPage"></div>
                    </div>
                </div>
            </div>
        </div>
        <!-- 底部导航控件 (置于book-world内部，位于书本下方) -->
        <div class="nav-controls" id="navControls" style="display: none;">
            <button class="nav-btn" id="prevBtn">◀ 上一页</button>
            <div class="dot-group" id="dotGroup"></div>
            <button class="nav-btn" id="nextBtn">下一页 ▶</button>
        </div>
    </div>

    <script>
        // ======================= 1. 动态星星 =======================
        (function initStars() {
            const starContainer = document.getElementById('star-bg');
            const starCount = 260;
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

        // ======================= 2. 视频与内容数据配置 =======================
        // 为了方便放置大量视频，这里提供 pagesData 数组，每个对象代表一页（左页或右页）
        // 程序会自动两两配对成一个跨页。您只需要在这里按顺序添加您的视频页面。
        // 示例中包含6个跨页（12个视频），您可以根据需求复制添加至总共30个视频。
        const pagesData = [
            // 跨页1 左
            { title: "🎬 半周年特别纪念", message: "这是我们故事的开端，感谢遇见。", videoSrc: "videos/left1.mp4", caption: "✨ 初次相遇的星光" },
            // 跨页1 右
            { title: "💌 写给未来的你", message: "愿所有美好都奔向你，永远爱你。", videoSrc: "videos/right1.mp4", caption: "🌟 永恒的约定" },
            // 跨页2 左
            { title: "📸 珍藏片段", message: "那些一起笑的时光，像星星一样闪耀。", videoSrc: "videos/left2.mp4", caption: "💖 快乐时光" },
            // 跨页2 右
            { title: "🌙 晚安絮语", message: "每晚想起你，心里就亮起一颗星。", videoSrc: "videos/right2.mp4", caption: "🌠 伴你入梦" },
            // 跨页3 左
            { title: "🍃 春风与甜", message: "和你一起，平凡的日子也发光。", videoSrc: "videos/left3.mp4", caption: "🌸 温柔时刻" },
            // 跨页3 右
            { title: "🎁 专属礼物", message: "这份星空手账只为独一无二的你。", videoSrc: "videos/right3.mp4", caption: "✨ 半周年贺礼" },
            // 跨页4 左
            { title: "🌟 星海漫游", message: "想和你去宇宙漫游，收集所有浪漫。", videoSrc: "videos/left4.mp4", caption: "🚀 星辰大海" },
            // 跨页4 右
            { title: "📖 手账时光", message: "每一页都是我想对你说的悄悄话。", videoSrc: "videos/right4.mp4", caption: "💫 专属回忆" },
            // 跨页5 左
            { title: "🎵 旋律记忆", message: "耳机分你一半，心跳给你全部。", videoSrc: "videos/left5.mp4", caption: "🎧 我们的歌" },
            // 跨页5 右
            { title: "🌈 彩色未来", message: "未来所有颜色都想和你一起涂鸦。", videoSrc: "videos/right5.mp4", caption: "🎨 永远相伴" },
            // 跨页6 左
            { title: "🏆 半周年成就", message: "183天，每一天都感谢你在我身边。", videoSrc: "videos/left6.mp4", caption: "🏅 珍惜纪念" },
            // 跨页6 右
            { title: "🌌 无边星空", message: "你像星星一样点亮我的夜空，爱你。", videoSrc: "videos/right6.mp4", caption: "✨ 永恒星光" }
            // ========== 需要更多视频请在下方继续添加，每两个为一组跨页 ==========
            // 例如再添加一对:
            // { title: "🌻 温暖瞬间", message: "你的笑容是每天最好的礼物。", videoSrc: "videos/left7.mp4", caption: "☀️ 治愈时刻" },
            // { title: "🍀 幸运遇见", message: "遇见你是我最幸运的事。", videoSrc: "videos/right7.mp4", caption: "🍀 小确幸" }
        ];

        // 将页面数据两两分组生成跨页数组
        function buildSpreadsFromPages(pages) {
            const spreads = [];
            for (let i = 0; i < pages.length; i += 2) {
                if (i + 1 < pages.length) {
                    spreads.push({ left: pages[i], right: pages[i+1] });
                } else {
                    // 奇数时补一个占位
                    spreads.push({ left: pages[i], right: { title: "✨ 待续 ✨", message: "更多美好即将到来", videoSrc: "", caption: "敬请期待" } });
                }
            }
            return spreads;
        }

        let spreadsData = buildSpreadsFromPages(pagesData);
        console.log(`📖 已加载 ${spreadsData.length} 个跨页，共可容纳 ${spreadsData.length * 2} 个视频`);

        // 防止无数据
        if (spreadsData.length === 0) {
            spreadsData = [{ left: { title: "等待你的故事", message: "请在 pagesData 中添加视频数据", videoSrc: "", caption: "" }, right: { title: "❤️", message: "半周年快乐", videoSrc: "", caption: "" } }];
        }

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

        // 辅助：创建视频元素（含优雅降级）
        function createVideoElement(videoSrc, captionText) {
            const wrapper = document.createElement('div');
            wrapper.className = 'video-box';
            if (!videoSrc || videoSrc === "") {
                wrapper.style.background = "#2e2a1f";
                wrapper.style.display = "flex";
                wrapper.style.flexDirection = "column";
                wrapper.style.alignItems = "center";
                wrapper.style.justifyContent = "center";
                wrapper.innerHTML = `<div style="text-align:center; color:#f5e2b0; padding:20px;">✨ 星空映像 ✨<br><span style="font-size:12px;">🎬 视频即将加载</span><br><span style="font-size:11px;">请将视频放入对应路径</span></div>`;
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
                wrapper.innerHTML = `<div style="text-align:center; color:#f5e2b0; padding:20px;">✨ 星空影像 ✨<br><span style="font-size:12px;">🎬 视频未找到</span><br><span style="font-size:11px;">路径: ${videoSrc}</span></div>`;
                const cap = document.createElement('div');
                cap.className = 'caption';
                cap.innerText = captionText || '✨ 请检查视频路径 ✨';
                wrapper.appendChild(cap);
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
            const videoWidget = createVideoElement(pageData.videoSrc, pageData.caption);
            container.appendChild(videoWidget);
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
                dot.addEventListener('click', () => { if (i !== currentIndex) goToSpread(i); });
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

        // 打开书本：隐藏封面，显示内页和导航
        function openBook() {
            closedCover.classList.add('hide-cover');
            setTimeout(() => {
                openedBookDiv.classList.add('show-inner');
                navControls.style.display = 'flex';
                buildDots();
                renderCurrentSpread();
                // 绑定事件
                prevBtn.onclick = prevPage;
                nextBtn.onclick = nextPage;
                // 触摸滑动
                let touchStartX = 0;
                spreadEl.addEventListener('touchstart', (e) => {
                    touchStartX = e.changedTouches[0].screenX;
                }, { passive: true });
                spreadEl.addEventListener('touchend', (e) => {
                    const diff = e.changedTouches[0].screenX - touchStartX;
                    if (Math.abs(diff) > 50) diff > 0 ? prevPage() : nextPage();
                });
                // 键盘支持
                window.addEventListener('keydown', (e) => {
                    if (openedBookDiv.classList.contains('show-inner')) {
                        if (e.key === 'ArrowLeft') { e.preventDefault(); prevPage(); }
                        if (e.key === 'ArrowRight') { e.preventDefault(); nextPage(); }
                    }
                });
            }, 500);
        }

        closedCover.addEventListener('click', openBook);

        // 3D 倾斜效果（不影响位置）
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
    </script>
</body>
</html>
