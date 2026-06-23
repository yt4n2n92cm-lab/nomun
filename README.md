# nomun
<!DOCTYPE html>
<html lang="mn">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Номунд 💖</title>

<style>
body {
    margin: 0;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background: #ffd6e7;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    overflow: hidden;
    position: relative;
}

.card {
    background: white;
    width: 350px;
    padding: 30px;
    border-radius: 25px;
    text-align: center;
    box-shadow: 0 10px 30px rgba(255, 105, 180, .3);
    z-index: 10;
}

h1 {
    color: #ff4f9a;
    margin-bottom: 10px;
}

h2 {
    color: #4a4a4a;
    font-size: 20px;
}

p {
    color: #666;
}

button {
    padding: 12px 25px;
    border: none;
    border-radius: 20px;
    cursor: pointer;
    margin: 10px;
    font-size: 16px;
    font-weight: bold;
    transition: transform 0.2s;
}

button:active {
    transform: scale(0.95);
}

.yes {
    background: #ff4f9a;
    color: white;
    box-shadow: 0 4px 15px rgba(255, 79, 154, 0.4);
}

.no {
    background: white;
    border: 2px solid #ff4f9a;
    color: #ff4f9a;
}

input[type="date"] {
    padding: 10px;
    border: 2px solid #ff4f9a;
    border-radius: 10px;
    color: #ff4f9a;
    font-size: 16px;
    outline: none;
    margin-top: 10px;
}

.heart {
    position: absolute;
    color: pink;
    animation: float 6s linear infinite;
    pointer-events: none;
    z-index: 1;
}

@keyframes float {
    from {
        transform: translateY(100vh) rotate(0deg);
        opacity: 1;
    }
    to {
        transform: translateY(-100px) rotate(360deg);
        opacity: 0;
    }
}
</style>
</head>
<body>

<div class="card" id="page1">
    <h1>🐰 Номун 💖</h1>
    <p>Чамаас нэг зүйл асуумаар байна...</p>
    <h2>Надтай болзоонд гарах уу? 💕</h2>

    <button class="yes" onclick="nextPage()">ТИЙМ 🥰</button>
    <button class="no" id="noBtn">ҮГҮЙ 🙈</button>
</div>

<script>
// --- ЭНД ӨӨРИЙН МЭДЭЭЛЛЭЭ ОРУУЛААРАЙ ---
const TELEGRAM_BOT_TOKEN = 'ЭНД_БОТЫН_ТОКЕН_БАЙРЛАНА';
const TELEGRAM_CHAT_ID = 'ЭНД_ЧИНИЙ_CHAT_ID_БАЙРЛАНА';

const noBtn = document.getElementById("noBtn");
noBtn.addEventListener("mouseover", () => {
    noBtn.style.position = "absolute";
    noBtn.style.left = Math.random() * 80 + "vw";
    noBtn.style.top = Math.random() * 80 + "vh";
});

function nextPage() {
    document.getElementById("page1").innerHTML = `
    <h1>🥹💖</h1>
    <h2>Баярлалаа Номун!</h2>
    <p>Чи намайг маш их баярлууллаа 💕</p>
    <p>Хэзээ завтай вэ? Өдрөө сонгоорой:</p>
    <input type="date" id="date">
    <br><br>
    <button class="yes" id="submitBtn" onclick="finalPage()">Дараах ➜</button>
    `;
}

function finalPage() {
    let dateVal = document.getElementById("date").value;
    
    if (!dateVal) {
        alert("Завтай өдрөө сонгоорой 😊");
        return;
    }

    // Товчлуурыг түр идэвхгүй болгож, "Уншиж байна..." төлөвт оруулна
    const submitBtn = document.getElementById("submitBtn");
    submitBtn.disabled = true;
    submitBtn.innerText = "Түр хүлээнэ үү...";

    // Telegram руу илгээх зурвас бэлдэх
    const message = `🎉 Номун болзооны урилгыг зөвшөөрлөө! \n📅 Сонгосон өдөр: ${dateVal}`;
    const url = `https://api.telegram.org/bot${TELEGRAM_BOT_TOKEN}/sendMessage`;

    // Мэдэгдэл илгээх хүсэлт (Fetch API)
    fetch(url, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
            chat_id: TELEGRAM_CHAT_ID,
            text: message
        })
    })
    .then(response => {
        // Хүсэлт амжилттай болсон ч, болоогүй ч дараагийн хуудас руу шилжүүлнэ
        showSuccessPage(dateVal);
    })
    .catch(error => {
        console.error("Алдаа гарлаа:", error);
        showSuccessPage(dateVal); 
    });
}

function showSuccessPage(date) {
    document.getElementById("page1").innerHTML = `
    <h1>💘 Болзоо батлагдлаа!</h1>
    <p><b>Нэр:</b> Номун 💕</p>
    <p><b>Өдөр:</b> ${date}</p>
    <hr style="border: 1px inset #ffd6e7; margin: 15px 0;">
    <p>Кино үзэх 🎬</p>
    <p>Кофе уух ☕</p>
    <p>Эсвэл хамт алхах 🌙</p>
    <h3>Тэр өдрийг тэсэн ядан хүлээж байна ❤️</h3>
    `;
}

// Зүрх хөөргөх хэсэг
setInterval(() => {
    let heart = document.createElement("div");
    heart.classList.add("heart");
    heart.innerHTML = "💖";
    heart.style.left = Math.random() * 100 + "vw";
    heart.style.fontSize = (Math.random() * 20 + 15) + "px";
    document.body.appendChild(heart);

    setTimeout(() => {
        heart.remove();
    }, 6000);
}, 400);
</script>

</body>
</html>

