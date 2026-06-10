<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>半周年礼物 · 星空手账</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            user-select: none; /* 避免拖动时误选，不影响文字复制 */
        }

        body {
            min-height: 100vh;
            background: radial-gradient(circle at 20% 30%, #0a0f2a, #030617);
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: "Segoe UI", "Microsoft YaHei", "PingFang SC", "Helvetica Neue", sans-serif;
            overflow: hidden;
            position: relative;
            padding: 20px;
        }

        /* ========= 星星闪烁背景 ========= */
        .star {
            position: absolute;
            background-color: #fff;
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

        /* ========= 横板书本容器 ========= */
        .book-wrapper {
            perspective: 2000px;
            width: 1100px;
            max-width: 90vw;
            height: 650px;
            max-height: 80vh;
            position: relative;
            z-index: 10;
        }

        /* 真正的书本（双开页效果） */
        .book {
            width: 100%;
            height: 100%;
            position: relative;
            transform-style: preserve-3d;
            transition: transform 0.4s cubic-bezier(0.2, 0.8, 0.3, 1);
            border-radius: 16px;
        }

        /* 页面通用样式 ———— 不透明材质，更像书本内页 */
        .page {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            background: #fffcf0;        /* 米白不透明书页，温暖复古感 */
            border-radius: 12px;
            box-shadow: 0 20px 35px rgba(0, 0, 0, 0.3), 0 0 0 1px rgba(255, 245, 215, 0.5);
            backface-visibility: hidden;
            transform-origin: left center;
            transition: transform 0.8s ease-in-out;
            padding: 28px 32px;
            display: flex;
            flex-direction: column;
            overflow-y: auto;
            color: #1e2a3a;
            font-weight: 500;
        }

        /* 右页面需要独立的右原点 (右侧翻书效果做双页展示) */
        /* 这里采用双页展示模式: 左页+右页同时可见，通过translate + 翻页实现类似真实书本效果 */
        /* 为了简化并达到「左右各放视频+文字」且横板，设计一个双页结构：同时显示两个.page，
           用父级旋转和z-index控制。但为了简单维护与完美横板，重写逻辑:
           使用双页展开模式: 每一「跨页」由左页(right side 为0deg)和右页(rotateY 0deg但位置不同)
           这里更优雅: 每一页实际就是一个跨页(左右两个内容区)，用户点击左右箭头切换「跨页」。
           符合横版且不透明书的感觉，且每个跨页内左侧为视频+文字，右侧为视频+文字。 */
        
        /* 重新构思: 因为原代码单页旋转累积容易混乱，采用双面书页但只展示当前打开的一个跨页(左右各一区)，
           优点是完全横版，左右两侧自然分布视频与寄语，且书本厚实不透明。 */
        
        /* 书本跨页容器 */
        .spread {
            width: 100%;
            height: 100%;
            position: relative;
            background: #fffcf0;
            border-radius: 12px;
            box-shadow: 0 20px 35px rgba(0, 0, 0, 0.4);
            display: flex;
            overflow: hidden;
            transition: box-shadow 0.3s;
        }

        /* 左页 & 右页 (各占一半) */
        .left-page, .right-page {
            flex: 1;
            padding: 28px 22px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            background: #fffcf0;
            overflow-y: auto;
            scrollbar-width: thin;
        }

        /* 中间书缝阴影效果 */
        .left-page {
            border-right: 1px solid #e2d8bd;
            box-shadow: inset -2px 0 5px rgba(0,0,0,0.02);
        }

        .right-page {
            border-left: 1px solid #e9e0c7;
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

        /* 标题、文字风格 */
        .greeting-title {
            font-size: 1.9rem;
            font-weight: 700;
            background: linear-gradient(135deg, #b85c1a, #5e2a0c);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 20px;
            letter-spacing: 2px;
            border-left: 5px solid #ffb347;
            padding-left: 18px;
        }

        .message-text {
            font-size: 1rem;
            line-height: 1.65;
            color: #2c3e2f;
            background: rgba(245, 235, 210, 0.6);
            padding: 18px;
            border-radius: 28px;
            margin: 15px 0;
            font-style: normal;
            font-weight: 500;
            box-shadow: inset 0 0 0 1px #fff8e7, 0 5px 12px rgba(0,0,0,0.05);
        }

        /* 视频容器 */
        .video-box {
            background: #1e1b14;
            border-radius: 24px;
            overflow: hidden;
            margin: 15px 0;
            box-shadow: 0 12px 22px rgba(0, 0, 0, 0.2);
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
            font-size: 0.9rem;
            text-align: center;
            margin-top: 10px;
            color: #a37242;
            font-weight: 500;
            letter-spacing: 1px;
        }

        /* 装饰分隔 */
        .deco-line {
            height: 2px;
            background: linear-gradient(90deg, #f7d98c, #c8a86b, #f7d98c);
            width: 60px;
            margin: 12px 0;
        }

        /* 书本页码指示器 (圆形小点) 和 翻页箭头 置于书本外侧 */
        .nav-controls {
            position: absolute;
            bottom: -60px;
            left: 0;
            width: 100%;
            display: flex;
            justify-content: center;
            gap: 20px;
            z-index: 20;
        }

        .nav-btn {
            background: rgba(30, 25, 45, 0.75);
            backdrop-filter: blur(6px);
            border: 1px solid rgba(255, 215, 150, 0.6);
            color: #ffecb3;
            font-size: 1.8rem;
            padding: 8px 20px;
            border-radius: 48px;
            cursor: pointer;
            transition: all 0.25s;
            font-weight: bold;
            box-shadow: 0 2px 12px rgba(0,0,0,0.3);
        }

        .nav-btn:hover {
            background: #b87c3e;
            color: white;
            border-color: #ffe0a3;
            transform: scale(1.03);
        }

        .dot-group {
            display: flex;
            gap: 14px;
            align-items: center;
            background: rgba(0,0,0,0.3);
            backdrop-filter: blur(4px);
            padding: 0 20px;
            border-radius: 60px;
        }

        .dot {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            background: #9f8b6e;
            transition: all 0.2s;
            cursor: pointer;
        }

        .dot.active {
            background: #ffc485;
            transform: scale(1.3);
            box-shadow: 0 0 8px #ffbc6e;
        }

        /* 书本外部装饰 */
        .book-shadow {
            position: absolute;
            width: 100%;
            height: 100%;
            border-radius: 16px;
            box-shadow: 0 25px 45px rgba(0, 0, 0, 0.5);
            pointer-events: none;
        }

        /* 确保翻页只有一跨页滑动，横板左右内容同时可见，没有全局标题遮挡 */
        /* 全局标题移除，在每个跨页内部各自展示半周年纪念主题 */
        
        /* 响应式调整 */
        @media (max-width: 780px) {
            .book-wrapper {
                height: 580px;
            }
            .left-page, .right-page {
                padding: 18px 15px;
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
                font-size: 1.2rem;
                padding: 6px 16px;
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

        /* 书脊效果 */
        .book-spine {
            position: absolute;
            left: 0;
            top: 0;
            width: 18px;
            height: 100%;
            background: #cfa668;
            border-radius: 8px 0 0 8px;
            z-index: 5;
            box-shadow: inset -1px 0 3px rgba(0,0,0,0.2);
        }
    </style>
</head>
<body>

    <!-- 动态星星背景 -->
    <div id="starfield"></div>

    <div class="book-wrapper">
        <!-- 模拟书脊装饰 (不遮挡内容) -->
        <div class="book-spine"></div>
        <div class="book" id="bookContainer">
            <!-- 跨页内容由 js 动态生成，便于管理不同跨页的数据，但保留结构与样式分离 -->
            <div class="spread" id="activeSpread">
                <!-- 左页区域 -->
                <div class="left-page" id="leftPage">
                    <!-- 动态内容填充 -->
                </div>
                <!-- 右页区域 -->
                <div class="right-page" id="rightPage">
                    <!-- 动态内容填充 -->
                </div>
            </div>
        </div>
        <div class="book-shadow"></div>
        
        <!-- 底部翻页控件 -->
        <div class="nav-controls">
            <button class="nav-btn" id="prevBtn">◀ 上一页</button>
            <div class="dot-group" id="dotGroup"></div>
            <button class="nav-btn" id="nextBtn">下一页 ▶</button>
        </div>
    </div>

    <script>
        // 创造闪烁星辰背景（数量增加，适配横板）
        function createStars() {
            const starCount = 220;
            const starField = document.getElementById('starfield');
            for (let i = 0; i < starCount; i++) {
                const star = document.createElement('div');
                star.classList.add('star');
                const size = Math.random() * 4 + 1;
                star.style.width = size + 'px';
                star.style.height = size + 'px';
                star.style.left = Math.random() * 100 + '%';
                star.style.top = Math.random() * 100 + '%';
                const duration = Math.random() * 3 + 1.5;
                star.style.animationDuration = duration + 's';
                star.style.animationDelay = Math.random() * 4 + 's';
                star.style.opacity = Math.random() * 0.8 + 0.2;
                starField.appendChild(star);
            }
        }
        createStars();

        // ========= 跨页数据集：每一跨页包含左页内容（视频+文字） 和 右页内容（视频+文字） =========
        // 注意：需要用户自己替换视频链接，此处预留示例及提示，将 your-video-left.mp4, your-video-right.mp4
        // 替换成仓库真实视频文件。为了演示，可使用线上占位视频或提醒。
        // 因为真实场景中用户可能本地视频，但为了开箱体验，我放置示例提示，实际使用时替换视频src。
        // 视频路径可按需修改，例如 "video1.mp4" "video2.mp4"，这里使用类似示例提供但确保不会报错空白。
        
        const spreadsData = [
            {   // 跨页1: 半周年专属首页
                left: {
                    title: "✨ 半周年快乐 ✨",
                    message: "遇见你的第183天，每一天都像星星在夜空发光。谢谢你让我明白温柔的力量，这是属于我们的第一个半周年，未来还有很多个半年。",
                    videoSrc: "assets/video-left.mp4",   // 替换成你的视频
                    videoPoster: "",
                    caption: "初次相遇的那个瞬间"
                },
                right: {
                    title: "给特别的你",
                    message: "你像星星一样照亮了我的世界，和你在一起的每一刻都值得珍藏。半周年快乐，我最重要的人。",
                    videoSrc: "assets/video-right.mp4",
                    videoPoster: "",
                    caption: "那些甜甜的小碎片"
                }
            },
            {   // 跨页2: 温馨日常
                left: {
                    title: "📖 我们的纪念册",
                    message: "想起那些一起度过的安静夜晚，你笑着说话的样子，是记忆里最暖的星芒。愿我们继续分享喜悦，分担忧愁。",
                    videoSrc: "assets/memory-left.mp4",
                    caption: "偷偷记录的笑容"
                },
                right: {
                    title: "🌙 未来的信",
                    message: "你是我平凡生活里的浪漫奇迹，想要和你一起看遍春夏秋冬。愿你永远自由闪亮，我永远在你身边。",
                    videoSrc: "assets/memory-right.mp4",
                    caption: "晚风与星光见证"
                }
            },
            {   // 跨页3: 浪漫星语
                left: {
                    title: "💫 星语心愿",
                    message: "每一颗星星都代表我想对你说的话——喜欢你的温柔，喜欢你的坚定，喜欢和你一起的每分每秒。",
                    videoSrc: "assets/star-left.mp4",
                    caption: "爱意藏在星河里"
                },
                right: {
                    title: "🎁 半周年礼赠",
                    message: "愿这份小小礼物带给你整晚的好心情。你永远值得世上所有美好，我会一直陪你漫步星空下。",
                    videoSrc: "assets/star-right.mp4",
                    caption: "专属浪漫定格"
                }
            }
        ];

        // 如果视频不存在，为了避免报错和控制台烦人，但保留可加载提示，用户替换真实视频即可。
        // 为了让演示时视频区域更美观，加入优雅降级：若视频加载失败显示文字占位符。
        // 此外，为了不因为视频缺失影响整体美感，用背景提示。
        
        // 当前跨页索引
        let currentSpreadIndex = 0;
        const totalSpreads = spreadsData.length;

        // DOM 元素
        const leftPageDiv = document.getElementById('leftPage');
        const rightPageDiv = document.getElementById('rightPage');
        const prevBtn = document.getElementById('prevBtn');
        const nextBtn = document.getElementById('nextBtn');
        const dotGroup = document.getElementById('dotGroup');

        // 生成对应页码圆点
        function renderDots() {
            dotGroup.innerHTML = '';
            for (let i = 0; i < totalSpreads; i++) {
                const dot = document.createElement('div');
                dot.classList.add('dot');
                if (i === currentSpreadIndex) dot.classList.add('active');
                dot.addEventListener('click', () => {
                    if (i !== currentSpreadIndex) {
                        currentSpreadIndex = i;
                        renderSpread();
                        updateDotsActive();
                    }
                });
                dotGroup.appendChild(dot);
            }
        }

        function updateDotsActive() {
            const dots = document.querySelectorAll('.dot');
            dots.forEach((dot, idx) => {
                if (idx === currentSpreadIndex) dot.classList.add('active');
                else dot.classList.remove('active');
            });
        }

        // 辅助函数：创建视频元素，并处理加载失败时显示占位提示
        function createVideoElement(src, captionText, poster = '') {
            const container = document.createElement('div');
            container.className = 'video-box';
            const video = document.createElement('video');
            video.controls = true;
            video.preload = "metadata";
            video.playsInline = true;
            if (poster) video.poster = poster;
            // 设置视频源
            const source = document.createElement('source');
            source.src = src;
            source.type = 'video/mp4';
            video.appendChild(source);
            // 优雅降级: 如果视频加载错误，显示提示文字，避免空白区域尴尬
            video.onerror = () => {
                // 移除可能出现的错误样式，显示背景提示
                container.style.background = "#30271c";
                container.style.display = "flex";
                container.style.alignItems = "center";
                container.style.justifyContent = "center";
                container.style.color = "#ecd9b4";
                container.style.fontSize = "14px";
                container.innerHTML = '<div style="text-align:center;">✨ 视频即将加载 ✨<br>可替换 src 为真实视频</div>';
                video.style.display = 'none';
            };
            container.appendChild(video);
            const captionEl = document.createElement('div');
            captionEl.className = 'caption';
            captionEl.innerText = captionText;
            container.appendChild(captionEl);
            return container;
        }

        // 渲染当前跨页左右内容
        function renderSpread() {
            const data = spreadsData[currentSpreadIndex];
            if (!data) return;
            
            // 渲染左页
            renderPageContent(leftPageDiv, data.left);
            // 渲染右页
            renderPageContent(rightPageDiv, data.right);
        }

        function renderPageContent(container, content) {
            // 清空容器，保留原有类结构但完全重绘
            container.innerHTML = '';
            
            // 标题
            const title = document.createElement('h2');
            title.className = 'greeting-title';
            title.innerText = content.title || '✨ 珍藏时刻 ✨';
            container.appendChild(title);
            
            // 装饰细线
            const deco = document.createElement('div');
            deco.className = 'deco-line';
            container.appendChild(deco);
            
            // 文字内容
            const msgBox = document.createElement('div');
            msgBox.className = 'message-text';
            msgBox.innerText = content.message || '愿所有星光奔向你。';
            container.appendChild(msgBox);
            
            // 视频区域（如果提供视频src）
            if (content.videoSrc) {
                // 避免重复创建复杂的视频逻辑
                const videoContainer = createVideoElement(content.videoSrc, content.caption || '♡ 珍藏片段 ♡', content.poster || '');
                container.appendChild(videoContainer);
            } else {
                // 如果没有视频，展示一张图像占位符或星星图案
                const placeholder = document.createElement('div');
                placeholder.style.background = "#efe2cc";
                placeholder.style.borderRadius = "28px";
                placeholder.style.padding = "24px 12px";
                placeholder.style.textAlign = "center";
                placeholder.style.margin = "20px 0";
                placeholder.innerHTML = '⭐ 星空映像 ⭐<br style="margin:6px"> 浪漫影像稍后呈现';
                placeholder.style.color = "#956e3e";
                placeholder.style.fontWeight = "500";
                container.appendChild(placeholder);
                if (content.caption) {
                    const cap = document.createElement('div');
                    cap.className = 'caption';
                    cap.innerText = content.caption;
                    container.appendChild(cap);
                }
            }
            
            // 额外增加一点点浪漫小元素
            const starIcon = document.createElement('div');
            starIcon.style.textAlign = 'center';
            starIcon.style.marginTop = '16px';
            starIcon.style.fontSize = '20px';
            starIcon.style.letterSpacing = '4px';
            starIcon.innerHTML = '✧  ⋆  ✦  ⋆  ✧';
            starIcon.style.opacity = '0.5';
            container.appendChild(starIcon);
        }
        
        // 翻页逻辑 (横板左右内容整体更换，具有书本动画翻页感觉)
        // 为增加书本翻页优雅效果: 给spread添加瞬时动画类模仿翻页，但不做复杂3d保持简洁横板。
        // 让用户感受到书页更替的流畅过渡，添加淡入淡出 + 轻微滑动。
        const spreadElement = document.querySelector('.spread');
        
        function animateTransition(direction, callback) {
            if (!spreadElement) return callback();
            // 添加翻动渐隐效果
            spreadElement.style.transition = 'opacity 0.2s ease, transform 0.25s';
            spreadElement.style.opacity = '0';
            spreadElement.style.transform = `scale(0.98) translateX(${direction === 'next' ? '8px' : '-8px'})`;
            setTimeout(() => {
                callback();
                spreadElement.style.transition = 'opacity 0.25s ease, transform 0.3s';
                spreadElement.style.opacity = '1';
                spreadElement.style.transform = 'scale(1) translateX(0)';
                setTimeout(() => {
                    if (spreadElement) spreadElement.style.transition = '';
                }, 300);
            }, 180);
        }
        
        function goToPrev() {
            if (currentSpreadIndex > 0) {
                animateTransition('prev', () => {
                    currentSpreadIndex--;
                    renderSpread();
                    updateDotsActive();
                });
            } else {
                // 第一页轻弹提示效果（可加震动动画）
                spreadElement.style.transform = 'translateX(6px)';
                setTimeout(() => { if(spreadElement) spreadElement.style.transform = ''; }, 150);
            }
        }
        
        function goToNext() {
            if (currentSpreadIndex < totalSpreads - 1) {
                animateTransition('next', () => {
                    currentSpreadIndex++;
                    renderSpread();
                    updateDotsActive();
                });
            } else {
                spreadElement.style.transform = 'translateX(-6px)';
                setTimeout(() => { if(spreadElement) spreadElement.style.transform = ''; }, 150);
            }
        }
        
        // 绑定按钮事件
        prevBtn.addEventListener('click', goToPrev);
        nextBtn.addEventListener('click', goToNext);
        
        // 键盘左右键支持
        window.addEventListener('keydown', (e) => {
            if (e.key === 'ArrowLeft') {
                e.preventDefault();
                goToPrev();
            } else if (e.key === 'ArrowRight') {
                e.preventDefault();
                goToNext();
            }
        });
        
        // 触摸滑动支持 (横滑)
        let touchStart = 0;
        let touchEnd = 0;
        spreadElement.addEventListener('touchstart', (e) => {
            touchStart = e.changedTouches[0].screenX;
        });
        spreadElement.addEventListener('touchend', (e) => {
            touchEnd = e.changedTouches[0].screenX;
            const diff = touchEnd - touchStart;
            if (Math.abs(diff) > 50) {
                if (diff > 0) {
                    goToPrev();
                } else {
                    goToNext();
                }
            }
        });
        
        // 注意：全局标题问题已被完全解决，原代码中封面独立的标题遮挡已经消失，因为现在是每跨页双内容展示
        // 且没有任何单独的浮动全局标题层。第一个跨页左侧就已经有半周年快乐主题。
        // 用户可再根据需要修改 spreadsData 内的任意文字和视频链接。
        
        // 为了体现横板视频+文字完美展示，同时保证示例即使没有视频也显示占位，提示用户替换
        // 控制台输出友好提示：如何替换视频路径
        console.log("✨ 半周年礼物已加载 ✨ 如需替换视频，请修改 spreadsData 中的 videoSrc 字段为你的视频相对路径，例如 'videos/halfyear.mp4'");
        
        // 预初始化展示
        renderDots();
        renderSpread();
        
        // 如果用户想要使用更加丰富的视频链接，直接在上方数据集调整即可。
        // 另外，用户提到「首页展示的这是你的礼物变成了全局展示」，现完全移除此问题，每页独立，左右各自展示想说的话。
        // 此外背景星星已加密，横板书本质感不透明米色纸张，更具礼物质感。
        // 增加一些小优化：防止页面滚动导致边缘滑动浏览器后退 (overscroll 阻止无影响)
        document.body.addEventListener('touchmove', (e) => {
            // 不干扰书本内部滑动，但防止在 body 上滚动时让背景动，轻微禁止非必要滚动
            if (e.target.closest('.left-page') || e.target.closest('.right-page')) return;
            e.preventDefault();
        }, { passive: false });
        
        // 增加书页阴影动态
        const bookDiv = document.querySelector('.book');
        if(bookDiv) {
            bookDiv.addEventListener('mousemove', (e) => {
                const rect = bookDiv.getBoundingClientRect();
                const x = (e.clientX - rect.left) / rect.width - 0.5;
                const y = (e.clientY - rect.top) / rect.height - 0.5;
                bookDiv.style.transform = `perspective(2000px) rotateX(${y * 1.5}deg) rotateY(${x * 3}deg)`;
            });
            bookDiv.addEventListener('mouseleave', () => {
                bookDiv.style.transform = '';
            });
        }
    </script>
</body>
</html>
