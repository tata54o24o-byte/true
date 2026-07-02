<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>True - هوش مصنوعی آفلاین</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        /* ===== تم پیش‌فرض (دارک) ===== */
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #121212;
            height: 100vh;
            display: flex;
            flex-direction: column;
            max-width: 500px;
            margin: 0 auto;
            position: relative;
            color: #e0e0e0;
            transition: background 0.3s, color 0.3s;
        }

        /* ===== تم روشن (Light Mode) ===== */
        body.light-mode {
            background: #f5f5f5;
            color: #222;
        }
        body.light-mode .header {
            background: #4CAF50;
            color: white;
            border-bottom: none;
        }
        body.light-mode .chat-container {
            background: #f5f5f5;
        }
        body.light-mode .input-area {
            background: #fff;
            border-top: 1px solid #ddd;
        }
        body.light-mode .input-area input {
            background: #f0f0f0;
            color: #222;
            border-color: #ccc;
        }
        body.light-mode .input-area input:focus {
            border-color: #4CAF50;
            background: #fff;
        }
        body.light-mode .message.user {
            background: #4CAF50;
        }
        body.light-mode .message.bot {
            background: #2196F3;
        }
        body.light-mode .welcome {
            color: #555;
        }
        body.light-mode .toast {
            background: #e0e0e0;
            color: #222;
            border-color: #aaa;
        }
        body.light-mode .settings-panel {
            background: #fff;
            border-left: 2px solid #4CAF50;
        }
        body.light-mode .settings-panel .close-btn {
            color: #333;
        }
        body.light-mode .settings-item {
            border-bottom: 1px solid #eee;
        }

        /* ===== هدر ===== */
        .header {
            background: #1e1e1e;
            color: #e0e0e0;
            padding: 15px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid #333;
            flex-shrink: 0;
            box-shadow: 0 2px 5px rgba(0,0,0,0.5);
            transition: background 0.3s;
        }
        .header-title {
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 20px;
            font-weight: bold;
        }
        .header-title span {
            font-size: 28px;
        }
        .header-actions {
            display: flex;
            gap: 12px;
            align-items: center;
        }
        .header-actions button {
            background: none;
            border: none;
            color: inherit;
            font-size: 24px;
            cursor: pointer;
            padding: 5px;
            border-radius: 50%;
            transition: 0.2s;
            line-height: 1;
        }
        .header-actions button:active {
            transform: scale(0.9);
            background: rgba(255,255,255,0.1);
        }
        .clear-btn {
            background: #c62828;
            color: white;
            border: none;
            border-radius: 25px;
            padding: 6px 15px;
            font-size: 12px;
            cursor: pointer;
            transition: 0.3s;
        }
        .clear-btn:active {
            transform: scale(0.95);
            background: #b71c1c;
        }

        /* ===== بخش چت ===== */
        .chat-container {
            flex: 1;
            overflow-y: auto;
            padding: 15px;
            display: flex;
            flex-direction: column;
            gap: 10px;
            background: #121212;
            transition: background 0.3s;
        }
        .message {
            max-width: 80%;
            padding: 12px 18px;
            border-radius: 18px;
            font-size: 16px;
            line-height: 1.5;
            word-wrap: break-word;
            animation: fadeIn 0.3s ease;
            position: relative;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .message.user {
            background: #2e7d32;
            color: #e8f5e9;
            align-self: flex-end;
            border-bottom-left-radius: 5px;
        }
        .message.bot {
            background: #0d47a1;
            color: #e3f2fd;
            align-self: flex-start;
            border-bottom-right-radius: 5px;
        }
        .message-actions {
            display: flex;
            gap: 8px;
            margin-top: 5px;
            justify-content: flex-end;
            opacity: 0.7;
        }
        .message-actions button {
            background: none;
            border: none;
            color: rgba(255,255,255,0.7);
            font-size: 12px;
            cursor: pointer;
            padding: 2px 8px;
            border-radius: 4px;
        }
        .message-actions button:active {
            background: rgba(255,255,255,0.15);
        }

        /* ===== ورودی ===== */
        .input-area {
            background: #1e1e1e;
            padding: 10px 15px;
            display: flex;
            gap: 10px;
            border-top: 1px solid #333;
            flex-shrink: 0;
            transition: background 0.3s;
        }
        .input-area input {
            flex: 1;
            padding: 12px 16px;
            border: 2px solid #333;
            border-radius: 25px;
            font-size: 16px;
            outline: none;
            transition: 0.3s;
            background: #2c2c2c;
            color: #e0e0e0;
        }
        .input-area input::placeholder {
            color: #888;
        }
        .input-area input:focus {
            border-color: #2e7d32;
            background: #333;
        }
        .input-area button {
            background: #2e7d32;
            color: white;
            border: none;
            border-radius: 25px;
            padding: 12px 24px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.3s;
            white-space: nowrap;
        }
        .input-area button:active {
            transform: scale(0.95);
            background: #1b5e20;
        }

        /* ===== اسکرول ===== */
        .chat-container::-webkit-scrollbar { width: 5px; }
        .chat-container::-webkit-scrollbar-thumb { background: #2e7d32; border-radius: 10px; }
        .chat-container::-webkit-scrollbar-track { background: #1a1a1a; }

        /* ===== خوش‌آمد ===== */
        .welcome {
            text-align: center;
            color: #aaa;
            padding: 20px;
            font-size: 14px;
        }
        .welcome strong { color: #4CAF50; }

        /* ===== توست ===== */
        .toast {
            position: fixed;
            bottom: 90px;
            left: 50%;
            transform: translateX(-50%);
            background: #333;
            color: #e0e0e0;
            padding: 10px 24px;
            border-radius: 25px;
            font-size: 14px;
            z-index: 9999;
            animation: fadeIn 0.3s ease;
            text-align: center;
            max-width: 90%;
            border: 1px solid #555;
            transition: 0.3s;
        }

        /* ===== پنل تنظیمات (مودال کشویی) ===== */
        .settings-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.6);
            z-index: 9998;
            display: none;
            justify-content: flex-end;
            animation: fadeInOverlay 0.2s;
        }
        .settings-overlay.active {
            display: flex;
        }
        @keyframes fadeInOverlay {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        .settings-panel {
            background: #1e1e1e;
            width: 85%;
            max-width: 350px;
            height: 100%;
            padding: 30px 20px;
            box-shadow: -5px 0 15px rgba(0,0,0,0.5);
            display: flex;
            flex-direction: column;
            gap: 20px;
            animation: slideIn 0.3s ease;
            overflow-y: auto;
            border-left: 2px solid #2e7d32;
            transition: background 0.3s;
        }
        @keyframes slideIn {
            from { transform: translateX(100%); }
            to { transform: translateX(0); }
        }
        .settings-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            border-bottom: 1px solid #333;
            padding-bottom: 15px;
        }
        .settings-header h2 {
            font-size: 22px;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        .settings-header .close-btn {
            font-size: 30px;
            background: none;
            border: none;
            color: #e0e0e0;
            cursor: pointer;
        }
        .settings-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px 0;
            border-bottom: 1px solid #2a2a2a;
        }
        .settings-item .label {
            font-size: 16px;
        }
        .settings-item .desc {
            font-size: 13px;
            color: #888;
        }
        /* دکمه سوئیچ */
        .switch {
            position: relative;
            width: 50px;
            height: 28px;
            background: #555;
            border-radius: 14px;
            cursor: pointer;
            transition: 0.3s;
            flex-shrink: 0;
        }
        .switch.active {
            background: #2e7d32;
        }
        .switch .ball {
            position: absolute;
            top: 3px;
            left: 3px;
            width: 22px;
            height: 22px;
            background: white;
            border-radius: 50%;
            transition: 0.3s;
        }
        .switch.active .ball {
            left: 25px;
        }
        .danger-btn {
            background: #c62828;
            color: white;
            border: none;
            padding: 8px 20px;
            border-radius: 25px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.2s;
        }
        .danger-btn:active {
            transform: scale(0.95);
        }
        .stat-number {
            font-size: 24px;
            font-weight: bold;
            color: #4CAF50;
        }
    </style>
</head>
<body>

    <!-- ===== هدر ===== -->
    <div class="header">
        <div class="header-title">
            <span>🧠</span> True
        </div>
        <div class="header-actions">
            <button onclick="toggleSettings()" title="تنظیمات">⚙️</button>
            <button class="clear-btn" onclick="clearAll()">🗑️ پاک کردن</button>
        </div>
    </div>

    <!-- ===== محفظه چت ===== -->
    <div class="chat-container" id="chatContainer">
        <div class="welcome">
            🤖 سلام! من <strong>True</strong> هستم.<br>
            هر کلمه یا جمله‌ای به من یاد بدی، تا ابد یادم می‌مونه!
        </div>
    </div>

    <!-- ===== بخش ورودی ===== -->
    <div class="input-area">
        <input type="text" id="messageInput" placeholder="یک کلمه یا جمله بنویس..." autofocus>
        <button id="sendBtn" onclick="sendMessage()">📤 ارسال</button>
    </div>

    <!-- ===== پنل تنظیمات (مودال) ===== -->
    <div class="settings-overlay" id="settingsOverlay" onclick="closeSettingsOutside(event)">
        <div class="settings-panel" id="settingsPanel">
            <div class="settings-header">
                <h2>⚙️ تنظیمات</h2>
                <button class="close-btn" onclick="toggleSettings()">✕</button>
            </div>

            <div class="settings-item">
                <div>
                    <div class="label">🌓 تم تاریک/روشن</div>
                    <div class="desc">تغییر ظاهر برنامه</div>
                </div>
                <div class="switch active" id="themeSwitch" onclick="toggleTheme()">
                    <div class="ball"></div>
                </div>
            </div>

            <div class="settings-item">
                <div>
                    <div class="label">📊 آمار</div>
                    <div class="desc">تعداد کلمات آموخته شده</div>
                </div>
                <div class="stat-number" id="statsCount">0</div>
            </div>

            <div class="settings-item">
                <div>
                    <div class="label" style="color:#ef5350;">🗑️ پاک کردن دیکشنری</div>
                    <div class="desc">همه پاسخ‌های ذخیره شده حذف می‌شوند</div>
                </div>
                <button class="danger-btn" onclick="clearDictionary()">پاک کن</button>
            </div>

            <div style="margin-top: auto; text-align: center; color: #666; font-size: 12px; padding-top: 20px;">
                True Bot v2.0 - آفلاین و امن
            </div>
        </div>
    </div>

    <script>
        // ============================================================
        // 1. داده‌ها و حافظه
        // ============================================================
        const STORAGE_KEY = 'true_bot_data';
        const MESSAGES_KEY = 'true_bot_messages';
        const THEME_KEY = 'true_bot_theme';

        let data = {};
        let messages = [];

        // ============================================================
        // 2. بارگذاری و ذخیره‌سازی
        // ============================================================
        function loadData() {
            const saved = localStorage.getItem(STORAGE_KEY);
            if (saved) {
                try { data = JSON.parse(saved); } catch (e) { data = {}; }
            }
        }
        function saveData() {
            localStorage.setItem(STORAGE_KEY, JSON.stringify(data));
            updateStats();
        }

        function loadMessages() {
            const saved = localStorage.getItem(MESSAGES_KEY);
            if (saved) {
                try { messages = JSON.parse(saved); } catch (e) { messages = []; }
            }
            const container = document.getElementById('chatContainer');
            if (messages.length > 0) {
                const welcome = container.querySelector('.welcome');
                if (welcome) welcome.remove();
            }
            messages.forEach(msg => {
                addMessageToUI(msg.text, msg.isUser, false);
            });
        }
        function saveMessages() {
            localStorage.setItem(MESSAGES_KEY, JSON.stringify(messages));
        }

        // ============================================================
        // 3. تم (دارک/روشن)
        // ============================================================
        function loadTheme() {
            const theme = localStorage.getItem(THEME_KEY);
            const isDark = theme !== 'light';
            const body = document.body;
            const switcher = document.getElementById('themeSwitch');
            if (isDark) {
                body.classList.remove('light-mode');
                switcher.classList.add('active');
            } else {
                body.classList.add('light-mode');
                switcher.classList.remove('active');
            }
        }

        function toggleTheme() {
            const body = document.body;
            const switcher = document.getElementById('themeSwitch');
            body.classList.toggle('light-mode');
            switcher.classList.toggle('active');
            const isLight = body.classList.contains('light-mode');
            localStorage.setItem(THEME_KEY, isLight ? 'light' : 'dark');
            showToast(isLight ? '🌞 تم روشن' : '🌙 تم تاریک');
        }

        // ============================================================
        // 4. آمار و تنظیمات
        // ============================================================
        function updateStats() {
            const count = Object.keys(data).length;
            document.getElementById('statsCount').textContent = count;
        }

        function toggleSettings() {
            const overlay = document.getElementById('settingsOverlay');
            overlay.classList.toggle('active');
            updateStats();
        }

        function closeSettingsOutside(e) {
            if (e.target === e.currentTarget) {
                toggleSettings();
            }
        }

        function clearDictionary() {
            if (confirm('⚠️ آیا از پاک کردن تمام پاسخ‌های ذخیره شده اطمینان دارید؟\nاین کار قابل بازگشت نیست!')) {
                data = {};
                saveData();
                updateStats();
                showToast('🗑️ همه پاسخ‌ها پاک شدند!');
                // ریفرش صفحه برای به‌روزرسانی لیست پیام‌ها (اختیاری)
                // برای راحتی کاربر، پیام‌های ربات قبلی رو پاک نمی‌کنیم ولی دیکشنری خالی میشه.
            }
        }

        // ============================================================
        // 5. مدیریت پیام‌ها در UI
        // ============================================================
        const container = document.getElementById('chatContainer');

        function addMessageToUI(text, isUser, save = true) {
            const welcome = container.querySelector('.welcome');
            if (welcome) welcome.remove();

            const div = document.createElement('div');
            div.className = `message ${isUser ? 'user' : 'bot'}`;

            const textSpan = document.createElement('span');
            textSpan.textContent = text;
            div.appendChild(textSpan);

            if (isUser) {
                const actions = document.createElement('div');
                actions.className = 'message-actions';
                const editBtn = document.createElement('button');
                editBtn.textContent = '✏️ ویرایش';
                editBtn.onclick = function(e) { e.stopPropagation(); editMessage(text, div); };
                const deleteBtn = document.createElement('button');
                deleteBtn.textContent = '🗑️ حذف';
                deleteBtn.onclick = function(e) { e.stopPropagation(); deleteMessage(text, div); };
                actions.appendChild(editBtn);
                actions.appendChild(deleteBtn);
                div.appendChild(actions);
            }

            container.appendChild(div);
            container.scrollTop = container.scrollHeight;

            if (save) {
                messages.push({ text, isUser });
                saveMessages();
            }
        }

        // ============================================================
        // 6. منطق اصلی ارسال و یادگیری
        // ============================================================
        function sendMessage() {
            const input = document.getElementById('messageInput');
            const text = input.value.trim();
            if (!text) { input.focus(); return; }
            input.value = '';
            input.focus();

            addMessageToUI(text, true);
            const answer = data[text];

            if (answer) {
                setTimeout(() => addMessageToUI(answer, false), 300);
            } else {
                setTimeout(() => showLearnDialog(text), 500);
            }
        }

        function showLearnDialog(keyword) {
            const answer = prompt(`🤖 من این جمله را بلد نیستم:\n"${keyword}"\n\nلطفاً پاسخی که باید بدهم را وارد کنید:`);
            if (answer !== null && answer.trim() !== '') {
                const trimmedAnswer = answer.trim();
                data[keyword] = trimmedAnswer;
                saveData();
                addMessageToUI(trimmedAnswer, false);
                showToast('✅ پاسخ ذخیره شد!');
            } else if (answer !== null) {
                showToast('❌ پاسخ خالی بود، ذخیره نشد.');
            }
        }

        // ============================================================
        // 7. ویرایش و حذف
        // ============================================================
        function editMessage(oldText, divElement) {
            const newText = prompt('✏️ متن جدید را وارد کنید:', oldText);
            if (newText !== null && newText.trim() !== '') {
                const trimmed = newText.trim();
                if (data[oldText] !== undefined) {
                    const answer = data[oldText];
                    delete data[oldText];
                    data[trimmed] = answer;
                    saveData();
                }
                const index = messages.findIndex(m => m.text === oldText && m.isUser === true);
                if (index !== -1) { messages[index].text = trimmed; saveMessages(); }
                const textSpan = divElement.querySelector('span');
                if (textSpan) textSpan.textContent = trimmed;
                showToast('✅ ویرایش شد!');
            }
        }

        function deleteMessage(text, divElement) {
            if (confirm(`آیا از حذف "${text}" اطمینان دارید؟`)) {
                if (data[text] !== undefined) { delete data[text]; saveData(); }
                const index = messages.findIndex(m => m.text === text && m.isUser === true);
                if (index !== -1) { messages.splice(index, 1); saveMessages(); }
                divElement.remove();
                showToast('🗑️ حذف شد!');
            }
        }

        function clearAll() {
            if (confirm('⚠️ آیا از پاک کردن تمام پیام‌ها اطمینان دارید؟\n(پاسخ‌های ذخیره شده حذف نمی‌شوند)')) {
                container.innerHTML = '';
                messages = [];
                saveMessages();
                const welcome = document.createElement('div');
                welcome.className = 'welcome';
                welcome.innerHTML = '🤖 سلام! من <strong>True</strong> هستم.<br>هر کلمه یا جمله‌ای به من یاد بدی، تا ابد یادم می‌مونه!';
                container.appendChild(welcome);
                showToast('🧹 همه پیام‌ها پاک شدند!');
            }
        }

        // ============================================================
        // 8. توست و ابزار
        // ============================================================
        function showToast(msg) {
            const toast = document.createElement('div');
            toast.className = 'toast';
            toast.textContent = msg;
            document.body.appendChild(toast);
            setTimeout(() => {
                toast.style.opacity = '0';
                toast.style.transition = 'opacity 0.5s';
                setTimeout(() => toast.remove(), 500);
            }, 2500);
        }

        // ============================================================
        // 9. رویدادهای کلید Enter
        // ============================================================
        document.getElementById('messageInput').addEventListener('keydown', function(e) {
            if (e.key === 'Enter') { e.preventDefault(); sendMessage(); }
        });

        // ============================================================
        // 10. راه‌اندازی نهایی
        // ============================================================
        loadData();
        loadMessages();
        loadTheme();
        updateStats();

        if (messages.length === 0) { /* پیام خوش‌آمد موجود است */ }

        console.log('🧠 True - هوش مصنوعی آفلاین (نسخه تنظیمات)');
        console.log('📚 تعداد پاسخ‌های ذخیره شده:', Object.keys(data).length);
    </script>
</body>
</html>
