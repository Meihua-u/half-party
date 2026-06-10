<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
    <title>半周年礼物 · 星空手账 · 珍藏视频集</title>
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

        /* ---------- 动态闪烁星星背景 (一闪一闪亮晶晶) ---------- */
        .star {
            position: absolute;
            background-color: #ffffff;
            border-radius: 50%;
            box-shadow: 0 0 6px rgba(255, 255, 255, 0.9);
            animation: twinkle 2.2s infinite alternate ease-in-out;
            pointer-events: none;
            z-index: 0;
        }

        @keyframes twinkle {
            0% { opacity: 0.15; transform: scale(0.5); }
            100% { opacity: 1; transform: scale(1.3); box-shadow: 0 0 12px #fff8e0; }
        }

        /* 大星星偶尔划过 */
        .shooting-star {
            position: absolute;
            width: 2px;
            height: 2px;
            background: white;
            border-radius: 50%;
            box-shadow: 0 0 8px #fff;
            animation: shoot 4s linear infinite;
            opacity: 0;
            z-index: 1;
        }

        @keyframes shoot {
            0% { transform: translateX(0) translateY(0); opacity: 1; width: 2px; height: 2px; }
            70% { opacity: 0.8; }
            100% { transform: translateX(-300px) translateY(200px); opacity: 0; width: 0px; height: 0px; }
        }

        /* ---------- 横板书本容器 (固定位置，不偏移) ---------- */
        .book-wrapper {
            perspective: 1800px;
            width: 1300px;
            max-width: 92vw;
            height: 700px;
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
            transition: transform 0.3s ease-out;
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
            padding: 24px 22px;
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
            font-size: 1.7rem;
            font-weight: 700;
            background: linear-gradient(135deg, #b85c1a, #7b3e10);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            margin-bottom: 12px;
            letter-spacing: 1px;
            border-left: 5px solid #ffb347;
            padding-left: 16px;
        }

        /* 文字寄语框 */
        .message-text {
            font-size: 0.95rem;
            line-height: 1.65;
            color: #2c3e2f;
            background: rgba(248, 240, 218, 0.7);
            padding: 14px 16px;
            border-radius: 28px;
            margin: 12px 0;
            font-weight: 500;
            box-shadow: inset 0 0 0 1px #fff9ef, 0 6px 12px rgba(0, 0, 0, 0.04);
        }

        /* 视频容器 */
        .video-box {
            background: #1e1b14;
            border-radius: 20px;
            overflow: hidden;
            margin: 12px 0 6px 0;
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
            font-size: 0.8rem;
            text-align: center;
            margin-top: 6px;
            color: #a37242;
            font-weight: 500;
            letter-spacing: 1px;
        }

        /* 装饰细线 */
        .deco-line {
            height: 2px;
            background: linear-gradient(90deg, #f7d98c, #c8a86b, #f7d98c);
            width: 60px;
            margin: 6px 0 6px 0;
        }

        /* 底部导航栏 */
        .nav-controls {
            position: absolute;
            bottom: -75px;
            left: 0;
            width: 100%;
            display: flex;
            justify-content: center;
            gap: 28px;
            align-items: center;
            z-index: 20;
        }

        .nav-btn {
            background: rgba(25, 20, 35, 0.85);
            backdrop-filter: blur(8px);
            border: 1px solid rgba(255, 215, 150, 0.7);
            color: #ffefcf;
            font-size: 1.2rem;
            padding: 6px 26px;
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
            background: #b9a077;
            transition: all 0.2s;
            cursor: pointer;
        }

        .dot.active {
            background: #ffc485;
            transform: scale(1.35);
            box-shadow: 0 0 8px #ffbc6e;
        }

        /* 书脊装饰 */
        .book-spine {
            position: absolute;
            left: -10px;
            top: 12px;
            width: 18px;
            height: calc(100% - 24px);
            background: #cfa668;
            border-radius: 6px 2px 2px 6px;
            z-index: 5;
            box-shadow: inset -1px 0 4px rgba(0,0,0,0.2);
        }

        /* 手机适配 */
        @media (max-width: 900px) {
            .book-wrapper {
                height: 620px;
            }
            .left-page, .right-page {
                padding: 16px 14px;
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
                font-size: 0.9rem;
                padding: 5px 18px;
            }
        }

        @media (max-width: 650px) {
            .book-wrapper {
                height: 560px;
            }
            .greeting-title {
                font-size: 1.1rem;
            }
            .message-text {
                font-size: 0.75rem;
            }
            .left-page, .right-page {
                padding: 12px 10px;
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
        // ======================== 1. 动态闪烁星星 + 流星 ========================
        (function initStars() {
            const starContainer = document.getElementById('star-bg');
            // 增加星星数量，更加璀璨
            const starCount = 320;
            for (let i = 0; i < starCount; i++) {
                const star = document.createElement('div');
                star.classList.add('star');
                const size = Math.random() * 4 + 1.2;
                star.style.width = size + 'px';
                star.style.height = size + 'px';
                star.style.left = Math.random() * 100 + '%';
                star.style.top = Math.random() * 100 + '%';
                const duration = Math.random() * 3 + 1.6;
                star.style.animationDuration = duration + 's';
                star.style.animationDelay = Math.random() * 5 + 's';
                star.style.opacity = Math.random() * 0.8 + 0.2;
                starContainer.appendChild(star);
            }
            // 添加几颗流星效果 (增加梦幻感)
            for (let i = 0; i < 6; i++) {
                const meteor = document.createElement('div');
                meteor.classList.add('shooting-star');
                meteor.style.top = Math.random() * 40 + '%';
                meteor.style.left = Math.random() * 70 + 20 + '%';
                meteor.style.animationDelay = Math.random() * 8 + 's';
                meteor.style.animationDuration = Math.random() * 3 + 2.5 + 's';
                starContainer.appendChild(meteor);
            }
        })();

        // ======================== 2. 书本数据 - 扩充至 20 个视频 (10个跨页，每个跨页左右各一个视频) ========================
        // 为了让你能快速放入 20 个视频，这里预先构建 10 个跨页，每个跨页包含左右两页。
        // 你只需要将 videoSrc 替换成你自己的视频路径（例如 "videos/1.mp4"），以及自定义标题和寄语。
        // 视频文件建议放在仓库的 "videos" 文件夹下。
        
        const spreadsData = [
            { // 跨页1 
                left: { title: "🎬 我们的初见", message: "还记得那一天吗？星光落在你肩上，故事悄悄开始。", videoSrc: "videos/video_01.mp4", caption: "✨ 初遇时的星光" },
                right: { title: "💌 心动瞬间", message: "你笑起来的样子，比星河还温柔。", videoSrc: "videos/video_02.mp4", caption: "🌟 心动定格" }
            },
            { // 跨页2
                left: { title: "📸 快乐碎片", message: "那些一起大笑、一起发呆的日子，闪闪发光。", videoSrc: "videos/video_03.mp4", caption: "🎉 欢乐时光" },
                right: { title: "🌙 晚安日记", message: "每晚睡前都会想起你，像星星准时亮起。", videoSrc: "videos/video_04.mp4", caption: "🌠 伴你入眠" }
            },
            { // 跨页3
                left: { title: "🍃 微风与甜", message: "和你走过的每一条路，都开满花。", videoSrc: "videos/video_05.mp4", caption: "🌸 温柔陪伴" },
                right: { title: "🎁 专属浪漫", message: "你是宇宙赠予我的独一无二的礼物。", videoSrc: "videos/video_06.mp4", caption: "💝 半周年快乐" }
            },
            { // 跨页4
                left: { title: "🌟 星海漫游", message: "想和你一起，把银河系所有浪漫都经历一遍。", videoSrc: "videos/video_07.mp4", caption: "🚀 星辰大海" },
                right: { title: "📖 记忆手账", message: "每一页都写满你的名字，和我的心跳。", videoSrc: "videos/video_08.mp4", caption: "💫 专属回忆" }
            },
            { // 跨页5
                left: { title: "🎵 旋律记忆", message: "耳机分你一半，心跳也分你一半。", videoSrc: "videos/video_09.mp4", caption: "🎧 我们的歌" },
                right: { title: "🌈 彩色未来", message: "未来的风景，想和你一起涂上喜欢的颜色。", videoSrc: "videos/video_10.mp4", caption: "🎨 永远相伴" }
            },
            { // 跨页6
                left: { title: "🏆 半周年纪念", message: "183个日夜，每一天都因你而特别。", videoSrc: "videos/video_11.mp4", caption: "🏅 珍贵纪念" },
                right: { title: "🌌 无尽星空", message: "你像星星一样，点亮我的宇宙。", videoSrc: "videos/video_12.mp4", caption: "✨ 永恒星光" }
            },
            { // 跨页7
                left: { title: "☀️ 暖阳时刻", message: "你的笑容是我每天最好的解药。", videoSrc: "videos/video_13.mp4", caption: "🌻 治愈瞬间" },
                right: { title: "🍀 幸运遇见", message: "遇见你是我这辈子最大的幸运。", videoSrc: "videos/video_14.mp4", caption: "🍀 小确幸" }
            },
            { // 跨页8
                left: { title: "💎 珍藏影像", message: "每次翻看这些片段，心里都甜甜的。", videoSrc: "videos/video_15.mp4", caption: "📀 时光胶囊" },
                right: { title: "🕯️ 约定", message: "未来很长，但我们一起走就不怕。", videoSrc: "videos/video_16.mp4", caption: "🤝 永恒约定" }
            },
            { // 跨页9
                left: { title: "🌊 海边絮语", message: "想带你去看海，把誓言说给浪花听。", videoSrc: "videos/video_17.mp4", caption: "🌊 浪漫浪潮" },
                right: { title: "🎈 放飞的梦", message: "每个梦想里都有你，你就是我的梦想。", videoSrc: "videos/video_18.mp4", caption: "🎈 自由爱意" }
            },
            { // 跨页10  总共20个视频
                left: { title: "🏔️ 山顶约定", message: "一起看过最高的星空，说过最真的誓言。", videoSrc: "videos/video_19.mp4", caption: "⛰️ 顶峰相见" },
                right: { title: "♾️ 无限爱意", message: "半周年只是起点，爱你直到宇宙尽头。", videoSrc: "videos/video_20.mp4", caption: "💖 永远未完待续" }
            }
        ];

        // ------------------ 全局变量 ------------------
        let currentIndex = 0;
        const totalSpreads = spreadsData.length;  // 总共10个跨页 = 20个视频
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
            
            // 如果视频源为空或未正确提供，显示唯美占位
            if (!videoSrc || videoSrc === "" || videoSrc === "videos/undefined.mp4") {
                wrapper.style.background = "#2e2a1f";
                wrapper.style.display = "flex";
                wrapper.style.flexDirection = "column";
                wrapper.style.alignItems = "center";
                wrapper.style.justifyContent = "center";
                wrapper.innerHTML = `
                    <div style="text-align:center; color:#f5e2b0; padding:20px;">
                        ✨ 星空映像 ✨<br>
                        <span style="font-size:12px;">🎬 等待你的视频</span><br>
                        <span style="font-size:11px;">请将视频放入 videos/ 文件夹并修改路径</span>
                    </div>
                `;
                const captionDiv = document.createElement('div');
                captionDiv.className = 'caption';
                captionDiv.innerText = captionText || '✨ 即将点亮 ✨';
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
            
            // 视频加载失败时优雅降级 (不显示错误alert，而是显示提示)
            video.onerror = () => {
                wrapper.style.background = "#2e2a1f";
                wrapper.style.display = "flex";
                wrapper.style.flexDirection = "column";
                wrapper.style.alignItems = "center";
                wrapper.style.justifyContent = "center";
                wrapper.style.borderRadius = "20px";
                wrapper.innerHTML = `
                    <div style="text-align:center; color:#f5e2b0; padding:20px;">
                        ✨ 星河映像 ✨<br>
                        <span style="font-size:12px;">🎬 视频待放入</span><br>
                        <span style="font-size:11px;">路径: ${videoSrc}</span>
                    </div>
                `;
                const cap = document.createElement('div');
                cap.className = 'caption';
                cap.innerText = captionText || '♡ 请将视频文件放入对应位置 ♡';
                wrapper.appendChild(cap);
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
            
            // 视频区域 (无论路径是什么，都创建优雅容器)
            const videoWidget = createVideoElement(pageData.videoSrc, pageData.caption || '♡ 你的故事 ♡');
            container.appendChild(videoWidget);
            
            // 底部加一点星尘装饰
            const starDust = document.createElement('div');
            starDust.style.textAlign = 'center';
            starDust.style.marginTop = '14px';
            starDust.style.fontSize = '16px';
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
        spreadEl.addEventListener('touchstart', (e) => {
            touchStartX = e.changedTouches[0].screenX;
        }, { passive: true });
        
        spreadEl.addEventListener('touchend', (e) => {
            const touchEndX = e.changedTouches[0].screenX;
            const diff = touchEndX - touchStartX;
            if (Math.abs(diff) > 50) {
                if (diff > 0) {
                    prevPage();
                } else {
                    nextPage();
                }
            }
        });
        
        // 增加微妙的鼠标倾斜效果 (增强立体感)
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
            console.log(`✨ 半周年礼物已加载 ✨ 当前跨页数量: ${totalSpreads} 个 (共 ${totalSpreads * 2} 个视频位)`);
            console.log("📌 提示: 请将您的视频文件放入 videos/ 目录，并修改 spreadsData 中的 videoSrc 路径。");
        }
        
        init();
    </script>
</body>
</html>
