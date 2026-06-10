<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>半周年礼物 · 星空手账 | 珍藏视频集</title>
    <style>
        /* 全局重置 & 基础 */
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
            font-family: "Segoe UI", "Microsoft YaHei", "PingFang SC", "Helvetica Neue", sans-serif;
            overflow: hidden;
            position: relative;
            padding: 20px;
        }

        /* ---------- 动态闪烁星星背景 (增强闪烁感) ---------- */
        .star {
            position: absolute;
            background-color: #ffffff;
            border-radius: 50%;
            box-shadow: 0 0 6px rgba(255, 255, 255, 0.9);
            animation: starTwinkle 2.2s infinite alternate ease-in-out;
            pointer-events: none;
            z-index: 0;
        }

        @keyframes starTwinkle {
            0% { opacity: 0.15; transform: scale(0.6); box-shadow: 0 0 2px rgba(255,255,200,0.3);}
            100% { opacity: 1; transform: scale(1.3); box-shadow: 0 0 12px rgba(255,240,150,0.9);}
        }

        /* ---------- 横板书本容器 (稳定位置不变) ---------- */
        .book-wrapper {
            perspective: 1800px;
            width: 1200px;
            max-width: 90vw;
            height: 680px;
            max-height: 80vh;
            position: relative;
            z-index: 10;
            margin: 0 auto;
        }

        /* 书本主体 */
        .book {
            width: 100%;
            height: 100%;
            position: relative;
            transition: transform 0.2s ease-out;
            border-radius: 16px;
        }

        /* 跨页 (左右双页) — 不透明书页质感 */
        .spread {
            width: 100%;
            height: 100%;
            background: #fffcf0;
            border-radius: 16px;
            box-shadow: 0 25px 45px rgba(0, 0, 0, 0.4), inset 0 0 0 1px rgba(255, 245, 215, 0.8);
            display: flex;
            overflow: hidden;
            transition: opacity 0.25s ease, transform 0.3s ease;
        }

        /* 左页 & 右页 (各占一半) */
        .left-page, .right-page {
            flex: 1;
            padding: 22px 24px;
            display: flex;
            flex-direction: column;
            justify-content: flex-start;
            background: #fffcf0;
            overflow-y: auto;
            scrollbar-width: thin;
        }

        /* 书缝装饰 */
        .left-page {
            border-right: 2px solid #e6dcc6;
            box-shadow: inset -2px 0 5px rgba(0, 0, 0, 0.02);
        }
        .right-page {
            border-left: 2px solid #f1e8d4;
        }

        /* 自定义滚动条 */
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

        /* 标题样式 */
        .greeting-title {
            font-size: 1.6rem;
            font-weight: 700;
            background: linear-gradient(135deg, #b85c1a, #7b3e10);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 12px;
            letter-spacing: 1px;
            border-left: 5px solid #ffb347;
            padding-left: 18px;
        }

        /* 文字寄语框 */
        .message-text {
            font-size: 0.93rem;
            line-height: 1.65;
            color: #2c3e2f;
            background: rgba(248, 240, 218, 0.7);
            padding: 14px 18px;
            border-radius: 28px;
            margin: 12px 0;
            font-weight: 500;
            box-shadow: inset 0 0 0 1px #fff9ef, 0 6px 14px rgba(0, 0, 0, 0.04);
        }

        /* 视频容器 */
        .video-box {
            background: #1e1b14;
            border-radius: 20px;
            overflow: hidden;
            margin: 12px 0 6px 0;
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
            letter-spacing: 0.5px;
        }

        /* 装饰细线 */
        .deco-line {
            height: 2px;
            background: linear-gradient(90deg, #f7d98c, #c8a86b, #f7d98c);
            width: 60px;
            margin: 6px 0 8px;
        }

        /* 底部导航栏 */
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
            background: rgba(25, 20, 35, 0.85);
            backdrop-filter: blur(8px);
            border: 1px solid rgba(255, 215, 150, 0.7);
            color: #ffefcf;
            font-size: 1.2rem;
            padding: 8px 26px;
            border-radius: 48px;
            cursor: pointer;
            transition: all 0.2s;
            font-weight: bold;
            letter-spacing: 2px;
            font-family: inherit;
        }

        .nav-btn:hover {
            background: #b87c3e;
            color: white;
            border-color: #ffe0a3;
            transform: scale(1.02);
        }

        .dot-group {
            display: flex;
            gap: 12px;
            align-items: center;
            background: rgba(0, 0, 0, 0.35);
            backdrop-filter: blur(4px);
            padding: 6px 22px;
            border-radius: 60px;
        }

        .dot {
            width: 10px;
            height: 10px;
            border-radius: 50%;
            background: #d4bc8c;
            transition: all 0.2s;
            cursor: pointer;
        }

        .dot.active {
            background: #ffc485;
            transform: scale(1.4);
            box-shadow: 0 0 10px #ffbc6e;
        }

        /* 书脊装饰 */
        .book-spine {
            position: absolute;
            left: -8px;
            top: 12px;
            width: 16px;
            height: calc(100% - 24px);
            background: #cfa668;
            border-radius: 6px 2px 2px 6px;
            z-index: 5;
            box-shadow: inset -1px 0 4px rgba(0,0,0,0.2);
        }

        /* 手机适配 (确保位置不偏移) */
        @media (max-width: 800px) {
            .book-wrapper {
                height: 580px;
            }
            .left-page, .right-page {
                padding: 14px 12px;
            }
            .greeting-title {
                font-size: 1.2rem;
            }
            .message-text {
                font-size: 0.8rem;
                padding: 10px;
            }
            .caption {
                font-size: 0.65rem;
            }
            .nav-btn {
                font-size: 0.9rem;
                padding: 5px 18px;
            }
        }

        @media (max-width: 600px) {
            .greeting-title {
                font-size: 1rem;
            }
            .message-text {
                font-size: 0.7rem;
            }
        }
    </style>
</head>
<body>

    <!-- 动态星星背景容器 -->
    <div id="star-bg"></div>

    <div class="book-wrapper">
        <div class="book-spine"></div>
        <div class="book" id="book3d">
            <div class="spread" id="spreadContainer">
                <!-- 左页 -->
                <div class="left-page" id="leftPage"></div>
                <!-- 右页 -->
                <div class="right-page" id="rightPage"></div>
            </div>
        </div>
        
        <!-- 底部翻页控件 -->
        <div class="nav-controls">
            <button class="nav-btn" id="prevBtn">◀ 上一页</button>
            <div class="dot-group" id="dotGroup"></div>
            <button class="nav-btn" id="nextBtn">下一页 ▶</button>
        </div>
    </div>

    <script>
        // ======================== 1. 生成动态闪烁星星 (增强版) ========================
        (function initStars() {
            const starContainer = document.getElementById('star-bg');
            const starCount = 280;  // 更多星星，氛围更浓
            for (let i = 0; i < starCount; i++) {
                const star = document.createElement('div');
                star.classList.add('star');
                const size = Math.random() * 4 + 1.2;
                star.style.width = size + 'px';
                star.style.height = size + 'px';
                star.style.left = Math.random() * 100 + '%';
                star.style.top = Math.random() * 100 + '%';
                // 随机动画时长，更自然
                const duration = Math.random() * 2.5 + 1.2;
                star.style.animationDuration = duration + 's';
                star.style.animationDelay = Math.random() * 5 + 's';
                star.style.opacity = Math.random() * 0.6 + 0.3;
                starContainer.appendChild(star);
            }
        })();

        // ======================== 2. 扩充数据 (支持20个视频, 即10个跨页) ========================
        // 为了方便用户放置20个视频，这里构建10个跨页 (每跨页左右各一个视频，共20个视频位)
        // 您只需要按照格式替换 videoSrc 路径和文字即可，非常清晰。
        // 所有视频路径建议存放在 "videos/" 文件夹下，命名如 video01.mp4 ... video20.mp4
        // 如果不修改路径，会显示占位提示，不报错。
        
        const spreadsData = [
            { // 跨页1
                left: { title: "✨ 半周年序章", message: "我们的故事，从星光开始。", videoSrc: "videos/video_01.mp4", caption: "初遇时分" },
                right: { title: "💝 心动印记", message: "第一次心动，像流星划过夜空。", videoSrc: "videos/video_02.mp4", caption: "珍藏瞬间" }
            },
            { // 跨页2
                left: { title: "📸 欢笑时光", message: "你笑起来，世界都亮了。", videoSrc: "videos/video_03.mp4", caption: "灿烂笑容" },
                right: { title: "🌙 晚安电台", message: "每晚睡前，都会想起你温柔的声音。", videoSrc: "videos/video_04.mp4", caption: "伴你入梦" }
            },
            { // 跨页3
                left: { title: "🍃 春日漫步", message: "一起走过的路，开满鲜花。", videoSrc: "videos/video_05.mp4", caption: "踏青记忆" },
                right: { title: "🎂 特别的日子", message: "每一个纪念日，都想和你庆祝。", videoSrc: "videos/video_06.mp4", caption: "甜蜜庆典" }
            },
            { // 跨页4
                left: { title: "🎵 我们的旋律", message: "耳机分你一半，心跳连成和弦。", videoSrc: "videos/video_07.mp4", caption: "专属BGM" },
                right: { title: "🌈 彩虹约定", message: "风雨之后，一起看最美彩虹。", videoSrc: "videos/video_08.mp4", caption: "雨后晴空" }
            },
            { // 跨页5
                left: { title: "🌟 星语心愿", message: "每一颗星星都藏着一句我爱你。", videoSrc: "videos/video_09.mp4", caption: "星河告白" },
                right: { title: "🎁 惊喜礼物", message: "想把全世界的美好都送给你。", videoSrc: "videos/video_10.mp4", caption: "心意包裹" }
            },
            { // 跨页6  (第11、12个视频)
                left: { title: "📖 旅行日记", message: "想和你一起丈量世界的每一寸浪漫。", videoSrc: "videos/video_11.mp4", caption: "在路上" },
                right: { title: "☕ 日常温暖", message: "平凡的日子，有你就不平凡。", videoSrc: "videos/video_12.mp4", caption: "小确幸" }
            },
            { // 跨页7  (第13、14)
                left: { title: "🎨 涂鸦未来", message: "一起描绘属于我们的明天。", videoSrc: "videos/video_13.mp4", caption: "梦想蓝图" },
                right: { title: "🏆 成长纪念", message: "见证彼此的进步与蜕变。", videoSrc: "videos/video_14.mp4", caption: "蜕变时刻" }
            },
            { // 跨页8 (第15、16)
                left: { title: "🌊 夏日海边", message: "海风、夕阳，和你的侧脸。", videoSrc: "videos/video_15.mp4", caption: "浪花记忆" },
                right: { title: "❄️ 冬日暖阳", message: "寒冷的日子，你是我最暖的拥抱。", videoSrc: "videos/video_16.mp4", caption: "温暖相依" }
            },
            { // 跨页9 (第17、18)
                left: { title: "🕯️ 烛光私语", message: "安静的夜晚，听你诉说心事。", videoSrc: "videos/video_17.mp4", caption: "深谈时刻" },
                right: { title: "🌌 银河约定", message: "想和你一起，数遍漫天星辰。", videoSrc: "videos/video_18.mp4", caption: "星空诺言" }
            },
            { // 跨页10 (第19、20个视频)
                left: { title: "💖 半周年快乐", message: "183天，感谢有你。未来请多指教。", videoSrc: "videos/video_19.mp4", caption: "周年献礼" },
                right: { title: "✨ 永无止境", message: "我们的故事，未完待续……", videoSrc: "videos/video_20.mp4", caption: "to be continued" }
            }
        ];

        // 你可以轻松扩展更多跨页：只需继续向 spreadsData 中添加对象，每加一个对象代表一个跨页（左右各一视频）
        // 例如再加第11跨页: { left: {...}, right: {...} }
        
        // ------------------ 全局变量 ------------------
        let currentIndex = 0;          
        const totalSpreads = spreadsData.length;
        const leftContainer = document.getElementById('leftPage');
        const rightContainer = document.getElementById('rightPage');
        const prevBtn = document.getElementById('prevBtn');
        const nextBtn = document.getElementById('nextBtn');
        const dotGroup = document.getElementById('dotGroup');
        const spreadEl = document.getElementById('spreadContainer');

        // 优雅创建视频元素 (加载失败显示温馨占位)
        function createVideoElement(videoSrc, captionText) {
            const wrapper = document.createElement('div');
            wrapper.className = 'video-box';
            
            const video = document.createElement('video');
            video.controls = true;
            video.preload = "metadata";
            video.playsInline = true;
            
            const source = document.createElement('source');
            source.src = videoSrc;
            source.type = 'video/mp4';
            video.appendChild(source);
            
            // 加载失败时占位符，不会破坏布局
            video.onerror = () => {
                wrapper.style.background = "#2e2a1f";
                wrapper.style.display = "flex";
                wrapper.style.flexDirection = "column";
                wrapper.style.alignItems = "center";
                wrapper.style.justifyContent = "center";
                wrapper.style.borderRadius = "20px";
                wrapper.innerHTML = `
                    <div style="text-align:center; color:#f5e2b0; padding:20px;">
                        ✨ 星空影像 ✨<br>
                        <span style="font-size:12px;">🎬 等待你的视频</span><br>
                        <span style="font-size:11px;">请将视频放入 videos/ 目录</span>
                    </div>
                `;
                video.style.display = 'none';
                return;
            };
            
            wrapper.appendChild(video);
            const captionDiv = document.createElement('div');
            captionDiv.className = 'caption';
            captionDiv.innerText = captionText || '♡ 珍藏片段 ♡';
            wrapper.appendChild(captionDiv);
            return wrapper;
        }

        // 渲染单个页面内容 (左页或右页)
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
            
            // 视频区域 (视频路径存在则尝试加载，否则占位)
            if (pageData.videoSrc) {
                const videoWidget = createVideoElement(pageData.videoSrc, pageData.caption || '♡ 你的故事 ♡');
                container.appendChild(videoWidget);
            } else {
                const placeholder = document.createElement('div');
                placeholder.style.background = "#efe2cc";
                placeholder.style.borderRadius = "28px";
                placeholder.style.padding = "28px 12px";
                placeholder.style.textAlign = "center";
                placeholder.style.margin = "20px 0";
                placeholder.innerHTML = '⭐ 星空映像馆 ⭐<br><span style="font-size:12px;">浪漫影像即将呈现</span>';
                placeholder.style.color = "#956e3e";
                placeholder.style.fontWeight = "500";
                container.appendChild(placeholder);
                if (pageData.caption) {
                    const cap = document.createElement('div');
                    cap.className = 'caption';
                    cap.innerText = pageData.caption;
                    container.appendChild(cap);
                }
            }
            
            // 星尘装饰
            const starDust = document.createElement('div');
            starDust.style.textAlign = 'center';
            starDust.style.marginTop = '16px';
            starDust.style.fontSize = '16px';
            starDust.style.letterSpacing = '4px';
            starDust.style.opacity = '0.5';
            starDust.innerHTML = '✧  ⋆  ✦  ⋆  ✧';
            container.appendChild(starDust);
        }
        
        // 刷新跨页
        function renderCurrentSpread() {
            const data = spreadsData[currentIndex];
            if (!data) return;
            renderPageContent(leftContainer, data.left);
            renderPageContent(rightContainer, data.right);
            updateDots();
        }
        
        // 圆点高亮
        function updateDots() {
            const dots = document.querySelectorAll('.dot');
            dots.forEach((dot, idx) => {
                if (idx === currentIndex) dot.classList.add('active');
                else dot.classList.remove('active');
            });
        }
        
        // 生成底部圆点导航
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
        
        // 翻页过渡动画
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
                    setTimeout(() => {
                        if (spreadEl) spreadEl.style.transition = '';
                    }, 280);
                }
                updateDots();
            }, 180);
        }
        
        function nextPage() {
            if (currentIndex < totalSpreads - 1) {
                goToSpread(currentIndex + 1);
            } else {
                if (spreadEl) {
                    spreadEl.style.transform = 'translateX(-5px)';
                    setTimeout(() => { if(spreadEl) spreadEl.style.transform = ''; }, 200);
                }
            }
        }
        
        function prevPage() {
            if (currentIndex > 0) {
                goToSpread(currentIndex - 1);
            } else {
                if (spreadEl) {
                    spreadEl.style.transform = 'translateX(5px)';
                    setTimeout(() => { if(spreadEl) spreadEl.style.transform = ''; }, 200);
                }
            }
        }
        
        // 事件绑定
        prevBtn.addEventListener('click', prevPage);
        nextBtn.addEventListener('click', nextPage);
        
        // 键盘支持
        window.addEventListener('keydown', (e) => {
            if (e.key === 'ArrowLeft') {
                e.preventDefault();
                prevPage();
            } else if (e.key === 'ArrowRight') {
                e.preventDefault();
                nextPage();
            }
        });
        
        // 触摸滑动
        let touchStartX = 0;
        spreadEl.addEventListener('touchstart', (e) => {
            touchStartX = e.changedTouches[0].screenX;
        }, { passive: true });
        
        spreadEl.addEventListener('touchend', (e) => {
            const touchEndX = e.changedTouches[0].screenX;
            const diff = touchEndX - touchStartX;
            if (Math.abs(diff) > 50) {
                if (diff > 0) prevPage();
                else nextPage();
            }
        });
        
        // 书本悬停3D微倾斜 (优雅不偏移)
        const book3d = document.getElementById('book3d');
        if (book3d) {
            book3d.addEventListener('mousemove', (e) => {
                const rect = book3d.getBoundingClientRect();
                const x = (e.clientX - rect.left) / rect.width - 0.5;
                const y = (e.clientY - rect.top) / rect.height - 0.5;
                book3d.style.transform = `perspective(1800px) rotateX(${y * 1}deg) rotateY(${x * 2}deg)`;
            });
            book3d.addEventListener('mouseleave', () => {
                book3d.style.transform = '';
            });
        }
        
        // 初始化所有
        function init() {
            buildDots();
            renderCurrentSpread();
            console.log(`✨ 半周年礼物已加载 ✨ 当前共 ${totalSpreads} 个跨页，可容纳 ${totalSpreads * 2} 个视频。`);
            console.log("💡 提示：请将视频文件放入 videos/ 文件夹，并对应修改 spreadsData 中的 videoSrc 路径。");
        }
        
        init();
    </script>
</body>
</html>
