# Wwj.github.io
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>简洁网址导航</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        body {
            background-color: #f5f7fa;
            padding: 20px;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
        }
        header {
            text-align: center;
            margin-bottom: 30px;
        }
        h1 {
            color: #333;
            margin-bottom: 15px;
        }
        .search-box {
            display: flex;
            max-width: 600px;
            margin: 0 auto;
        }
        #search-input {
            flex: 1;
            padding: 12px 15px;
            font-size: 16px;
            border: 2px solid #ddd;
            border-radius: 8px 0 0 8px;
            outline: none;
            transition: border 0.3s;
        }
        #search-input:focus {
            border-color: #4285f4;
        }
        #search-btn {
            padding: 0 20px;
            background-color: #4285f4;
            color: white;
            border: none;
            border-radius: 0 8px 8px 0;
            cursor: pointer;
            transition: background 0.3s;
        }
        #search-btn:hover {
            background-color: #3367d6;
        }
        .category {
            margin-bottom: 30px;
        }
        .category h2 {
            color: #555;
            margin-bottom: 15px;
            padding-bottom: 8px;
            border-bottom: 2px solid #eee;
        }
        .sites {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
        }
        .site-card {
            background: white;
            border-radius: 8px;
            padding: 15px;
            width: calc(20% - 12px);
            min-width: 150px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            transition: transform 0.2s, box-shadow 0.2s;
            cursor: pointer;
        }
        .site-card:hover {
            transform: translateY(-3px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        .site-name {
            font-weight: 600;
            color: #333;
            margin-bottom: 5px;
        }
        .site-url {
            font-size: 14px;
            color: #666;
            overflow: hidden;
            text-overflow: ellipsis;
            white-space: nowrap;
        }
        @media (max-width: 768px) {
            .site-card {
                width: calc(33.333% - 10px);
            }
        }
        @media (max-width: 480px) {
            .site-card {
                width: calc(50% - 7.5px);
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>常用网址导航</h1>
            <div class="search-box">
                <input type="text" id="search-input" placeholder="搜索网站...">
                <button id="search-btn">搜索</button>
            </div>
        </header>

        <div class="category">
            <h2>搜索引擎</h2>
            <div class="sites">
                <div class="site-card" data-url="https://www.baidu.com">
                    <div class="site-name">百度</div>
                    <div class="site-url">www.baidu.com</div>
                </div>
                <div class="site-card" data-url="https://www.google.com">
                    <div class="site-name">谷歌</div>
                    <div class="site-url">www.google.com</div>
                </div>
                <div class="site-card" data-url="https://cn.bing.com">
                    <div class="site-name">必应</div>
                    <div class="site-url">cn.bing.com</div>
                </div>
            </div>
        </div>

        <div class="category">
            <h2>社交平台</h2>
            <div class="sites">
                <div class="site-card" data-url="https://weixin.qq.com">
                    <div class="site-name">微信</div>
                    <div class="site-url">weixin.qq.com</div>
                </div>
                <div class="site-card" data-url="https://weibo.com">
                    <div class="site-name">微博</div>
                    <div class="site-url">weibo.com</div>
                </div>
                <div class="site-card" data-url="https://www.douban.com">
                    <div class="site-name">豆瓣</div>
                    <div class="site-url">www.douban.com</div>
                </div>
            </div>
        </div>

        <div class="category">
            <h2>视频平台</h2>
            <div class="sites">
                <div class="site-card" data-url="https://www.bilibili.com">
                    <div class="site-name">哔哩哔哩</div>
                    <div class="site-url">www.bilibili.com</div>
                </div>
                <div class="site-card" data-url="https://v.qq.com">
                    <div class="site-name">腾讯视频</div>
                    <div class="site-url">v.qq.com</div>
                </div>
                <div class="site-card" data-url="https://www.iqiyi.com">
                    <div class="site-name">爱奇艺</div>
                    <div class="site-url">www.iqiyi.com</div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // 点击网站卡片跳转
        document.querySelectorAll('.site-card').forEach(card => {
            card.addEventListener('click', () => {
                const url = card.getAttribute('data-url');
                window.open(url, '_blank');
            });
        });

        // 搜索功能
        document.getElementById('search-btn').addEventListener('click', performSearch);
        document.getElementById('search-input').addEventListener('keypress', (e) => {
            if (e.key === 'Enter') performSearch();
        });

        function performSearch() {
            const keyword = document.getElementById('search-input').value.trim().toLowerCase();
            if (!keyword) return;
            
            // 优先在导航中查找匹配网站
            const matched = Array.from(document.querySelectorAll('.site-card')).find(card => 
                card.querySelector('.site-name').textContent.toLowerCase().includes(keyword) ||
                card.querySelector('.site-url').textContent.toLowerCase().includes(keyword)
            );
            
            if (matched) {
                window.open(matched.getAttribute('data-url'), '_blank');
            } else {
                // 未找到则使用百度搜索
                window.open(`https://www.baidu.com/s?wd=${encodeURIComponent(keyword)}`, '_blank');
            }
        }
    </script>
</body>
</html>
