<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>أوقات الصلاة</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>أوقات الصلاة</h1>
        <nav>
            <ul>
                <li><a href="index.html">الرئيسية</a></li>
                <li><a href="privacy.html">سياسة الخصوصية</a></li>
            </ul>
        </nav>
    </header>
    <main>
        <div id="prayer-times">
            <h2>أوقات الصلاة اليوم</h2>
            <p>جارٍ تحميل أوقات الصلاة...</p>
        </div>
        <div id="qibla-direction">
            <h2>اتجاه القبلة</h2>
            <p id="qibla">جارٍ تحميل اتجاه القبلة...</p>
        </div>
        <div id="daily-content">
            <h2>دعاء اليوم</h2>
            <p id="dua">جارٍ تحميل الدعاء...</p>
            <h2>حديث اليوم</h2>
            <p id="hadith">جارٍ تحميل الحديث...</p>
        </div>
    </main>
    <footer>
        <p>© 2023 موقع أوقات الصلاة. جميع الحقوق محفوظة.</p>
    </footer>
    <script src="script.js"></script>
</body>
</html>
<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>سياسة الخصوصية</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <header>
        <h1>سياسة الخصوصية</h1>
        <nav>
            <ul>
                <li><a href="index.html">الرئيسية</a></li>
                <li><a href="privacy.html">سياسة الخصوصية</a></li>
            </ul>
        </nav>
    </header>
    <main>
        <div class="privacy-policy">
            <h2>سياسة الخصوصية</h2>
            <p>
                نحن نحترم خصوصيتك ونلتزم بحماية بياناتك الشخصية. هذه السياسة توضح كيفية تعاملنا مع المعلومات التي نجمعها منك.
            </p>
            <h3>1. المعلومات التي نجمعها</h3>
            <p>
                نجمع معلومات مثل الموقع الجغرافي لتحديد أوقات الصلاة واتجاه القبلة.
            </p>
            <h3>2. استخدام المعلومات</h3>
            <p>
                نستخدم المعلومات لتوفير خدمات مثل أوقات الصلاة واتجاه القبلة.
            </p>
            <h3>3. مشاركة المعلومات</h3>
            <p>
                نحن لا نشارك معلوماتك الشخصية مع أطراف خارجية.
            </p>
        </div>
    </main>
    <footer>
        <p>© 2023 موقع أوقات الصلاة. جميع الحقوق محفوظة.</p>
    </footer>
</body>
</html>
body {
    font-family: 'Arial', sans-serif;
    text-align: center;
    margin: 0;
    padding: 0;
    background: linear-gradient(270deg, #4CAF50, #2196F3, #FFC107, #E91E63);
    background-size: 400% 400%;
    animation: GradientBackground 15s ease infinite;
    color: #333;
}

@keyframes GradientBackground {
    0% { background-position: 0% 50%; }
    50% { background-position: 100% 50%; }
    100% { background-position: 0% 50%; }
}

header {
    background-color: rgba(255, 255, 255, 0.8);
    padding: 20px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

header h1 {
    margin: 0;
    font-size: 2.5rem;
    color: #4CAF50;
}

nav ul {
    list-style: none;
    padding: 0;
    margin: 10px 0 0;
}

nav ul li {
    display: inline;
    margin: 0 15px;
}

nav ul li a {
    color: #4CAF50;
    text-decoration: none;
    font-weight: bold;
    font-size: 1.1rem;
}

nav ul li a:hover {
    text-decoration: underline;
}

main {
    padding: 20px;
}

#prayer-times, #qibla-direction, #daily-content, .privacy-policy {
    background-color: rgba(255, 255, 255, 0.9);
    padding: 20px;
    border-radius: 10px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    margin: 20px auto;
    max-width: 600px;
}

footer {
    margin-top: 20px;
    padding: 10px;
    background-color: rgba(255, 255, 255, 0.8);
    box-shadow: 0 -4px 6px rgba(0, 0, 0, 0.1);
    color: #333;
}

footer p {
    margin: 0;
    font-size: 0.9rem;
}

/* تحسينات للجوال */
@media (max-width: 600px) {
    header h1 {
        font-size: 2rem;
    }

    nav ul li {
        display: block;
        margin: 10px 0;
    }

    #prayer-times, #qibla-direction, #daily-content, .privacy-policy {
        padding: 15px;
        margin: 10px;
    }
}
document.addEventListener('DOMContentLoaded', function() {
    const apiUrl = 'https://api.aladhan.com/v1/timingsByCity?city=Cairo&country=Egypt&method=5';
    const qiblaApiUrl = 'https://api.aladhan.com/v1/qibla/21.4225/39.8262'; // إحداثيات مكة المكرمة

    // مصفوفة تحتوي على مجموعة من الأدعية
    const adiya = [
        "اللهم إني أسألك علماً نافعاً، ورزقاً طيباً، وعملاً متقبلاً.",
        "اللهم إني أعوذ بك من الهم والحزن، والعجز والكسل، والبخل والجبن، وضلع الدين وغلبة الرجال.",
        "اللهم إني أسألك رحمة من عندك تهدي بها قلبي، وتجمع بها شملي، وتلم بها شعثي.",
        "اللهم إني أسألك من الخير كله عاجله وآجله ما علمت منه وما لم أعلم، وأعوذ بك من الشر كله عاجله وآجله ما علمت منه وما لم أعلم."
    ];

    // مصفوفة تحتوي على مجموعة من الأحاديث
    const ahadith = [
        "قال رسول الله صلى الله عليه وسلم: «من صلى علي صلاة واحدة صلى الله عليه عشرًا». (صحيح مسلم)",
        "قال رسول الله صلى الله عليه وسلم: «الكلمة الطيبة صدقة». (صحيح البخاري)",
        "قال رسول الله صلى الله عليه وسلم: «من كان يؤمن بالله واليوم الآخر فليقل خيرًا أو ليصمت». (صحيح البخاري)",
        "قال رسول الله صلى الله عليه وسلم: «لا يؤمن أحدكم حتى يحب لأخيه ما يحب لنفسه». (صحيح البخاري)"
    ];

    // اختيار دعاء وحديث عشوائي
    const randomDua = adiya[Math.floor(Math.random() * adiya.length)];
    const randomHadith = ahadith[Math.floor(Math.random() * ahadith.length)];

    // عرض الدعاء والحديث
    document.getElementById('dua').textContent = randomDua;
    document.getElementById('hadith').textContent = randomHadith;

    // جلب أوقات الصلاة
    fetch(apiUrl)
        .then(response => response.json())
        .then(data => {
            const timings = data.data.timings;
            const prayerTimesDiv = document.getElementById('prayer-times');
            prayerTimesDiv.innerHTML = `
                <p>الفجر: ${timings.Fajr}</p>
                <p>الشروق: ${timings.Sunrise}</p>
                <p>الظهر: ${timings.Dhuhr}</p>
                <p>العصر: ${timings.Asr}</p>
                <p>المغرب: ${timings.Maghrib}</p>
                <p>العشاء: ${timings.Isha}</p>
            `;
        })
        .catch(error => {
            console.error('Error fetching prayer times:', error);
            document.getElementById('prayer-times').innerHTML = '<p>حدث خطأ أثناء جلب أوقات الصلاة.</p>';
        });

    // جلب اتجاه القبلة
    fetch(qiblaApiUrl)
        .then(response => response.json())
        .then(data => {
            const qiblaDirection = data.data.direction;
            document.getElementById('qibla').textContent = `اتجاه القبلة: ${qiblaDirection} درجة من الشمال.`;
        })
        .catch(error => {
            console.error('Error fetching qibla direction:', error);
            document.getElementById('qibla').textContent = 'حدث خطأ أثناء جلب اتجاه القبلة.';
        });

    // إشعارات الصلاة
    function showPrayerNotification(prayerName, prayerTime) {
        if (Notification.permission === 'granted') {
            new Notification(`حان وقت صلاة ${prayerName}`, {
                body: `الوقت الحالي: ${prayerTime}`,
                icon: 'icon.png'
            });
        }
    }

    // طلب إذن الإشعارات
    if (Notification.permission !== 'granted') {
        Notification.requestPermission();
    }
});
