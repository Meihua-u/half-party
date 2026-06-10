半周年礼物
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>给你的小礼物 ✨</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            min-height: 100vh;
            background: linear-gradient(to bottom, #0a0a23, #1a1a40, #0f0f33);
            color: white;
            font-family: "Microsoft YaHei", sans-serif;
            overflow: hidden;
            position: relative;
        }

        /* 闪烁星星背景 */
        .star {
            position: absolute;
            background: white;
            border-radius: 50%;
            animation: twinkle 2s infinite ease-in-out;
        }

        @keyframes twinkle {
            0%, 100% { opacity: 0.3; transform: scale(0.8); }
            50% { opacity: 1; transform: scale(1.2); }
        }

        /* 翻书容器 */
        .book-container {
            position: relative;
            width: 90vw;
            max-width: 800px;
            height: 80vh;
            margin: 10vh auto;
            perspective: 1500px;
        }

        .book {
            width: 100%;
            height: 100%;
            position: relative;
            transform-style: preserve-3d;
        }

        .page {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            background: rgba(15, 15, 40, 0.85);
            border-radius: 10px;
            box-shadow: 0 0 30px rgba(100, 150, 255, 0.2);
            padding: 40px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            backface-visibility: hidden;
            transform-origin: left center;
            transition: transform 1s ease-in-out;
        }

        .page h1 {
            font-size: 2rem;
            margin-bottom: 20px;
            color: #fff;
            text-shadow: 0 0 10px rgba(200, 220, 255, 0.8);
        }

        .page p {
            font-size: 1.2rem;
            line-height: 1.8;
            text-align: center;
            color: #e0e0ff;
        }

        .page video {
            max-width: 100%;
            max-height: 50vh;
            border-radius: 8px;
            margin: 20px 0;
            box-shadow: 0 0 20px rgba(100, 150, 255, 0.3);
        }

        /* 翻页按钮 */
        .nav-btn {
            position: absolute;
            top: 50%;
            transform: translateY(-50%);
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.3);
            color: white;
            font-size: 2rem;
            padding: 15px 20px;
            cursor: pointer;
            border-radius: 50%;
            transition: all 0.3s ease;
            z-index: 10;
        }

        .nav-btn:hover {
            background: rgba(255, 255, 255, 0.2);
            box-shadow: 0 0 15px rgba(100, 150, 255, 0.5);
        }

        .prev-btn { left: -60px; }
        .next-btn { right: -60px; }

        /* 页码指示器 */
        .page-indicator {
            position: absolute;
            bottom: 20px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            gap: 10px;
        }

        .dot {
            width: 10px;
            height: 10px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.3);
            transition: all 0.3s ease;
        }

        .dot.active {
            background: white;
            box-shadow: 0 0 10px rgba(200, 220, 255, 0.8);
        }

        /* 响应式适配 */
        @media (max-width: 768px) {
            .book-container {
                width: 95vw;
                height: 70vh;
                margin: 15vh auto;
            }
            .page {
                padding: 20px;
            }
            .page h1 {
                font-size: 1.5rem;
            }
            .page p {
                font-size: 1rem;
            }
            .nav-btn {
                font-size: 1.5rem;
                padding: 10px 15px;
            }
            .prev-btn { left: -40px; }
            .next-btn { right: -40px; }
        }
    </style>
</head>
<body>
    <!-- 动态星星背景 -->
    <script>
        // 生成随机星星
        function createStars() {
            const count = 150; // 星星数量，可调整
            for (let i = 0; i < count; i++) {
                const star = document.createElement("div");
                star.className = "star";
                // 随机位置、大小、延迟
                const size = Math.random() * 3 + 1;
                star.style.width = size + "px";
                star.style.height = size + "px";
                star.style.left = Math.random() * 100 + "%";
                star.style.top = Math.random() * 100 + "%";
                star.style.animationDelay = Math.random() * 2 + "s";
                star.style.animationDuration = (Math.random() * 2 + 1) + "s";
                document.body.appendChild(star);
            }
        }
        createStars();
    </script>

    <!-- 翻书容器 -->
    <div class="book-container">
        <div class="book">
            <!-- 第1页：封面 -->
            <div class="page" style="transform: rotateY(0deg); z-index: 5;">
                <h1>✨ 给你的小礼物 ✨</h1>
                <p>这是一本只属于你的星空手账<br>每一页，都是我想对你说的话</p>
            </div>

            <!-- 第2页：文字页 -->
            <div class="page" style="transform: rotateY(-180deg); z-index: 4;">
                <h1>第一封信</h1>
                <p>谢谢你出现在我的生命里<br>像星星一样，照亮了很多平凡的夜晚<br>往后的日子，也请多多指教啦</p>
            </div>

            <!-- 第3页：视频页（替换为你的视频） -->
            <div class="page" style="transform: rotateY(-180deg); z-index: 3;">
                <h1>给你的一段小视频</h1>
                <video controls>
                    <!-- 把下面的 src 改成你上传到仓库里的视频文件名，比如 "video1.mp4" -->
                    <source src="your-video.mp4" type="video/mp4">
                    你的浏览器不支持视频播放
                </video>
                <p>这是我偷偷录下的小片段<br>希望你能感受到我的心意</p>
            </div>

            <!-- 第4页：结尾页 -->
            <div class="page" style="transform: rotateY(-180deg); z-index: 2;">
                <h1>最后一页</h1>
                <p>愿你永远像星星一样闪亮<br>愿所有温柔和美好，都奔向你<br>我会一直在，陪你看遍所有星空</p>
            </div>
        </div>

        <!-- 翻页按钮 -->
        <button class="nav-btn prev-btn" onclick="prevPage()">◀</button>
        <button class="nav-btn next-btn" onclick="nextPage()">▶</button>

        <!-- 页码指示器 -->
        <div class="page-indicator">
            <div class="dot active"></div>
            <div class="dot"></div>
            <div class="dot"></div>
            <div class="dot"></div>
        </div>
    </div>

    <script>
        let currentPage = 0;
        const pages = document.querySelectorAll(".page");
        const dots = document.querySelectorAll(".dot");
        const totalPages = pages.length;

        function updatePage() {
            pages.forEach((page, index) => {
                if (index <= currentPage) {
                    // 已翻过去的页，保持翻开状态
                    page.style.transform = `rotateY(${-index * 180}deg)`;
                    page.style.zIndex = totalPages - index;
                } else {
                    // 未翻到的页，保持关闭状态
                    page.style.transform = "rotateY(-180deg)";
                    page.style.zIndex = 1;
                }
            });

            // 更新指示器
            dots.forEach((dot, index) => {
                dot.classList.toggle("active", index === currentPage);
            });
        }

        function nextPage() {
            if (currentPage < totalPages - 1) {
                currentPage++;
                updatePage();
            }
        }

        function prevPage() {
            if (currentPage > 0) {
                currentPage--;
                updatePage();
            }
        }

        // 键盘翻页支持
        document.addEventListener("keydown", (e) => {
            if (e.key === "ArrowRight") nextPage();
            if (e.key === "ArrowLeft") prevPage();
        });

        // 触摸滑动支持（手机端）
        let touchStartX = 0;
        document.addEventListener("touchstart", (e) => {
            touchStartX = e.touches[0].clientX;
        });
        document.addEventListener("touchend", (e) => {
            const touchEndX = e.changedTouches[0].clientX;
            const diff = touchEndX - touchStartX;
            if (diff > 50) prevPage(); // 右滑上一页
            if (diff < -50) nextPage(); // 左滑下一页
        });
    </script>
</body>
</html>
