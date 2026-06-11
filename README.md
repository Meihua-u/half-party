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
            overflow-y: auto;
            overflow-x: hidden;
        }

        /* 闪烁星星背景 */
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

        .book-wrapper {
            perspective: 2000px;
            width: 1200px;
            max-width: 95vw;
            height: auto;
            min-height: 620px;
            transition: all 0.2s;
            position: relative;
        }

        .book {
            width: 100%;
            position: relative;
            transition: transform 0.2s ease;
            border-radius: 20px;
        }

        .book-viewport {
            width: 100%;
            background: transparent;
            border-radius: 20px;
            transition: all 0.35s cubic-bezier(0.2, 0.9, 0.4, 1.1);
        }

        /* 封面样式 */
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

        /* 内页跨页样式 */
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
            background: #fffcf0;
            overflow-y: auto;
            scrollbar-width: thin;
            max-height: 70vh;
            /* 确保内部元素排列紧凑且视频区域位置相对稳定 */
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

        /* 标题样式 */
        .greeting-title {
            font-size: 1.8rem;
            font-weight: 700;
            background: linear-gradient(135deg, #b85c1a, #7b3e10);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 12px;
            border-left: 5px solid #ffb347;
            padding-left: 18px;
        }

        /* 装饰线 */
        .deco-line {
            height: 2px;
            background: linear-gradient(90deg, #f7d98c, #c8a86b, #f7d98c);
            width: 60px;
            margin: 6px 0 12px 0;
        }

        /* 消息文本区域 —— 固定最小高度+最大高度，滚动处理，防止视频区域过度上下漂移 */
        .message-text {
            font-size: 1rem;
            line-height: 1.6;
            color: #2c3e2f;
            background: rgba(248, 240, 218, 0.7);
            padding: 14px 18px;
            border-radius: 28px;
            margin: 8px 0 14px 0;
            font-weight: 500;
            box-shadow: inset 0 0 0 1px #fff9ef, 0 6px 14px rgba(0, 0, 0, 0.04);
            /* 关键优化：固定视频垂直位置，限制文本高度范围 */
            min-height: 85px;      /* 至少保证2~3行高度，减少视频位置波动 */
            max-height: 130px;     /* 超出则滚动，不会无限撑开 */
            overflow-y: auto;
            scrollbar-width: thin;
        }
        .message-text::-webkit-scrollbar {
            width: 4px;
        }
        .message-text::-webkit-scrollbar-track {
            background: #e7ddca;
            border-radius: 10px;
        }
        .message-text::-webkit-scrollbar-thumb {
            background: #bc9468;
            border-radius: 10px;
        }

        /* 视频容器 —— 放大显示区域 & 固定比例尺寸，更醒目 */
        .video-box {
            background: #1e1b14;
            border-radius: 28px;
            overflow: hidden;
            margin: 6px 0 12px 0;
            box-shadow: 0 14px 24px rgba(0, 0, 0, 0.25), inset 0 1px 2px rgba(255, 245, 200, 0.2);
            /* 从 16/9 放大为 4/3  (视觉上更高，内容更突出) */
            aspect-ratio: 4 / 3;
            width: 100%;
            transition: transform 0.2s ease;
            cursor: pointer;
        }
        .video-box:hover {
            transform: scale(0.99);
        }
        .video-box video {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: block;
        }
        /* 占位符/错误提示也保持同样比例，稳定占位 */
        .video-placeholder {
            background: #2e2a1f;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            text-align: center;
            width: 100%;
            height: 100%;
            color: #f5e2b0;
            font-size: 0.9rem;
            border-radius: 24px;
            backdrop-filter: blur(2px);
        }

        .caption {
            font-size: 0.8rem;
            text-align: center;
            margin-top: 6px;
            margin-bottom: 4px;
            color: #a37242;
            font-weight: 500;
            letter-spacing: 1px;
        }

        /* 底部星尘装饰 */
        .star-dust {
            text-align: center;
            margin-top: 18px;
            font-size: 18px;
            letter-spacing: 4px;
            opacity: 0.5;
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

        /* 响应式优化 */
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
                margin-bottom: 6px;
            }
            .message-text {
                font-size: 0.85rem;
                min-height: 70px;
                max-height: 110px;
                padding: 10px 14px;
            }
            .cover-title {
                font-size: 2rem;
            }
            .video-box {
                aspect-ratio: 4 / 3;
                margin: 8px 0 10px;
            }
        }

        @media (max-width: 600px) {
            .cover-title {
                font-size: 1.7rem;
                letter-spacing: 2px;
            }
            .greeting-title {
                font-size: 1.1rem;
                padding-left: 12px;
            }
            .message-text {
                min-height: 65px;
                max-height: 100px;
                font-size: 0.8rem;
            }
            .video-box {
                border-radius: 20px;
            }
        }

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
            <div id="dynamicView" class="book-viewport"></div>
        </div>
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
    // 跨页数据配置 (每一个对象代表打开书后的一个左右跨页)
    // 您可以自由增删跨页，每个跨页包含 left / right 内容，支持视频显示区域统一且稳定
    const spreadsData = [
        { 
            left: { title: "✨ 半周年快乐 ✨", message: "琴师，开启了一把神秘的钥匙。之后的每一天都像星星在夜空发光。", videoSrc: "videos/half-left.mp4", caption: "最初相遇时的星光" },
            right: { title: "💖 抽象永不过时", message: "臣退了，这一退，就是一辈子。但星光会永远记得笑容。", videoSrc: "videos/half-right.mp4", caption: "那些温暖的小碎片" }
        },
        { 
            left: { title: "📖 奇怪的音效增加了", message: "曹老板和暮光星灵来此做客，空气里都是魔性的笑声✨", videoSrc: "videos/memory-left.mp4", caption: "偷偷记录的心动" },
            right: { title: "🌙 居然比唱歌难吗", message: "第一次唱跑调歌，竟然比正常唱歌要难吗？！此子实力恐怖如斯！", videoSrc: "videos/memory-right.mp4", caption: "晚风与星光见证" }
        },
        { 
            left: { title: "🎁 专属礼物", message: "鸟想要，鸟得到，爱意藏在星河的每个角落里。", videoSrc: "videos/star-left.mp4", caption: "星尘礼物盒" },
            right: { title: "🎇 新的风格", message: "呦呦切克闹！旋律和心跳同频共振，浪漫永不逾期。", videoSrc: "videos/star-right.mp4", caption: "永恒的浪漫定格" }
        },
        { 
            left: { title: "☕ 把恶魔带向世界吧", message: "我的朋友，你应该支付我听到这段话的费用。——不过半周年，免费赠你星河万里。", videoSrc: "videos/daily-left.mp4", caption: "微小而确定的幸福" },
            right: { title: "🌸 老板？嚼嚼嚼", message: "相对，那就针锋相对。但温柔，永远留给你。", videoSrc: "videos/daily-right.mp4", caption: "四季如诗" }
        },
        { 
            left: { title: "🎶 奇怪，我的运气加到哪里去了", message: "有谁愿意帮我洗个袜子吗？奖励一段私人星空漫游✨", videoSrc: "videos/music-left.mp4", caption: "属于我们的歌单" },
            right: { title: "🏆 语言小天才", message: "叽里哇啦叽里哇啦。宇宙暗号解码完毕，今日份快乐发送成功！", videoSrc: "videos/music-right.mp4", caption: "与你同行" }
        },
        { 
            left: { title: "🌌 无垠星空", message: "宇宙浩瀚，而你是我唯一的轨道。半周年不是终点，而是永恒星图的起点。", videoSrc: "videos/space-left.mp4", caption: "银河之约" },
            right: { title: "🔮 永恒誓约", message: "愿每一颗流星都承载着我对你的祝福。爱你，不止半周年。星光永伴。", videoSrc: "videos/space-right.mp4", caption: "星光不负赶路人" }
        }
    ];
    
    // 当前状态
    let isBookOpen = false;
    let currentSpreadIndex = 0;
    const totalSpreads = spreadsData.length;
    
    const dynamicView = document.getElementById('dynamicView');
    const navControls = document.getElementById('navControls');
    let spreadElement = null;   // 当前跨页DOM
    
    // 创建视频组件 (保证大小一致、占位区域固定比例)
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
        
        // 视频加载失败时的优雅降级 —— 保持相同比例和视觉美感
        video.onerror = () => {
            // 清空wrapper，构建同等比例的占位内容，确保视频区域不会塌陷，位置稳定
            wrapper.innerHTML = '';
            wrapper.style.background = "#2e2a1f";
            wrapper.style.display = "flex";
            wrapper.style.alignItems = "center";
            wrapper.style.justifyContent = "center";
            wrapper.style.flexDirection = "column";
            const placeholderDiv = document.createElement('div');
            placeholderDiv.className = 'video-placeholder';
            placeholderDiv.innerHTML = `<div style="font-size:1.2rem;">✨ 星空影像 ✨</div><div style="font-size:0.75rem; margin-top:6px;">🎬 即将降临</div><div style="font-size:0.65rem; margin-top:4px;">请将视频放入指定路径</div>`;
            wrapper.appendChild(placeholderDiv);
            // 仍然保留 caption
            const captionDiv = document.createElement('div');
            captionDiv.className = 'caption';
            captionDiv.innerText = captionText || '♡ 浪漫待加载 ♡';
            wrapper.appendChild(captionDiv);
        };
        
        // 正常加载时添加视频和说明
        video.oncanplay = () => {
            wrapper.innerHTML = '';
            wrapper.appendChild(video);
            const captionDiv = document.createElement('div');
            captionDiv.className = 'caption';
            captionDiv.innerText = captionText || '♡ 珍藏片段 ♡';
            wrapper.appendChild(captionDiv);
        };
        
        // 如果视频立刻能加载成功，提前触发一次内容构建
        if (video.readyState >= 2) {
            wrapper.innerHTML = '';
            wrapper.appendChild(video);
            const captionDiv = document.createElement('div');
            captionDiv.className = 'caption';
            captionDiv.innerText = captionText || '♡ 珍藏片段 ♡';
            wrapper.appendChild(captionDiv);
        } else {
            // 临时占位避免闪动，稍后替换
            wrapper.style.display = "flex";
            wrapper.style.alignItems = "center";
            wrapper.style.justifyContent = "center";
            wrapper.style.backgroundColor = "#2e2a1f";
            const tempSpan = document.createElement('div');
            tempSpan.style.color = "#f5e2b0";
            tempSpan.innerText = "✨ 星轨读取中 ✨";
            wrapper.appendChild(tempSpan);
            // 异步实际渲染由video的canplay或error接管，为防止覆盖过多，使用一次替换机会
            const replaceContent = () => {
                if (video.parentNode === wrapper) return;
                wrapper.innerHTML = '';
                wrapper.appendChild(video);
                const captionDiv = document.createElement('div');
                captionDiv.className = 'caption';
                captionDiv.innerText = captionText || '♡ 珍藏片段 ♡';
                wrapper.appendChild(captionDiv);
                video.removeEventListener('canplay', replaceContent);
                video.removeEventListener('error', errorFallback);
            };
            const errorFallback = () => {
                wrapper.innerHTML = '';
                wrapper.style.background = "#2e2a1f";
                wrapper.style.display = "flex";
                wrapper.style.alignItems = "center";
                wrapper.style.justifyContent = "center";
                wrapper.style.flexDirection = "column";
                const errDiv = document.createElement('div');
                errDiv.className = 'video-placeholder';
                errDiv.innerHTML = `<div>✨ 星空影像 ✨</div><div style="font-size:0.7rem;">🎬 视频待放入</div>`;
                wrapper.appendChild(errDiv);
                const captionDiv = document.createElement('div');
                captionDiv.className = 'caption';
                captionDiv.innerText = captionText || '♡ 浪漫待续 ♡';
                wrapper.appendChild(captionDiv);
                video.removeEventListener('canplay', replaceContent);
                video.removeEventListener('error', errorFallback);
            };
            video.addEventListener('canplay', replaceContent, { once: true });
            video.addEventListener('error', errorFallback, { once: true });
        }
        return wrapper;
    }
    
    // 渲染单个页面 (左侧或右侧)
    function renderPageContent(container, pageData) {
        container.innerHTML = '';
        // 标题
        const title = document.createElement('h2');
        title.className = 'greeting-title';
        title.innerText = pageData.title || '✨ 珍藏时刻 ✨';
        container.appendChild(title);
        // 装饰线
        const deco = document.createElement('div');
        deco.className = 'deco-line';
        container.appendChild(deco);
        // 消息文本 (已经通过CSS min/max-height稳定区域)
        const msgBox = document.createElement('div');
        msgBox.className = 'message-text';
        msgBox.innerText = pageData.message || '愿所有星光奔向你。';
        container.appendChild(msgBox);
        
        // 视频区域 (稳定大小 & 固定相对位置)
        if (pageData.videoSrc) {
            const videoWidget = createVideoElement(pageData.videoSrc, pageData.caption || '♡ 你的故事 ♡');
            container.appendChild(videoWidget);
        } else {
            // 无视频时同样保证固定比例占位，防止起伏
            const staticPlaceholder = document.createElement('div');
            staticPlaceholder.className = 'video-box';
            staticPlaceholder.style.background = "#efe2cc";
            staticPlaceholder.style.display = "flex";
            staticPlaceholder.style.flexDirection = "column";
            staticPlaceholder.style.alignItems = "center";
            staticPlaceholder.style.justifyContent = "center";
            staticPlaceholder.innerHTML = `<div style="font-size:1rem; color:#956e3e;">⭐ 星空映像馆 ⭐</div><div style="font-size:0.7rem; margin-top:6px;">浪漫影像即将呈现</div>`;
            container.appendChild(staticPlaceholder);
            if (pageData.caption) {
                const cap = document.createElement('div');
                cap.className = 'caption';
                cap.innerText = pageData.caption;
                container.appendChild(cap);
            } else {
                const defaultCap = document.createElement('div');
                defaultCap.className = 'caption';
                defaultCap.innerText = '✨ 星河待启 ✨';
                container.appendChild(defaultCap);
            }
        }
        // 底部星星装饰 (为增强稳定感)
        const starDust = document.createElement('div');
        starDust.className = 'star-dust';
        starDust.innerHTML = '✧  ⋆  ✦  ⋆  ✧';
        container.appendChild(starDust);
    }
    
    // 渲染当前跨页
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
    
    function updateDotsActive() {
        const dots = document.querySelectorAll('.dot');
        dots.forEach((dot, idx) => {
            if (idx === currentSpreadIndex) dot.classList.add('active');
            else dot.classList.remove('active');
        });
    }
    
    function buildDots() {
        const dotGroup = document.getElementById('dotGroup');
        if (!dotGroup) return;
        dotGroup.innerHTML = '';
        for (let i = 0; i < totalSpreads; i++) {
            const dot = document.createElement('div');
            dot.classList.add('dot');
            if (i === currentSpreadIndex) dot.classList.add('active');
            dot.addEventListener('click', () => {
                if (isBookOpen && i !== currentSpreadIndex) goToSpread(i);
            });
            dotGroup.appendChild(dot);
        }
    }
    
    function goToSpread(newIndex) {
        if (!isBookOpen) return;
        if (newIndex === currentSpreadIndex || newIndex < 0 || newIndex >= totalSpreads) return;
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
    
    // 打开书本，翻开动画
    function openBook() {
        if (isBookOpen) return;
        const coverElement = dynamicView.querySelector('.cover-container');
        if (!coverElement) return;
        coverElement.style.transition = 'opacity 0.35s ease, transform 0.4s cubic-bezier(0.2, 0.9, 0.6, 1.1)';
        coverElement.style.opacity = '0';
        coverElement.style.transform = 'rotateY(-30deg) scale(0.9)';
        setTimeout(() => {
            const { spreadDiv, leftDiv, rightDiv } = buildSpreadView();
            spreadElement = spreadDiv;
            dynamicView.innerHTML = '';
            dynamicView.appendChild(spreadDiv);
            currentSpreadIndex = 0;
            renderSpread();
            spreadDiv.style.opacity = '0';
            spreadDiv.style.transform = 'scale(0.98)';
            setTimeout(() => {
                spreadDiv.style.transition = 'opacity 0.3s ease, transform 0.3s';
                spreadDiv.style.opacity = '1';
                spreadDiv.style.transform = 'scale(1)';
                isBookOpen = true;
                navControls.style.display = 'flex';
                document.getElementById('prevBtn').onclick = () => prevPageInner();
                document.getElementById('nextBtn').onclick = () => nextPageInner();
                buildDots();
                updateDotsActive();
                bindTouchSwipe();
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
    
    // 构建封面
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
    
    // 书本3D倾斜效果
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
    
    buildCover();
</script>
</body>
</html>
