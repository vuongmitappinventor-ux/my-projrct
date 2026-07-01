<!DOCTYPE html>
<html lang="vi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Khu Vườn Thiện Nguyện May Mắn</title>
    <style>
        /* --- ĐỊNH DẠNG CƠ BẢN & CHUỘT TÙY CHỈNH --- */
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Arial, sans-serif;
            cursor: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='24' height='24' viewBox='0 0 24 24'%3E%3Ctext y='18' font-size='18'%3E🌱%3C/text%3E%3C/svg%3E"), auto;
        }

        body {
            background: linear-gradient(135deg, #e8f5e9 0%, #c8e6c9 100%);
            color: #2e7d32;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            position: relative;
            overflow-x: hidden;
        }

        /* --- HIỆU ỨNG CHUỘT CLICK BÙNG NỔ (RIPPLE) --- */
        .click-effect {
            position: absolute;
            border: 3px solid #4caf50;
            border-radius: 50%;
            width: 10px;
            height: 10px;
            transform: translate(-50%, -50%);
            animation: ripple-out 0.6s ease-out forwards;
            pointer-events: none;
            z-index: 9999;
        }
        @keyframes ripple-out {
            from { width: 0; height: 0; opacity: 1; }
            to { width: 60px; height: 60px; opacity: 0; border-color: #81c784; }
        }

        /* --- PHÔNG NỀN CÂY CỐI ĐUNG ĐƯA TỰ NHIÊN --- */
        .background-leaves {
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0; left: 0;
            pointer-events: none;
            z-index: 1;
            overflow: hidden;
        }
        .leaf-nature {
            position: absolute;
            font-size: 50px;
            opacity: 0.15;
            animation: sway 4s ease-in-out infinite alternate;
        }
        .ln1 { top: 15%; left: 8%; animation-delay: 0s; }
        .ln2 { bottom: 20%; right: 8%; animation-delay: 1s; transform: rotate(45deg); }
        .ln3 { top: 70%; left: 12%; animation-delay: 0.5s; }
        .ln4 { top: 10%; right: 15%; animation-delay: 1.5s; }

        @keyframes sway {
            0% { transform: rotate(-10deg) translateY(0); }
            100% { transform: rotate(15deg) translateY(-15px); }
        }

        /* --- KHUNG THẺ CHUNG --- */
        .nature-card {
            background: rgba(255, 255, 255, 0.95);
            border: 1px solid rgba(200, 230, 201, 0.5);
            padding: 30px;
            border-radius: 30px;
            width: 100%;
            max-width: 420px;
            box-shadow: 0 15px 35px rgba(46, 125, 50, 0.1);
            position: relative;
            z-index: 10;
        }

        .icon-header { text-align: center; font-size: 35px; margin-bottom: 10px; }
        h2 { text-align: center; font-size: 22px; margin-bottom: 25px; color: #1b5e20; }
        .form-group { margin-bottom: 18px; }
        label { display: block; font-size: 13px; font-weight: 500; margin-bottom: 6px; color: #4e342e; }
        
        input {
            width: 100%; padding: 12px 16px; background: #f1f8e9;
            border: 1.5px solid #dcedc8; border-radius: 16px; color: #2e7d32; font-size: 15px; outline: none;
        }
        input:focus { border-color: #81c784; background: #ffffff; box-shadow: 0 0 0 4px rgba(129, 199, 132, 0.2); }

        button {
            width: 100%; padding: 14px; background: #4caf50; border: none; border-radius: 16px;
            color: white; font-size: 15px; font-weight: 600; cursor: pointer; transition: all 0.2s; margin-top: 5px;
        }
        button:hover { background: #388e3c; }

        .links-container { display: flex; justify-content: space-between; margin-top: 20px; font-size: 13px; }
        .switch-link { color: #388e3c; cursor: pointer; text-decoration: none; font-weight: 500; }
        .hidden { display: none !important; }

        .captcha-area { display: flex; align-items: center; gap: 12px; margin-bottom: 12px; }
        #captchaCanvas { background: #f1f8e9; border-radius: 12px; border: 1.5px solid #dcedc8; }
        .status-msg { text-align: center; margin-top: 15px; font-size: 13px; min-height: 20px; }
        .text-success { color: #2e7d32; font-weight: bold; }
        .text-error { color: #d32f2f; }

        /* --- WEBSITE CHÍNH --- */
        .dashboard {
            width: 100%;
            max-width: 600px;
            background: rgba(255, 255, 255, 0.95);
            padding: 30px;
            border-radius: 30px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.05);
            z-index: 10;
            max-height: 85vh;
            overflow-y: auto;
            scroll-behavior: smooth;
        }

        .dashboard::-webkit-scrollbar { width: 6px; }
        .dashboard::-webkit-scrollbar-thumb { background-color: #a5d6a7; border-radius: 10px; }

        .user-bar { 
            position: sticky; top: 0; background: white; z-index: 20;
            display: flex; justify-content: space-between; align-items: center; 
            padding-bottom: 15px; border-bottom: 1px dashed #c8e6c9; margin-bottom: 20px;
        }
        .coin-count { background: #fff9c4; padding: 6px 14px; border-radius: 20px; font-weight: bold; color: #f57f17; border: 1px solid #fff59d; }

        /* Bảng điểm danh */
        .grid-days { display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px; margin-bottom: 30px; }
        .day-box { background: #f1f8e9; border: 2px solid #e8f5e9; border-radius: 16px; padding: 12px 5px; text-align: center; position: relative; transition: all 0.3s; }
        .day-box.day-7 { grid-column: span 2; background: #e8f5e9; }
        .day-title { font-size: 11px; font-weight: bold; color: #558b2f; }
        .day-gift { font-size: 18px; margin: 3px 0; }
        .day-reward { font-size: 11px; color: #2e7d32; font-weight: bold; }
        .day-box.claimed { background: #c8e6c9; border-color: #81c784; opacity: 0.7; }
        .day-box.claimed::after { content: '✓'; position: absolute; top: 3px; right: 6px; font-weight: bold; color: #1b5e20; }
        .day-box.active-claim { border-color: #4caf50; background: #e8f5e9; cursor: pointer; animation: pulse 1.5s infinite; }
        @keyframes pulse { 0% { box-shadow: 0 0 0 0 rgba(76, 175, 80, 0.4); } 100% { box-shadow: 0 0 0 8px rgba(76, 175, 80, 0); } }

        /* --- CHARITY QUYÊN GÓP (SCROLL FADE) --- */
        .charity-section-title { margin-top: 20px; margin-bottom: 15px; font-size: 18px; border-left: 4px solid #4caf50; padding-left: 10px; }
        
        .charity-card {
            background: #fafafa; border: 1px solid #e0e0e0; border-radius: 20px;
            padding: 20px; margin-bottom: 20px; display: flex; align-items: center; gap: 15px;
            opacity: 0.3; transform: scale(0.95); transition: opacity 0.5s ease, transform 0.5s ease;
        }
        .charity-card.visible-active {
            opacity: 1 !important; transform: scale(1);
            border-color: #a5d6a7; background: #f9fbf9; box-shadow: 0 5px 15px rgba(46, 125, 50, 0.05);
        }

        .charity-icon { font-size: 35px; }
        .charity-info { flex: 1; }
        .charity-info h4 { color: #1b5e20; margin-bottom: 4px; }
        .charity-info p { font-size: 13px; color: #616161; margin-bottom: 8px; }
        .donate-btn { padding: 8px 15px; font-size: 13px; border-radius: 10px; width: auto; display: inline-block; margin: 0; }

        /* --- POPUP UNLOCK 7 NGÀY --- */
        .popup-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0,0,0,0.4); display: flex; justify-content: center; align-items: center; z-index: 100; backdrop-filter: blur(4px); }
        .popup-box { background: white; padding: 30px; border-radius: 24px; text-align: center; max-width: 360px; width: 90%; box-shadow: 0 10px 25px rgba(0,0,0,0.15); }
        .popup-btns { display: flex; gap: 10px; margin-top: 15px; }
        .btn-yes { background: #4caf50; } .btn-no { background: #9e9e9e; }

        /* --- HIỆU ỨNG PHÁO HOA --- */
        .particle { position: absolute; pointer-events: none; border-radius: 50%; z-index: 999; animation: explode 0.8s ease-out forwards; }
        @keyframes explode {
            0% { transform: translate(0, 0) scale(1); opacity: 1; }
            100% { transform: translate(var(--mx), var(--my)) scale(0.2); opacity: 0; }
        }

        /* --- KHUNG DANH HIỆU LẤP LÁNH --- */
        .badge-banner {
            background: linear-gradient(45deg, #ffd700, #ffaa00, #fff7c2); color: #5d4037;
            padding: 15px; border-radius: 20px; text-align: center; font-weight: bold;
            border: 3px solid #ffb300; box-shadow: 0 0 20px rgba(255, 215, 0, 0.6);
            margin-top: 15px; animation: golden-glow 2s infinite alternate;
        }
        @keyframes golden-glow {
            0% { box-shadow: 0 0 10px rgba(255, 215, 0, 0.5); transform: scale(1); }
            100% { box-shadow: 0 0 25px rgba(255, 215, 0, 0.9); transform: scale(1.02); }
        }

        /* --- STYLE TRỨNG PHỤC SINH TRÒ ĐÙA (FOOTER CRREDIT) --- */
        .monkey-credit {
            text-align: center;
            font-size: 11px;
            color: #9e9e9e;
            margin-top: 30px;
            padding-top: 10px;
            border-top: 1px dashed #eee;
            cursor: pointer;
            transition: color 0.2s;
        }
        .monkey-credit:hover {
            color: #e91e63;
            text-decoration: underline;
        }
    </style>
</head>
<body>

    <div class="background-leaves">
        <div class="leaf-nature ln1">🌱</div>
        <div class="leaf-nature ln2">🍃</div>
        <div class="leaf-nature ln3">🌿</div>
        <div class="leaf-nature ln4">🌳</div>
    </div>

    <!-- KHU VỰC ĐĂNG NHẬP -->
    <div id="authSection" class="nature-card">
        <div id="welcomeStep">
            <div class="icon-header">🌱</div>
            <h2>Xin chào bạn!</h2>
            <div class="form-group"><label>Cho mình hỏi tên bạn là gì thế nhỉ?</label><input type="text" id="visitorName" placeholder="Nhập tên của bạn..."></div>
            <button onclick="submitName()">Tiếp tục thôi</button>
        </div>

        <div id="loginStep" class="hidden">
            <div class="icon-header">🏡</div><h2 id="loginTitle">Đăng Nhập</h2>
            <div class="form-group"><label>Tên tài khoản</label><input type="text" id="loginUser" placeholder="Tên đăng nhập"></div>
            <div class="form-group"><label>Địa chỉ Gmail</label><input type="email" id="loginEmail" placeholder="example@gmail.com"></div>
            <div class="form-group"><label>Mật khẩu</label><input type="password" id="loginPass" placeholder="••••••••"></div>
            <button onclick="handleLogin()">Đăng nhập</button>
            <div class="links-container">
                <span class="switch-link" onclick="routeTo('register')">Tạo tài khoản mới</span>
                <span class="switch-link" onclick="routeTo('forgot')">Quên mật khẩu?</span>
            </div>
        </div>

        <div id="registerStep" class="hidden">
            <div class="icon-header">🌿</div><h2>Đăng Ký Tài Khoản</h2>
            <div class="form-group"><label>Tên tài khoản mới</label><input type="text" id="regUser" placeholder="Tên đăng nhập"></div>
            <div class="form-group"><label>Địa chỉ Gmail</label><input type="email" id="regEmail" placeholder="Nhập Gmail"></div>
            <div class="form-group"><label>Mật khẩu</label><input type="password" id="regPass" placeholder="Tạo mật khẩu"></div>
            <div class="form-group"><label>Xác nhận mật khẩu</label><input type="password" id="regConfirmPass" placeholder="Nhập lại mật khẩu"></div>
            <label>Mã xác minh chống Robot</label>
            <div class="captcha-area"><canvas id="captchaCanvas" width="130" height="42"></canvas><span class="reload-captcha" onclick="generateCaptcha()">🔄</span></div>
            <div class="form-group"><input type="text" id="captchaInput" placeholder="Nhập chữ méo mó"></div>
            <button onclick="handleRegister()">Hoàn tất đăng ký</button>
            <div class="links-container" style="justify-content: center;"><span class="switch-link" onclick="routeTo('login')">Quay lại đăng nhập</span></div>
        </div>

        <div id="forgotStep" class="hidden">
            <div class="icon-header">🍂</div><h2>Quên Mật Khẩu</h2>
            <div class="form-group"><label>Tên tài khoản</label><input type="text" id="forgotUser" placeholder="Nhập tên tài khoản"></div>
            <div class="form-group"><label>Gmail đã đăng ký</label><input type="email" id="forgotEmail" placeholder="Nhập Gmail"></div>
            <button onclick="handleForgot()">Gửi mã xác minh</button>
            <div class="links-container" style="justify-content: center;"><span class="switch-link" onclick="routeTo('login')">Quay lại đăng nhập</span></div>
        </div>
        <div id="statusMsg" class="status-msg"></div>
    </div>

    <!-- KHU VỰC TRANG WEB CHÍNH -->
    <div id="mainWebsite" class="dashboard hidden" onscroll="handleScrollFade()">
        <div class="user-bar">
            <div>Chào, <strong id="txtUser">Bạn</strong>! 🌱</div>
            <div class="coin-count">💰 <span id="userCoins">0</span> Xu</div>
        </div>

        <h2>📅 Quà Điểm Danh</h2>
        <div class="grid-days">
            <div class="day-box active-claim" id="day1" onclick="claimDay1()"><div class="day-title">Ngày 1</div><div class="day-gift">💰</div><div class="day-reward">1.000</div></div>
            <div class="day-box" id="day2"><div class="day-title">Ngày 2</div><div class="day-gift">💰</div><div class="day-reward">3.000</div></div>
            <div class="day-box" id="day3"><div class="day-title">Ngày 3</div><div class="day-gift">💰</div><div class="day-reward">4.000</div></div>
            <div class="day-box" id="day4"><div class="day-title">Ngày 4</div><div class="day-gift">💰</div><div class="day-reward">5.000</div></div>
            <div class="day-box" id="day5"><div class="day-title">Ngày 5</div><div class="day-gift">💰</div><div class="day-reward">6.000</div></div>
            <div class="day-box" id="day6"><div class="day-title">Ngày 6</div><div class="day-gift">💰</div><div class="day-reward">6.000</div></div>
            <div class="day-box day-7" id="day7"><div class="day-title">Ngày 7</div><div class="day-gift">🚀</div><div class="day-reward">Tên Lửa</div></div>
        </div>

        <div id="richBadge" class="badge-banner hidden">
            🏆 DANH HIỆU HUYỀN THOẠI 🏆 <br>
            ✨ "The Richest in the World" ✨
        </div>

        <h3 class="charity-section-title">🌻 Quỹ Từ Thiện Xanh</h3>
        
        <div class="charity-card" id="charity1">
            <div class="charity-icon">🌳</div>
            <div class="charity-info">
                <h4>Trồng Rừng Phủ Xanh</h4>
                <p>Quyên góp xu để mua thêm cây non phủ xanh đồi trọc khắp hành tinh.</p>
                <button class="donate-btn" onclick="donateToCharity(this, 2000)">Donate 2.000 Xu</button>
            </div>
        </div>

        <div class="charity-card" id="charity2">
            <div class="charity-icon">🌊</div>
            <div class="charity-info">
                <h4>Làm Sạch Đại Dương</h4>
                <p>Chung tay loại bỏ rác thải nhựa, bảo vệ các sinh vật biển xanh khơi.</p>
                <button class="donate-btn" onclick="donateToCharity(this, 5000)">Donate 5.000 Xu</button>
            </div>
        </div>

        <div class="charity-card" id="charity3">
            <div class="charity-icon">🐱</div>
            <div class="charity-info">
                <h4>Trạm Cứu Hộ Thú Cưng</h4>
                <p>Cung cấp thức ăn, y tế và mái ấm tình thương cho động vật cơ nhỡ.</p>
                <button class="donate-btn" onclick="donateToCharity(this, 3000)">Donate 3.000 Xu</button>
            </div>
        </div>

        <div class="charity-card" id="charity4">
            <div class="charity-icon">☀️</div>
            <div class="charity-info">
                <h4>Năng Lượng Mặt Trời Trẻ Em</h4>
                <p>Lắp đặt hệ thống pin mặt trời cho các lớp học vùng sâu vùng xa.</p>
                <button class="donate-btn" onclick="donateToCharity(this, 4000)">Donate 4.000 Xu</button>
            </div>
        </div>

        <button onclick="location.reload()" style="background:#78909c; font-size:13px; padding:8px; margin-top:20px;">Đăng xuất</button>

        <!-- --- ĐÂY LÀ ĐOẠN TRỨNG PHỤC SINH LUỒNG CHẠY MỚI NÈ --- -->
        <div class="monkey-credit" onclick="triggerMonkeyJoke()">
            Created by a monkey from 7a9
        </div>
    </div>

    <!-- POPUP HOI UNLOCK -->
    <div id="unlockPopup" class="popup-overlay hidden">
        <div class="popup-box">
            <div style="font-size: 40px; margin-bottom: 10px;">✨🔮✨</div>
            <h3>Cơ Hỏi Kích Hoạt!</h3>
            <p>Dùng <strong>1.000 xu vừa nhận</strong> để UNLOCK FULL quà tặng của tất cả 7 ngày ngay lập tức?</p>
            <div class="popup-btns">
                <button class="btn-yes" onclick="confirmUnlock(true)">Đồng ý mở khóa</button>
                <button class="btn-no" onclick="confirmUnlock(false)">Tắt đi</button>
            </div>
        </div>
    </div>

<script>
    // --- HIỆU ỨNG CLICK CHUỘT ---
    document.addEventListener('click', function(e) {
        let ripple = document.createElement('div');
        ripple.classList.add('click-effect');
        ripple.style.left = e.pageX + 'px';
        ripple.style.top = e.pageY + 'px';
        document.body.appendChild(ripple);
        setTimeout(() => { ripple.remove(); }, 600);
    });

    // --- QUẢN LÝ ---
    const authSection = document.getElementById('authSection');
    const mainWebsite = document.getElementById('mainWebsite');
    const unlockPopup = document.getElementById('unlockPopup');
    const userCoinsTxt = document.getElementById('userCoins');
    const richBadge = document.getElementById('richBadge');
    
    let totalCoins = 0;
    let donatedCoins = 0;
    let currentCaptchaText = "";

    const views = {
        welcome: document.getElementById('welcomeStep'),
        login: document.getElementById('loginStep'),
        register: document.getElementById('registerStep'),
        forgot: document.getElementById('forgotStep')
    };
    const statusMsg = document.getElementById('statusMsg');

    function submitName() {
        const name = document.getElementById('visitorName').value.trim();
        if (!name) { showStatus('Bạn chưa nhập tên kìa! 😊🌿', 'error'); return; }
        document.getElementById('loginTitle').innerText = `Chào mừng ${name} quay lại nhé!`;
        routeTo('login');
    }

    function routeTo(targetView) {
        clearStatus();
        Object.keys(views).forEach(key => views[key].classList.add('hidden'));
        views[targetView].classList.remove('hidden');
        if (targetView === 'register') generateCaptcha();
    }

    function generateCaptcha() {
        const canvas = document.getElementById('captchaCanvas'); const ctx = canvas.getContext('2d');
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        const chars = "ABCDEFGHJKLMNPQRSTUVWXYZabcdefghijkmnpqrstuvwxyz23456789";
        currentCaptchaText = "";
        for (let i = 0; i < 5; i++) currentCaptchaText += chars.charAt(Math.floor(Math.random() * chars.length));
        ctx.font = "italic bold 21px Arial";
        for (let i = 0; i < currentCaptchaText.length; i++) {
            ctx.fillStyle = i % 2 === 0 ? "#2e7d32" : "#388e3c";
            ctx.save(); ctx.translate(16 + i * 22, 26 + Math.random() * 6 - 3);
            ctx.rotate((Math.random() * 24 - 12) * Math.PI / 180);
            ctx.fillText(currentCaptchaText[i], 0, 0); ctx.restore();
        }
    }

    function handleRegister() {
        const user = document.getElementById('regUser').value.trim();
        const email = document.getElementById('regEmail').value.trim();
        const pass = document.getElementById('regPass').value;
        const confirmPass = document.getElementById('regConfirmPass').value;
        const captchaInput = document.getElementById('captchaInput').value.trim();

        if (!user || !email || !pass || !confirmPass) { showStatus('Vui lòng điền đủ thông tin!', 'error'); return; }
        if (pass !== confirmPass) { showStatus('Mật khẩu nhập lại chưa khớp!', 'error'); return; }
        if (captchaInput.toLowerCase() !== currentCaptchaText.toLowerCase()) { showStatus('Mã xác minh sai!', 'error'); generateCaptcha(); return; }

        localStorage.setItem(user, JSON.stringify({ password: pass, email: email }));
        showStatus('🍀 Đăng ký thành công!', 'success');
        setTimeout(() => { routeTo('login'); document.getElementById('loginUser').value = user; document.getElementById('loginEmail').value = email; }, 1200);
    }

    function handleLogin() {
        const user = document.getElementById('loginUser').value.trim();
        const email = document.getElementById('loginEmail').value.trim();
        const pass = document.getElementById('loginPass').value;

        if (!user || !email || !pass) { showStatus('Vui lòng điền đủ thông tin!', 'error'); return; }
        const savedData = localStorage.getItem(user);
        if (savedData) {
            const parsedData = JSON.parse(savedData);
            if (parsedData.email === email && parsedData.password === pass) {
                document.getElementById('txtUser').innerText = user;
                authSection.classList.add('hidden');
                mainWebsite.classList.remove('hidden');
                setTimeout(handleScrollFade, 200);
            } else { showStatus('Thông tin tài khoản chưa đúng rồi!', 'error'); }
        } else { showStatus('Tài khoản chưa tồn tại!', 'error'); }
    }

    function handleForgot() {
        const user = document.getElementById('forgotUser').value.trim();
        const email = document.getElementById('forgotEmail').value.trim();
        const savedData = localStorage.getItem(user);
        if (savedData && JSON.parse(savedData).email === email) {
            showStatus(`✉️ Mã khôi phục: [${Math.floor(100000 + Math.random()*900000)}] gửi đến ${email}!`, 'success');
        } else { showStatus('Thông tin nhập sai!', 'error'); }
    }

    function showStatus(text, type) { statusMsg.innerText = text; statusMsg.className = `status-msg ${type === 'success' ? 'text-success' : 'text-error'}`; }
    function clearStatus() { statusMsg.innerText = ''; statusMsg.className = 'status-msg'; }

    // --- ĐIỂM DANH ---
    function claimDay1() {
        const day1Box = document.getElementById('day1');
        if (day1Box.classList.contains('claimed')) return;
        day1Box.classList.remove('active-claim');
        day1Box.classList.add('claimed');
        totalCoins += 1000;
        userCoinsTxt.innerText = totalCoins.toLocaleString();
        setTimeout(() => { unlockPopup.classList.remove('hidden'); }, 400);
    }

    function confirmUnlock(isYes) {
        unlockPopup.classList.add('hidden');
        if (isYes) {
            totalCoins -= 1000;
            let bonusFixedDays = 3000 + 4000 + 5000 + 6000 + 6000;
            let rocketRandomCoins = Math.floor(Math.random() * (20000 - 1000 + 1)) + 1000;
            totalCoins += (bonusFixedDays + rocketRandomCoins);
            userCoinsTxt.innerText = totalCoins.toLocaleString();
            for (let i = 2; i <= 7; i++) { document.getElementById(`day${i}`).classList.add('claimed'); }
            alert(`🚀 PHÓNG TÊN LỬA THÀNH CÔNG!\n\nNhận trọn bộ 24.000 Xu cố định.\nTên lửa nổ ra thêm: +${rocketRandomCoins.toLocaleString()} Xu!`);
        }
    }

    // --- LƯỚT MỜ ---
    function handleScrollFade() {
        const cards = document.querySelectorAll('.charity-card');
        const containerTop = mainWebsite.getBoundingClientRect().top;
        const containerBottom = mainWebsite.getBoundingClientRect().bottom;
        cards.forEach(card => {
            const cardRect = card.getBoundingClientRect();
            if (cardRect.top >= containerTop - 20 && cardRect.bottom <= containerBottom + 20) {
                card.classList.add('visible-active');
            } else {
                card.classList.remove('visible-active');
            }
        });
    }

    // --- NỔ PHÁO HOA KHI DONATE ---
    function createExplosion(x, y) {
        const colors = ['#4caf50', '#81c784', '#ffeb3b', '#ff9800', '#00bcd4', '#e91e63'];
        for (let i = 0; i < 35; i++) {
            const particle = document.createElement('div');
            particle.classList.add('particle');
            particle.style.background = colors[Math.floor(Math.random() * colors.length)];
            particle.style.left = x + 'px';
            particle.style.top = y + 'px';
            const moveX = (Math.random() - 0.5) * 250;
            const moveY = (Math.random() - 0.5) * 250;
            particle.style.setProperty('--mx', `${moveX}px`);
            particle.style.setProperty('--my', `${moveY}px`);
            const size = Math.random() * 8 + 4;
            particle.style.width = size + 'px';
            particle.style.height = size + 'px';
            document.body.appendChild(particle);
            setTimeout(() => { particle.remove(); }, 800);
        }
    }

    function donateToCharity(buttonEl, amount) {
        if (totalCoins < amount) { alert("Số dư xu của bạn không đủ rồi! 💰🌱"); return; }
        totalCoins -= amount;
        donatedCoins += amount;
        userCoinsTxt.innerText = totalCoins.toLocaleString();
        const rect = buttonEl.getBoundingClientRect();
        const posX = rect.left + window.scrollX + (rect.width / 2);
        const posY = rect.top + window.scrollY + (rect.height / 2);
        createExplosion(posX, posY);

        if (donatedCoins >= 10000 && richBadge.classList.contains('hidden')) {
            setTimeout(() => {
                richBadge.classList.remove('hidden');
                alert("🏆 KINH NGẠC CHƯA!! 🎉\n\nBạn chính thức nhận danh hiệu cao quý: [The Richest in the World]!");
            }, 500);
        }
    }

    // --- JOKE PHỤC SINH CỦA CHỦ THỚT ---
    function triggerMonkeyJoke() {
        alert("dumamay ấn vào đay lcdj");
    }
</script>
</body>
</html>
