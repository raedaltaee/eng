<!DOCTYPE html>
<html lang="ar" dir="rtl"> <!-- Added dir="rtl" for right-to-left layout -->
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>تطبيق بدون مصادقة</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            font-family: "Inter", sans-serif;
            background-color: #f0f4f8;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            margin: 0;
            padding: 1rem;
            box-sizing: border-box; /* Include padding in element's total width and height */
        }
        .container {
            background-color: #ffffff;
            padding: 2.5rem;
            border-radius: 0.75rem;
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            max-width: 90%;
            width: 400px;
            text-align: center;
            display: flex; /* Use flexbox for internal layout */
            flex-direction: column; /* Stack items vertically */
            gap: 1rem; /* Space between elements */
        }
        .message-box {
            background-color: #ffe0b2; /* برتقالي فاتح */
            color: #e65100; /* برتقالي داكن */
            padding: 1rem;
            border-radius: 0.5rem;
            margin-bottom: 1rem;
            border: 1px solid #ff9800;
            display: none; /* مخفي افتراضياً */
        }
        #appContent {
            margin-top: 1.5rem;
            padding-top: 1.5rem;
            border-top: 1px solid #e2e8f0; /* Light gray border */
            text-align: right; /* Align content to the right for RTL */
            /* This will be displayed by default now */
        }
        #appContent h2 {
            font-size: 1.75rem; /* text-2xl */
            font-weight: 700; /* font-bold */
            color: #334155; /* slate-700 */
            margin-bottom: 0.75rem; /* mb-3 */
        }
        #appContent p {
            font-size: 1rem; /* text-base */
            color: #475569; /* slate-600 */
            line-height: 1.5;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1 class="text-3xl font-bold text-gray-800 mb-6">تطبيق بسيط</h1>
        <div id="messageBox" class="message-box"></div>
        <p id="authStatus" class="text-lg text-gray-700 mb-4">لا توجد مصادقة مطلوبة.</p>
        <p class="text-sm text-gray-500">معرف المستخدم غير متوفر (المصادقة معطلة).<span id="userIdDisplay" class="font-mono"></span></p>

        <!-- Application content, now always visible -->
        <div id="appContent">
            <h2>مرحباً بك في تطبيقك!</h2>
            <p>هذا هو المحتوى الذي يظهر مباشرة لأن المصادقة معطلة.</p>
            <p>يمكنك إضافة وظائف أو معلومات هنا.</p>
            <p id="profileData" class="bg-gray-100 p-3 rounded-md mt-2 text-sm text-gray-700 text-right overflow-auto">
                لا توجد بيانات ملف شخصي من Firestore (المصادقة معطلة).
            </p>
        </div>
    </div>

    <script type="module">
        // تم إزالة جميع وحدات Firebase لأن المصادقة معطلة.

        /**
         * تعرض رسالة للمستخدم في صندوق الرسائل.
         * @param {string} message - الرسالة المراد عرضها.
         * @param {boolean} isError - إذا كانت صحيحة، تعرض الرسالة كخطأ.
         */
        function showMessage(message, isError = false) {
            const messageBox = document.getElementById('messageBox'); // تم نقل التعريف هنا
            if (messageBox) {
                messageBox.textContent = message;
                messageBox.style.display = 'block';
                if (isError) {
                    messageBox.style.backgroundColor = '#ffcdd2'; /* أحمر فاتح */
                    messageBox.style.color = '#b71c1c'; /* أحمر داكن */
                    messageBox.style.borderColor = '#ef5350';
                } else {
                    messageBox.style.backgroundColor = '#e8f5e9'; /* أخضر فاتح */
                    messageBox.style.color = '#2e7d32'; /* أخضر داكن */
                    messageBox.style.borderColor = '#66bb6a';
                }
            } else {
                console.error("Message box element not found.");
            }
        }

        // عند تحميل النافذة، قم بعرض المحتوى مباشرة
        window.onload = function() {
            console.log("Window loaded. Authentication is disabled, displaying content directly.");

            // تم نقل تعريف المتغيرات هنا لضمان أن عناصر DOM جاهزة
            const authStatusElement = document.getElementById('authStatus');
            const userIdDisplayElement = document.getElementById('userIdDisplay');
            const appContentElement = document.getElementById('appContent');
            const profileDataElement = document.getElementById('profileData');

            if (authStatusElement) {
                authStatusElement.textContent = "لا توجد مصادقة مطلوبة.";
            } else {
                console.error("authStatusElement not found.");
            }

            if (userIdDisplayElement) {
                userIdDisplayElement.textContent = "N/A";
            } else {
                console.error("userIdDisplayElement not found.");
            }

            if (profileDataElement) {
                profileDataElement.textContent = "لا توجد بيانات ملف شخصي من Firestore (المصادقة معطلة).";
            } else {
                console.error("profileDataElement not found.");
            }

            showMessage("تم تحميل التطبيق بنجاح. المصادقة معطلة.", false);
        };
    </script>
</body>
</html>
# eng
