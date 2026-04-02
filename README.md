# eslingercoleen614-alt.github.io
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>趣味测试</title>
    <!-- 引入 Tailwind CSS 进行快速样式开发 -->
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* 添加一些简单的过渡动画 */
        .fade-in {
            animation: fadeIn 0.5s ease-in-out forwards;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body class="bg-gradient-to-br from-indigo-100 via-purple-100 to-pink-100 min-h-screen flex items-center justify-center p-4 font-sans text-gray-800">

    <!-- 主容器 -->
    <div id="app-container" class="bg-white rounded-2xl shadow-xl w-full max-w-md overflow-hidden transition-all duration-300">
        
        <!-- 第一个页面：猴子与输入框 -->
        <div id="page1" class="p-6 sm:p-8 fade-in flex flex-col items-center">
            <h1 class="text-2xl sm:text-3xl font-bold mb-6 text-center text-indigo-600">灵长类动物鉴定器</h1>
            
            <!-- 猴子照片 (带有加载失败的备用显示) -->
            <div class="w-full aspect-square sm:aspect-[4/3] rounded-xl overflow-hidden mb-6 bg-gray-200 flex items-center justify-center relative shadow-inner">
                <img 
                    src="https://images.unsplash.com/photo-1540573133985-87b6da6d54a9?auto=format&fit=crop&w=800&q=80" 
                    alt="猴子" 
                    class="w-full h-full object-cover"
                    onerror="this.style.display='none'; this.nextElementSibling.style.display='flex';"
                >
                <div class="hidden absolute inset-0 flex items-center justify-center text-6xl">
                    🐒
                </div>
            </div>

            <p class="text-gray-600 mb-4 text-center">系统检测到你身上散发着独特的自然气息。请输入你的名字以查看你的真实形态：</p>
            
            <!-- 输入框 -->
            <input 
                type="text" 
                id="userName" 
                placeholder="请输入你的尊姓大名..." 
                class="w-full px-4 py-3 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-transparent transition-all mb-4"
                onkeypress="handleKeyPress(event)"
            >
            
            <!-- 提交按钮 -->
            <button 
                onclick="goToPage2()" 
                class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-3 px-4 rounded-lg transition-colors duration-200 transform hover:scale-[1.02] active:scale-95 shadow-md"
            >
                开始鉴定
            </button>
            
            <!-- 错误提示信息 -->
            <p id="error-msg" class="text-red-500 text-sm mt-2 hidden">随便输入点什么名字都可以哦！</p>
        </div>

        <!-- 第二个页面：母猪照片 (初始隐藏) -->
        <div id="page2" class="p-6 sm:p-8 hidden flex flex-col items-center relative">
            
            <!-- 越哥的专属水印 -->
            <div class="absolute top-4 right-4 text-xs sm:text-sm text-gray-400 font-bold opacity-70 select-none tracking-widest">
                不要感谢你越哥
            </div>

            <h1 class="text-2xl sm:text-3xl font-bold mb-2 text-center text-pink-600">鉴定结果</h1>
            <p id="greeting" class="text-lg text-gray-700 mb-6 text-center font-medium"></p>
            
            <!-- 母猪照片 (带有加载失败的备用显示) -->
            <div class="w-full aspect-square sm:aspect-[4/3] rounded-xl overflow-hidden mb-6 bg-pink-50 flex items-center justify-center relative shadow-inner border-4 border-pink-200">
                <img 
                    src="https://images.unsplash.com/photo-1603525547463-53531db78601?auto=format&fit=crop&w=800&q=80" 
                    alt="母猪" 
                    class="w-full h-full object-cover"
                    onerror="this.style.display='none'; this.nextElementSibling.style.display='flex';"
                >
                <div class="hidden absolute inset-0 flex items-center justify-center text-6xl">
                    🐖
                </div>
            </div>

            <p class="text-gray-600 mb-6 text-center italic">"哼哼，看起来今天胃口不错！"</p>
            
            <!-- 返回按钮 -->
            <button 
                onclick="goToPage1()" 
                class="w-full bg-gray-200 hover:bg-gray-300 text-gray-800 font-bold py-3 px-4 rounded-lg transition-colors duration-200 transform hover:scale-[1.02] active:scale-95"
            >
                重新测试
            </button>
        </div>

    </div>

    <script>
        // 获取页面元素
        const page1 = document.getElementById('page1');
        const page2 = document.getElementById('page2');
        const nameInput = document.getElementById('userName');
        const greeting = document.getElementById('greeting');
        const errorMsg = document.getElementById('error-msg');

        // 处理回车键直接提交
        function handleKeyPress(event) {
            if (event.key === 'Enter') {
                goToPage2();
            }
        }

        // 跳转到第二个页面的逻辑
        function goToPage2() {
            const name = nameInput.value.trim();
            
            // 简单的防空处理（也可以根据你的要求完全不限制，这里稍微引导一下用户输入）
            if (name === '') {
                errorMsg.classList.remove('hidden');
                nameInput.focus();
                return;
            }
            
            errorMsg.classList.add('hidden');

            // 设置第二页的问候语
            greeting.textContent = `尊敬的 ${name}，这就是你最本质的形态：`;

            // 切换页面显示
            page1.classList.add('hidden');
            page1.classList.remove('fade-in'); // 移除动画类以便下次可以重新触发
            
            page2.classList.remove('hidden');
            // 强制重绘以触发动画
            void page2.offsetWidth; 
            page2.classList.add('fade-in');
        }

        // 返回第一个页面的逻辑（方便反复测试）
        function goToPage1() {
            nameInput.value = ''; // 清空输入框
            
            page2.classList.add('hidden');
            page2.classList.remove('fade-in');
            
            page1.classList.remove('hidden');
            void page1.offsetWidth;
            page1.classList.add('fade-in');
            
            nameInput.focus();
        }
    </script>
</body>
</html>
