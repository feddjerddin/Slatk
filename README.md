# Slatk
 اوقات الصلاة 
<!DOCTYPE html>
<html lang="ar">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>مواقيت الصلاة والقبلة</title>
    <style>
        body { 
            font-family: Arial, sans-serif; 
            text-align: center; 
            background: url('https://upload.wikimedia.org/wikipedia/commons/9/9a/Grand_Mosque_Mecca.jpg') no-repeat center center fixed; 
            background-size: cover;
            direction: rtl; 
            color: white;
        }
        h1 { color: #FFD700; text-shadow: 2px 2px 4px #000; }
        #container { 
            margin: 20px auto; 
            padding: 20px; 
            background: rgba(0, 0, 0, 0.7); 
            border-radius: 10px; 
            width: 80%; 
            max-width: 400px; 
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.5); 
        }
        button { 
            padding: 10px 15px; 
            margin: 10px; 
            background: #FFD700; 
            color: black; 
            border: none; 
            border-radius: 5px; 
            cursor: pointer; 
            font-weight: bold;
        }
        button:hover { background: #FFC107; }
        #qibla img { width: 100px; margin-top: 10px; }
        .ad { 
            margin-top: 20px; 
            padding: 10px; 
            background: rgba(255, 255, 0, 0.7); 
            border-radius: 5px; 
            color: black; 
            font-weight: bold; 
        }
    </style>
</head>
<body>

    <h1>مواقيت الصلاة</h1>
    <div id="container">
        <button onclick="getPrayerTimes()">عرض أوقات الصلاة</button>
        <div id="prayer-times"></div>
    </div>

    <h1>دعاء اليوم</h1>
    <div id="container">
        <p id="daily-dua">يتم تحديث الدعاء يوميًا...</p>
    </div>

    <h1>اتجاه القبلة</h1>
    <div id="container">
        <button onclick="getQiblaDirection()">عرض اتجاه القبلة</button>
        <div id="qibla"></div>
    </div>

    <h1>التقويم الهجري</h1>
    <div id="container">
        <button onclick="getHijriDate()">عرض التاريخ الهجري</button>
        <p id="hijri-date"></p>
    </div>

    <!-- مساحة الإعلانات -->
    <div class="ad">
        <p>إعلان مخصص هنا - يمكن استبداله بإعلان Google AdSense</p>
    </div>

    <script src="script.js"></script>

</body>
</html>
function getPrayerTimes() {
    navigator.geolocation.getCurrentPosition(position => {
        let lat = position.coords.latitude;
        let lon = position.coords.longitude;
        let apiUrl = `https://api.aladhan.com/v1/timings?latitude=${lat}&longitude=${lon}&method=2`;

        fetch(apiUrl)
        .then(response => response.json())
        .then(data => {
            let times = data.data.timings;
            let output = `<h2>مواقيت الصلاة</h2>`;
            for (let prayer in times) {
                output += `<p><strong>${prayer}</strong>: ${times[prayer]}</p>`;
            }
            document.getElementById("prayer-times").innerHTML = output;
        })
        .catch(error => console.error("حدث خطأ:", error));
    });
}

const duas = [
    "اللهم اجعلني لك شاكراً، لك ذاكراً، لك مخبتاً إليك أواهاً منيباً.",
    "اللهم أصلح لي ديني الذي هو عصمة أمري، وأصلح لي دنياي التي فيها معاشي.",
    "اللهم اجعلنا من عبادك الصالحين، المتقين، المقربين.",
    "اللهم إني أسألك علماً نافعاً، ورزقاً طيباً، وعملاً متقبلاً.",
    "اللهم اغفر لي ذنوبي، وخطاياي، وجميع زلاتي."
];

function showDailyDua() {
    let todayIndex = new Date().getDate() % duas.length;
    document.getElementById("daily-dua").innerText = duas[todayIndex];
}

function getQiblaDirection() {
    navigator.geolocation.getCurrentPosition(position => {
        let lat = position.coords.latitude;
        let lon = position.coords.longitude;
        let apiUrl = `https://api.aladhan.com/v1/qibla/${lat}/${lon}`;

        fetch(apiUrl)
        .then(response => response.json())
        .then(data => {
            let qiblaDirection = data.data.direction;
            document.getElementById("qibla").innerHTML = `
                <p>زاوية القبلة: ${qiblaDirection.toFixed(2)}°</p>
                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/4/40/Kaaba_at_Masjid_al-Haram.jpg/320px-Kaaba_at_Masjid_al-Haram.jpg" alt="اتجاه القبلة">
            `;
        })
        .catch(error => console.error("حدث خطأ أثناء جلب اتجاه القبلة:", error));
    });
}

function getHijriDate() {
    let apiUrl = `https://api.aladhan.com/v1/gToH/${new Date().toISOString().split('T')[0]}`;

    fetch(apiUrl)
    .then(response => response.json())
    .then(data => {
        let hijriDate = data.data.hijri.date;
        document.getElementById("hijri-date").innerText = `التاريخ الهجري: ${hijriDate}`;
    })
    .catch(error => console.error("حدث خطأ أثناء جلب التاريخ الهجري:", error));
}

// تشغيل الدعاء اليومي عند تحميل الصفحة
showDailyDua();
