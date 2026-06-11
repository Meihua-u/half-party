<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes, viewport-fit=cover">
    <title>半周年礼物 · 星空手账 · 珍藏纪念册</title>
    <style>
        /* ---------- 全局重置，保证滚动与缩放体验 ---------- */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            user-select: none; /* 避免拖动时选中文字，不影响体验，不影响链接 */
        }

        body {
            min-height: 100vh;
            background: radial-gradient(circle at 30% 20%, #0a0f2a, #030617);
            display: flex;
            justify-content: center;
            align-items: center;
            font-family: "Segoe UI", "Microsoft YaHei", "PingFang SC", "Helvetica Neue", sans-serif;
            padding: 20px;
            /* 允许滚动，因为如果手机横屏或者尺寸极小，用户可上下滑动调整视野，同时书页内部也有滚动条 */
            overflow-y: auto;
            overflow-x: hidden;
        }

        /* ---------- 闪烁星星背景 (动态) ---------- */
        .star {
            position: fixed;
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

        /* 主容器：书本外层，使用flex让全书居中，且支持页面滚动时保持居中 */
        .global-book-container {
            display: flex;
            justify-content: center;
            align-items: center;
            width: 100%;
            min-height: 100vh;
            padding: 30px 20px;
            position: relative;
            z-index: 5;
        }

        /* 书本包装器：固定宽高比和最大尺寸，完美适配封面与内页统一大小 */
        .book-wrapper {
            perspective: 2000px;
            width: 1200px;
            max-width: 95vw;
            height: auto;
            min-height: 620px;
            transition: all 0.2s;
            position: relative;
        }

        /* 书本主体，将封面和内页共用相同尺寸容器 */
        .book {
            width: 100%;
            position: relative;
            transition: transform 0.2s ease;
            border-radius: 20px;
        }

        /* 核心翻页区域 (封面视图 & 内页视图共用统一尺寸) */
        .book-viewport {
            width: 100%;
            background: transparent;
            border-radius: 20px;
            transition: all 0.35s cubic-bezier(0.2, 0.9, 0.4, 1.1);
        }

        /* ---------- 封面样式 (合上的书) ---------- */
        .cover-container {
            width: 100%;
            background: linear-gradient(145deg, #2c2418, #1f1a10);
            border-radius: 24px;
            box-shadow: 0 35px 55px rgba(0, 0, 0, 0.5), inset 0 1px 2px rgba(255, 245, 200, 0.2);
            padding: 40px 30px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            text-align: center;
            cursor: pointer;
            transition: all 0.4s;
            border: 1px solid #c9aa6f;
            backdrop-filter: blur(1px);
            min-height: 620px;
        }

        .cover-container:hover {
            transform: scale(0.99);
            box-shadow: 0 25px 45px rgba(0, 0, 0, 0.6);
        }

        .cover-star {
            font-size: 5rem;
            letter-spacing: 20px;
            margin-bottom: 20px;
            filter: drop-shadow(0 0 8px #ffd27a);
        }

        .cover-title {
            font-size: 3rem;
            font-weight: 800;
            background: linear-gradient(135deg, #ffdb9f, #ffb347, #e5983e);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: 0 2px 8px rgba(0,0,0,0.2);
            letter-spacing: 6px;
            margin: 15px 0;
        }

        .cover-sub {
            color: #f7e5c2;
            font-size: 1.2rem;
            border-top: 2px solid #e7bc7e;
            display: inline-block;
            padding-top: 12px;
            margin-top: 10px;
            font-weight: 300;
        }

        .open-hint {
            margin-top: 45px;
            background: rgba(0,0,0,0.4);
            padding: 8px 24px;
            border-radius: 60px;
            color: #ffe5b4;
            font-size: 1rem;
            backdrop-filter: blur(4px);
            transition: 0.2s;
        }

        /* 内页跨页样式 (打开的书) 与原设计一致 */
        .spread {
            width: 100%;
            background: #fffcf0;
            border-radius: 20px;
            box-shadow: 0 25px 45px rgba(0, 0, 0, 0.4), inset 0 0 0 1px rgba(255, 245, 215, 0.8);
            display: flex;
            overflow: hidden;
            transition: opacity 0.25s ease, transform 0.3s;
            min-height: 620px;
        }

        .left-page, .right-page {
            flex: 1;
            padding: 28px 26px;
            display: flex;
            flex-direction: column;
            justify-content: flex-start;
            background: #fffcf0;
            overflow-y: auto;
            scrollbar-width: thin;
            max-height: 70vh;
        }

        .left-page {
            border-right: 2px solid #e6dcc6;
        }

        .right-page {
            border-left: 2px solid #f1e8d4;
        }

        /* 自定义滚动条保持优雅 */
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

        /* 内部样式 */
        .greeting-title {
            font-size: 1.8rem;
            font-weight: 700;
            background: linear-gradient(135deg, #b85c1a, #7b3e10);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 16px;
            border-left: 5px solid #ffb347;
            padding-left: 18px;
        }

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
        }

        .deco-line {
            height: 2px;
            background: linear-gradient(90deg, #f7d98c, #c8a86b, #f7d98c);
            width: 60px;
            margin: 8px 0 6px 0;
        }

        /* 底部导航栏 */
        .nav-controls {
            display: flex;
            justify-content: center;
            gap: 24px;
            align-items: center;
            margin-top: 35px;
            flex-wrap: wrap;
        }

        .nav-btn {
            background: rgba(25, 20, 35, 0.8);
            backdrop-filter: blur(8px);
            border: 1px solid rgba(255, 215, 150, 0.7);
            color: #ffefcf;
            font-size: 1.1rem;
            padding: 8px 28px;
            border-radius: 48px;
            cursor: pointer;
            transition: all 0.2s;
            font-weight: bold;
            font-family: inherit;
        }

        .nav-btn:hover {
            background: #b87c3e;
            color: white;
        }

        .dot-group {
            display: flex;
            gap: 14px;
            background: rgba(0, 0, 0, 0.3);
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

        .book-spine-effect {
            position: absolute;
            left: -6px;
            top: 12px;
            width: 12px;
            height: calc(100% - 24px);
            background: #dbb062;
            border-radius: 4px;
            opacity: 0.8;
            z-index: 6;
        }

        /* 响应式 保证封面和内页大小完全一致 */
        @media (max-width: 800px) {
            .cover-container, .spread {
                min-height: 540px;
            }
            .left-page, .right-page {
                padding: 18px 14px;
                max-height: 65vh;
            }
            .greeting-title {
                font-size: 1.3rem;
            }
            .message-text {
                font-size: 0.85rem;
            }
            .cover-title {
                font-size: 2rem;
            }
        }

        @media (max-width: 600px) {
            .cover-title {
                font-size: 1.7rem;
                letter-spacing: 2px;
            }
            .greeting-title {
                font-size: 1.1rem;
            }
        }

        /* 翻页动画过渡 */
        .fade-transition {
            transition: opacity 0.25s, transform 0.3s;
        }
    </style>
</head>
<body>
<div id="star-bg"></div>
<div class="global-book-container">
    <div class="book-wrapper">
        <div class="book-spine-effect"></div>
        <div class="book" id="bookRoot">
            <!-- 动态视图：封面 或 内页spread -->
            <div id="dynamicView" class="book-viewport"></div>
        </div>
        <!-- 底部导航（打开书本后显示，封面时隐藏或显示hint，设计为打开才出现） -->
        <div id="navControls" class="nav-controls" style="display: none;">
            <button class="nav-btn" id="prevBtn">◀ 上一页</button>
            <div class="dot-group" id="dotGroup"></div>
            <button class="nav-btn" id="nextBtn">下一页 ▶</button>
        </div>
    </div>
</div>

<script>
    // --------------------------------------------------------------
    // 星空背景生成
    (function initStars() {
        const starContainer = document.getElementById('star-bg');
        const starCount = 260;
        for (let i = 0; i < starCount; i++) {
            const star = document.createElement('div');
            star.classList.add('star');
            const size = Math.random() * 4 + 1.5;
            star.style.width = size + 'px';
            star.style.height = size + 'px';
            star.style.left = Math.random() * 100 + '%';
            star.style.top = Math.random() * 100 + '%';
            star.style.animationDuration = (Math.random() * 3 + 1.8) + 's';
            star.style.animationDelay = Math.random() * 4 + 's';
            star.style.opacity = Math.random() * 0.7 + 0.3;
            starContainer.appendChild(star);
        }
    })();

    // ======================== 📖 书本数据配置区域 ========================
    // 说明：这里是您增加或删减页面的核心位置。每一个对象代表一个“跨页”（左右两页）。
    // 增加页面：在 spreadsData 数组里 push 新对象，按照 left / right 格式填写即可。
    // 注意视频路径请填写您自己的 mp4 相对路径或者网络地址，如果视频不存在会有优雅占位。
    // 目前一共配置了 6 个跨页（即12个单页），加上封面共展示纪念册。您可以根据需求直接修改或新增。
    // 为了实现“一共11页（单页）”？严格说跨页是左右双页，为了满足您“总共11页单页”不容易奇偶，
    // 但您可以自由增删跨页数量，以下默认 5个跨页 = 10个单页 + 封面足够丰富。如需要更多直接在下面追加。
    // 我们准备了示例跨页 6个 (12单页)，您可自行删除或新增，非常方便。
    
    const spreadsData = [
        { // 跨页 1
            left: { title: "✨ 半周年快乐 ✨", message: "琴师，开启了一把神秘的钥匙。之后的每一天都像星星在夜空发光。谢谢你让我明白温柔的意义，这是属于我们的第一个半周年，未来还有更多故事。", videoSrc: "videos/half-left.mp4", caption: "最初相遇时的星光" },
            right: { title: "💖 抽象永不过时", message: "臣退了，这一退，就是一辈子。", videoSrc: "videos/half-right.mp4", caption: "那些温暖的小碎片" }
        },
        { // 跨页 2
            left: { title: "📖 奇怪的音效增加了", message: "曹老板和暮光星灵来此做客", videoSrc: "videos/memory-left.mp4", caption: "偷偷记录的心动" },
            right: { title: "🌙 居然比唱歌难吗", message: "第一次唱跑调歌，竟然比正常唱歌要难吗？！此子实力恐怖如斯", videoSrc: "videos/memory-right.mp4", caption: "晚风与星光见证" }
        },
        { // 跨页 3
            left: { title: "🎁 专属礼物", message: "鸟想要，鸟得到，", videoSrc: "videos/star-left.mp4", caption: "爱意藏在星河里" },
            right: { title: "🎇 新的风格", message: "呦呦切克闹！", videoSrc: "videos/star-right.mp4", caption: "永恒的浪漫定格" }
               },
        { // 跨页 4  (新增示例，你可以随意修改或增删)
            left: { title: "☕ 把恶魔带向世界吧", message: "我的朋友，你应该支付我听到这段话的费用。", videoSrc: "videos/daily-left.mp4", caption: "微小而确定的幸福" },
            right: { title: "🌸 老板？嚼嚼嚼", message: "相对，那就针锋相对。", videoSrc: "videos/daily-right.mp4", caption: "四季如诗" }
        },
        { // 跨页 5
            left: { title: "🎶 奇怪，我的运气加到哪里去了", message: "有谁愿意帮我洗个袜子吗？", videoSrc: "videos/music-left.mp4", caption: "属于我们的歌单" },
            right: { title: "🏆 语言小天才", message: "叽里哇啦叽里哇啦。", videoSrc: "videos/music-right.mp4", caption: "与你同行" }
        },
        { // 跨页 6 再增加一个，共6个跨页=12个内页，满足丰富度，你可以减至任意数量
            left: { title: "🌌 无垠星空", message: "宇宙浩瀚，而你是我唯一的轨道。半周年不是终点，而是永恒星图的起点。", videoSrc: "videos/space-left.mp4", caption: "银河之约" },
            right: { title: "🔮 永恒誓约", message: "愿每一颗流星都承载着我对你的祝福。爱你，不止半周年。", videoSrc: "videos/space-right.mp4", caption: "星光不负赶路人" }
        }
    ];
    // ------------------- 您可在此继续增加新的跨页对象，上方已经包含6个跨页(12个单页) -------------
    
    // 当前状态管理
    let isBookOpen = false;       // 是否打开书本（封面已翻开进入内页模式）
    let currentSpreadIndex = 0;   // 当前跨页索引
    const totalSpreads = spreadsData.length;
    
    // DOM 元素
    const dynamicView = document.getElementById('dynamicView');
    const navControls = document.getElementById('navControls');
    let leftContainer, rightContainer, spreadElement; // 动态引用
    
    // 辅助函数：创建视频元素（含占位逻辑）
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
        video.onerror = () => {
            wrapper.style.background = "#2e2a1f";
            wrapper.style.display = "flex";
            wrapper.style.flexDirection = "column";
            wrapper.style.alignItems = "center";
            wrapper.style.justifyContent = "center";
            wrapper.style.borderRadius = "24px";
            wrapper.innerHTML = `<div style="text-align:center; color:#f5e2b0; padding:20px;">✨ 星空影像 ✨<br><span style="font-size:12px;">🎬 视频待放入</span><br><span style="font-size:11px;">请将视频文件放入指定路径</span></div>`;
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
    
    // 渲染单个页面内容
    function renderPageContent(container, pageData) {
        container.innerHTML = '';
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
        starDust.style.marginTop = '18px';
        starDust.style.fontSize = '18px';
        starDust.style.letterSpacing = '4px';
        starDust.style.opacity = '0.5';
        starDust.innerHTML = '✧  ⋆  ✦  ⋆  ✧';
        container.appendChild(starDust);
    }
    
    // 渲染当前跨页 (内页模式)
    function renderSpread() {
        if (!spreadElement) return;
        const data = spreadsData[currentSpreadIndex];
        if (!data) return;
        const leftPageDiv = spreadElement.querySelector('.left-page');
        const rightPageDiv = spreadElement.querySelector('.right-page');
        if (leftPageDiv && rightPageDiv) {
            renderPageContent(leftPageDiv, data.left);
            renderPageContent(rightPageDiv, data.right);
        }
        updateDotsActive();
    }
    
    // 更新圆点高亮
    function updateDotsActive() {
        const dots = document.querySelectorAll('.dot');
        dots.forEach((dot, idx) => {
            if (idx === currentSpreadIndex) dot.classList.add('active');
            else dot.classList.remove('active');
        });
    }
    
    // 构建底部圆点导航
    function buildDots() {
        const dotGroup = document.getElementById('dotGroup');
        if (!dotGroup) return;
        dotGroup.innerHTML = '';
        for (let i = 0; i < totalSpreads; i++) {
            const dot = document.createElement('div');
            dot.classList.add('dot');
            if (i === currentSpreadIndex) dot.classList.add('active');
            dot.addEventListener('click', () => {
                if (isBookOpen && i !== currentSpreadIndex) {
                    goToSpread(i);
                }
            });
            dotGroup.appendChild(dot);
        }
    }
    
    // 内页翻带动画
    function goToSpread(newIndex) {
        if (!isBookOpen) return;
        if (newIndex === currentSpreadIndex) return;
        if (newIndex < 0 || newIndex >= totalSpreads) return;
        if (spreadElement) {
            spreadElement.style.transition = 'opacity 0.2s ease, transform 0.25s';
            spreadElement.style.opacity = '0';
            spreadElement.style.transform = 'scale(0.98)';
        }
        setTimeout(() => {
            currentSpreadIndex = newIndex;
            renderSpread();
            if (spreadElement) {
                spreadElement.style.opacity = '1';
                spreadElement.style.transform = 'scale(1)';
                setTimeout(() => {
                    if (spreadElement) spreadElement.style.transition = '';
                }, 280);
            }
            updateDotsActive();
        }, 180);
    }
    
    function nextPageInner() {
        if (!isBookOpen) return;
        if (currentSpreadIndex < totalSpreads - 1) {
            goToSpread(currentSpreadIndex + 1);
        } else {
            if (spreadElement) {
                spreadElement.style.transform = 'translateX(-6px)';
                setTimeout(() => { if(spreadElement) spreadElement.style.transform = ''; }, 200);
            }
        }
    }
    
    function prevPageInner() {
        if (!isBookOpen) return;
        if (currentSpreadIndex > 0) {
            goToSpread(currentSpreadIndex - 1);
        } else {
            if (spreadElement) {
                spreadElement.style.transform = 'translateX(6px)';
                setTimeout(() => { if(spreadElement) spreadElement.style.transform = ''; }, 200);
            }
        }
    }
    
    // 构建内页视图 (跨页结构)
    function buildSpreadView() {
        const spreadDiv = document.createElement('div');
        spreadDiv.className = 'spread';
        const leftDiv = document.createElement('div');
        leftDiv.className = 'left-page';
        const rightDiv = document.createElement('div');
        rightDiv.className = 'right-page';
        spreadDiv.appendChild(leftDiv);
        spreadDiv.appendChild(rightDiv);
        return { spreadDiv, leftDiv, rightDiv };
    }
    
    // 核心：从封面打开书本 (优雅翻页过渡)
    function openBook() {
        if (isBookOpen) return;
        // 开始翻开动画：模拟翻页效果
        const coverElement = dynamicView.querySelector('.cover-container');
        if (!coverElement) return;
        // 淡出并缩小封面
        coverElement.style.transition = 'opacity 0.35s ease, transform 0.4s cubic-bezier(0.2, 0.9, 0.6, 1.1)';
        coverElement.style.opacity = '0';
        coverElement.style.transform = 'rotateY(-30deg) scale(0.9)';
        setTimeout(() => {
            // 构建内页跨页
            const { spreadDiv, leftDiv, rightDiv } = buildSpreadView();
            spreadElement = spreadDiv;
            leftContainer = leftDiv;
            rightContainer = rightDiv;
            dynamicView.innerHTML = '';
            dynamicView.appendChild(spreadDiv);
            // 初始渲染数据
            currentSpreadIndex = 0;
            renderSpread();  // 填充内容
            // 让内页渐入
            spreadDiv.style.opacity = '0';
            spreadDiv.style.transform = 'scale(0.98)';
            setTimeout(() => {
                spreadDiv.style.transition = 'opacity 0.3s ease, transform 0.3s';
                spreadDiv.style.opacity = '1';
                spreadDiv.style.transform = 'scale(1)';
                isBookOpen = true;
                navControls.style.display = 'flex';
                // 重新绑定底部按钮事件
                document.getElementById('prevBtn').onclick = () => prevPageInner();
                document.getElementById('nextBtn').onclick = () => nextPageInner();
                buildDots();
                updateDotsActive();
                // 触摸滑动绑定
                bindTouchSwipe();
                // 键盘绑定
                bindKeyboard();
            }, 50);
        }, 220);
    }
    
    // 触摸滑动
    let touchStartX = 0;
    function bindTouchSwipe() {
        if (!spreadElement) return;
        spreadElement.removeEventListener('touchstart', touchStartHandler);
        spreadElement.removeEventListener('touchend', touchEndHandler);
        spreadElement.addEventListener('touchstart', touchStartHandler, { passive: true });
        spreadElement.addEventListener('touchend', touchEndHandler);
    }
    function touchStartHandler(e) {
        touchStartX = e.changedTouches[0].screenX;
    }
    function touchEndHandler(e) {
        const diff = e.changedTouches[0].screenX - touchStartX;
        if (Math.abs(diff) > 50) {
            if (diff > 0) prevPageInner();
            else nextPageInner();
        }
    }
    function bindKeyboard() {
        const handler = (e) => {
            if (!isBookOpen) return;
            if (e.key === 'ArrowLeft') { e.preventDefault(); prevPageInner(); }
            else if (e.key === 'ArrowRight') { e.preventDefault(); nextPageInner(); }
        };
        window.removeEventListener('keydown', window._keyHandler);
        window._keyHandler = handler;
        window.addEventListener('keydown', handler);
    }
    
    // 构建封面 (合上的书本)
    function buildCover() {
        const coverDiv = document.createElement('div');
        coverDiv.className = 'cover-container';
        coverDiv.innerHTML = `
            <div class="cover-star">✨ 🎀 ✨</div>
            <div class="cover-title">半周年快乐</div>
            <div class="cover-sub">· 我们的星空手账 ·</div>
            <div class="open-hint">⭐ 轻触翻开 · 星河流转 ⭐</div>
            <div style="margin-top: 20px; font-size: 0.8rem; letter-spacing:1px;">📖 纪念相识第183个夜晚</div>
        `;
        coverDiv.addEventListener('click', openBook);
        dynamicView.innerHTML = '';
        dynamicView.appendChild(coverDiv);
        isBookOpen = false;
        navControls.style.display = 'none';
    }
    
    // 鼠标悬浮书本3D效果
    const bookRoot = document.getElementById('bookRoot');
    if (bookRoot) {
        bookRoot.addEventListener('mousemove', (e) => {
            const rect = bookRoot.getBoundingClientRect();
            const x = (e.clientX - rect.left) / rect.width - 0.5;
            const y = (e.clientY - rect.top) / rect.height - 0.5;
            bookRoot.style.transform = `perspective(2000px) rotateX(${y * 1.2}deg) rotateY(${x * 2.5}deg)`;
        });
        bookRoot.addEventListener('mouseleave', () => {
            bookRoot.style.transform = '';
        });
    }
    
    // 初始加载封面
    buildCover();
    // 确保整体视口自适应，保持封面和内页大小统一（由于都在同一个容器内，宽高一致自然完美）
</script>
</body>
</html>
