<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>半周年礼物 · 星空手账</title>
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

        /* ---------- 闪烁星星背景 ---------- */
        .star {
            position: absolute;
            background-color: #ffffff;
            border-radius: 50%;
            box-shadow: 0 0 6px rgba(255, 255, 255, 0.8);
            animation: twinkle 3s infinite alternate ease-in-out;
            pointer-events: none;
            z-index: 0;
        }

        @keyframes twinkle {
            0% { opacity: 0.2; transform: scale(0.7); }
            100% { opacity: 1; transform: scale(1.2); }
        }

        /* ---------- 横板书本容器 ---------- */
        .book-wrapper {
            perspective: 1800px;
            width: 1200px;
            max-width: 90vw;
            height: 680px;
            max-height: 80vh;
            position: relative;
            z-index: 10;
        }

        /* 书本主体 */
        .book {
            width: 100%;
            height: 100%;
            position: relative;
            transition: transform 0.3s ease-out;
            border-radius: 16px;
        }

        /* 跨页 (左右双页) — 不透明书页质感 */
        .spread {
            width: 100%;
            height: 100%;
            background: #fffcf0;        /* 米白不透明书页 */
            border-radius: 16px;
            box-shadow: 0 25px 45px rgba(0, 0, 0, 0.4), inset 0 0 0 1px rgba(255, 245, 215, 0.8);
            display: flex;
            overflow: hidden;
            transition: opacity 0.25s ease, transform 0.3s ease;
        }

        /* 左页 & 右页 (各占一半) */
        .left-page, .right-page {
            flex: 1;
            padding: 28px 26px;
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
            font-size: 1.8rem;
            font-weight: 700;
            background: linear-gradient(135deg, #b85c1a, #7b3e10);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 16px;
            letter-spacing: 1px;
            border-left: 5px solid #ffb347;
            padding-left: 18px;
        }

        /* 文字寄语框 */
        .message-text {
            font-size: 1rem;
            line-height: 1.7;
            color: #2c3e2f;
            background: rgba(248, 240, 218, 0.7);
            padding: 18px 20px;
            border-radius: 28px;
            margin: 15px 0;
            font-weight: 500;
            box-shadow: inset 0 0 0 1px #fff9ef, 0 6px 14px rgba(0, 0, 0, 0.04);
        }

        /* 视频容器 */
        .video-box {
            background: #1e1b14;
            border-radius: 24px;
            overflow: hidden;
            margin: 16px 0 8px 0;
            box-shadow: 0 12px 20px rgba(0, 0, 0, 0.2);
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
            font-size: 0.85rem;
            text-align: center;
            margin-top: 8px;
            color: #a37242;
            font-weight: 500;
            letter-spacing: 1px;
        }

        /* 装饰细线 */
        .deco-line {
            height: 2px;
            background: linear-gradient(90deg, #f7d98c, #c8a86b, #f7d98c);
            width: 60px;
            margin: 8px 0 6px 0;
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
            background: rgba(25, 20, 35, 0.8);
            backdrop-filter: blur(8px);
            border: 1px solid rgba(255, 215, 150, 0.7);
            color: #ffefcf;
            font-size: 1.3rem;
            padding: 8px 28px;
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
            gap: 14px;
            align-items: center;
            background: rgba(0, 0, 0, 0.3);
            backdrop-filter: blur(4px);
            padding: 8px 24px;
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

        /* 手机适配 */
        @media (max-width: 800px) {
            .book-wrapper {
                height: 580px;
            }
            .left-page, .right-page {
                padding: 18px 14px;
            }
            .greeting-title {
                font-size: 1.3rem;
            }
            .message-text {
                font-size: 0.85rem;
                padding: 12px;
            }
            .caption {
                font-size: 0.7rem;
            }
            .nav-btn {
                font-size: 1rem;
                padding: 6px 20px;
            }
        }

        @media (max-width: 600px) {
            .greeting-title {
                font-size: 1.1rem;
            }
            .message-text {
                font-size: 0.75rem;
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
        // ======================== 1. 生成星星背景 ========================
        (function initStars() {
            const starContainer = document.getElementById('star-bg');
            const starCount = 220;
            for (let i = 0; i < starCount; i++) {
                const star = document.createElement('div');
                star.classList.add('star');
                const size = Math.random() * 4 + 1.5;
                star.style.width = size + 'px';
                star.style.height = size + 'px';
                star.style.left = Math.random() * 100 + '%';
                star.style.top = Math.random() * 100 + '%';
                const duration = Math.random() * 3 + 1.8;
                star.style.animationDuration = duration + 's';
                star.style.animationDelay = Math.random() * 4 + 's';
                star.style.opacity = Math.random() * 0.7 + 0.3;
                starContainer.appendChild(star);
            }
        })();

        // ======================== 2. 书本数据 (每个跨页: 左页 + 右页, 各自包含视频+文字) ========================
        // ！！！重要！！！ 请将下面的视频路径替换为你自己的视频文件 (例如 "videos/left1.mp4", "videos/right1.mp4")
        // 如果你还没有上传视频，可以暂时保留示例占位符，页面会显示可爱的占位提示。
        // 建议将视频放在仓库中的 "videos" 文件夹下，然后按照如下格式填写。
        
        const spreadsData = [
            { // 第1跨页 · 半周年纪念
                left: {
                    title: "✨ 半周年快乐 ✨",
                    message: "遇见你的第183天，每一天都像星星在夜空发光。谢谢你让我明白温柔的意义，这是属于我们的第一个半周年，未来还有更多故事。",
                    videoSrc: "videos/half-left.mp4",   // 👈 替换成你的视频路径
                    caption: "最初相遇时的星光"
                },
                right: {
                    title: "💖 致唯一的你",
                    message: "你像星星一样照亮我的世界，和你在一起的每一刻都是宝藏。半周年快乐，我最重要的人。",
                    videoSrc: "videos/half-right.mp4",  // 👈 替换成你的视频路径
                    caption: "那些温暖的小碎片"
                }
            },
            { // 第2跨页 · 珍藏时光
                left: {
                    title: "📖 我们的纪念册",
                    message: "想起那些一起散步、傻笑、分享耳机的夜晚，你笑起来的弧度是记忆里最暖的星芒。愿我们继续共享喜悦，陪伴彼此。",
                    videoSrc: "videos/memory-left.mp4",
                    caption: "偷偷记录的心动"
                },
                right: {
                    title: "🌙 未来情书",
                    message: "你是我平凡生活里的浪漫奇迹，想要和你一起看遍春夏秋冬。愿你永远自由闪亮，我会一直在你身边。",
                    videoSrc: "videos/memory-right.mp4",
                    caption: "晚风与星光见证"
                }
            },
            { // 第3跨页 · 星语心愿
                left: {
                    title: "💫 星河絮语",
                    message: "每一颗星星都代表我想对你说的话——喜欢你的温柔，喜欢你的坚定，喜欢和你在一起的每分每秒。",
                    videoSrc: "videos/star-left.mp4",
                    caption: "爱意藏在星河里"
                },
                right: {
                    title: "🎁 专属礼物",
                    message: "愿这份小小手账带给你整晚的好心情。你永远值得世上所有美好，我会一直陪你漫步星空下。",
                    videoSrc: "videos/star-right.mp4",
                    caption: "永恒的浪漫定格"
                }
            }
             { // 第4跨页 · 珍藏时光
                left: {
                    title: "📖 我们的纪念册",
                    message: "想起那些一起散步、傻笑、分享耳机的夜晚，你笑起来的弧度是记忆里最暖的星芒。愿我们继续共享喜悦，陪伴彼此。",
                    videoSrc: "videos/memory-left.mp4",
                    caption: "偷偷记录的心动"
                },
                right: {
                    title: "🌙 未来情书",
                    message: "你是我平凡生活里的浪漫奇迹，想要和你一起看遍春夏秋冬。愿你永远自由闪亮，我会一直在你身边。",
                    videoSrc: "videos/memory-right.mp4",
                    caption: "晚风与星光见证"
                }
                 { // 第5跨页 · 珍藏时光
                left: {
                    title: "📖 我们的纪念册",
                    message: "想起那些一起散步、傻笑、分享耳机的夜晚，你笑起来的弧度是记忆里最暖的星芒。愿我们继续共享喜悦，陪伴彼此。",
                    videoSrc: "videos/memory-left.mp4",
                    caption: "偷偷记录的心动"
                },
                right: {
                    title: "🌙 未来情书",
                    message: "你是我平凡生活里的浪漫奇迹，想要和你一起看遍春夏秋冬。愿你永远自由闪亮，我会一直在你身边。",
                    videoSrc: "videos/memory-right.mp4",
                    caption: "晚风与星光见证"
                }
        ];

        // ------------------ 全局变量 ------------------
        let currentIndex = 0;          // 当前跨页索引
        const totalSpreads = spreadsData.length;
        const leftContainer = document.getElementById('leftPage');
        const rightContainer = document.getElementById('rightPage');
        const prevBtn = document.getElementById('prevBtn');
        const nextBtn = document.getElementById('nextBtn');
        const dotGroup = document.getElementById('dotGroup');
        const spreadEl = document.getElementById('spreadContainer');

        // ------------------ 辅助函数: 优雅创建视频元素(含加载失败占位) ------------------
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
            
            // 如果视频加载失败 (文件不存在或路径错误)，显示占位而不报错丑陋
            video.onerror = () => {
                wrapper.style.background = "#2e2a1f";
                wrapper.style.display = "flex";
                wrapper.style.flexDirection = "column";
                wrapper.style.alignItems = "center";
                wrapper.style.justifyContent = "center";
                wrapper.style.borderRadius = "24px";
                wrapper.innerHTML = `
                    <div style="text-align:center; color:#f5e2b0; padding:20px;">
                        ✨ 星空影像 ✨<br>
                        <span style="font-size:12px;">🎬 视频待放入</span><br>
                        <span style="font-size:11px;">请将视频文件放入指定路径</span>
                    </div>
                `;
                video.style.display = 'none';
                return;
            };
            
            wrapper.appendChild(video);
            
            // 字幕说明
            const captionDiv = document.createElement('div');
            captionDiv.className = 'caption';
            captionDiv.innerText = captionText || '♡ 珍藏片段 ♡';
            wrapper.appendChild(captionDiv);
            
            return wrapper;
        }

        // 渲染单个页面内容 (左页或右页)
        function renderPageContent(container, pageData) {
            container.innerHTML = '';   // 清空
            
            // 标题
            const title = document.createElement('h2');
            title.className = 'greeting-title';
            title.innerText = pageData.title || '✨ 珍藏时刻 ✨';
            container.appendChild(title);
            
            // 装饰线
            const deco = document.createElement('div');
            deco.className = 'deco-line';
            container.appendChild(deco);
            
            // 寄语文字框
            const msgBox = document.createElement('div');
            msgBox.className = 'message-text';
            msgBox.innerText = pageData.message || '愿所有星光奔向你。';
            container.appendChild(msgBox);
            
            // 视频区域 (若路径存在则创建，否则优雅占位)
            if (pageData.videoSrc) {
                const videoWidget = createVideoElement(pageData.videoSrc, pageData.caption || '♡ 你的故事 ♡');
                container.appendChild(videoWidget);
            } else {
                // 如果没有提供视频路径，展示一个星空气氛占位
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
            
            // 底部加一点星尘装饰
            const starDust = document.createElement('div');
            starDust.style.textAlign = 'center';
            starDust.style.marginTop = '18px';
            starDust.style.fontSize = '18px';
            starDust.style.letterSpacing = '4px';
            starDust.style.opacity = '0.5';
            starDust.innerHTML = '✧  ⋆  ✦  ⋆  ✧';
            container.appendChild(starDust);
        }
        
        // 刷新整个跨页 (左右同时渲染)
        function renderCurrentSpread() {
            const data = spreadsData[currentIndex];
            if (!data) return;
            renderPageContent(leftContainer, data.left);
            renderPageContent(rightContainer, data.right);
            updateDots();
        }
        
        // 更新底部圆点高亮
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
                    if (i !== currentIndex) {
                        goToSpread(i);
                    }
                });
                dotGroup.appendChild(dot);
            }
        }
        
        // 带过渡动画的翻页
        function goToSpread(newIndex) {
            if (newIndex === currentIndex) return;
            if (newIndex < 0 || newIndex >= totalSpreads) return;
            
            // 添加淡入淡出+轻微位移动画
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
                // 最后一页微动反馈
                if (spreadEl) {
                    spreadEl.style.transform = 'translateX(-6px)';
                    setTimeout(() => { if(spreadEl) spreadEl.style.transform = ''; }, 200);
                }
            }
        }
        
        function prevPage() {
            if (currentIndex > 0) {
                goToSpread(currentIndex - 1);
            } else {
                if (spreadEl) {
                    spreadEl.style.transform = 'translateX(6px)';
                    setTimeout(() => { if(spreadEl) spreadEl.style.transform = ''; }, 200);
                }
            }
        }
        
        // ---------- 事件绑定 & 触摸滑动支持 ----------
        prevBtn.addEventListener('click', prevPage);
        nextBtn.addEventListener('click', nextPage);
        
        // 键盘左右键支持
        window.addEventListener('keydown', (e) => {
            if (e.key === 'ArrowLeft') {
                e.preventDefault();
                prevPage();
            } else if (e.key === 'ArrowRight') {
                e.preventDefault();
                nextPage();
            }
        });
        
        // 触摸滑动 (左右滑动切换跨页)
        let touchStartX = 0;
        let touchEndX = 0;
        spreadEl.addEventListener('touchstart', (e) => {
            touchStartX = e.changedTouches[0].screenX;
        }, { passive: true });
        
        spreadEl.addEventListener('touchend', (e) => {
            touchEndX = e.changedTouches[0].screenX;
            const diff = touchEndX - touchStartX;
            if (Math.abs(diff) > 50) {
                if (diff > 0) {
                    prevPage();   // 右滑上一页
                } else {
                    nextPage();   // 左滑下一页
                }
            }
        });
        
        // 可选: 增加微妙的鼠标倾斜效果 (增加书本立体感)
        const book3d = document.getElementById('book3d');
        if (book3d) {
            book3d.addEventListener('mousemove', (e) => {
                const rect = book3d.getBoundingClientRect();
                const x = (e.clientX - rect.left) / rect.width - 0.5;
                const y = (e.clientY - rect.top) / rect.height - 0.5;
                book3d.style.transform = `perspective(1800px) rotateX(${y * 1.2}deg) rotateY(${x * 2.5}deg)`;
            });
            book3d.addEventListener('mouseleave', () => {
                book3d.style.transform = '';
            });
        }
        
        // 初始化所有内容
        function init() {
            buildDots();
            renderCurrentSpread();
            // 控制台友好提示
            console.log("✨ 半周年礼物已加载 ✨ 请将视频文件放入对应路径（参考 spreadsData 中的 videoSrc），例如将视频放在 videos/ 文件夹下");
            console.log("📖 当前跨页数量: " + totalSpreads + "  |  使用左右箭头或滑动触摸翻页");
        }
        
        init();
    </script>
</body>
</html>
