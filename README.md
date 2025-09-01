
<!DOCTYPE html>
<html lang="fa" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>بازی الگوی اشکال</title>
    <link href="https://cdn.jsdelivr.net/gh/rastikerdar/vazirmatn@v33.003/Vazirmatn-font-face.css" rel="stylesheet">
    <style>
        * {
            box-sizing: border-box;
            font-family: Vazirmatn, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #6a11cb 0%, #2575fc 100%);
            margin: 0;
            padding: 20px;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            color: #333;
        }
        
        .container {
            background-color: white;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            width: 90%;
            max-width: 900px;
            padding: 30px;
            text-align: center;
            position: relative;
        }
        
        h1 {
            color: #4a148c;
            margin-bottom: 30px;
            font-size: 2.5rem;
            text-shadow: 1px 1px 2px rgba(0,0,0,0.1);
        }
        
        .question-header {
            background: linear-gradient(to right, #4facfe 0%, #00f2fe 100%);
            color: white;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 25px;
            font-size: 1.5rem;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1);
        }
        
        .pattern-explanation {
            background-color: #f5f5f5;
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
            font-size: 1.1rem;
            border-right: 5px solid #4a148c;
        }
        
        .shapes-container {
            display: flex;
            justify-content: space-around;
            margin: 30px 0;
            flex-wrap: wrap;
        }
        
        .shape-box {
            display: flex;
            flex-direction: column;
            align-items: center;
            margin: 10px;
        }
        
        .shape {
            display: flex;
            flex-wrap: wrap;
            width: 150px;
            min-height: 150px;
            border: 2px solid #ddd;
            border-radius: 10px;
            padding: 15px;
            justify-content: center;
            align-items: center;
            background-color: #f9f9f9;
            box-shadow: 0 4px 8px rgba(0,0,0,0.05);
        }
        
        .shape-placeholder {
            background-color: #edf7ff;
            border: 2px dashed #4facfe;
        }
        
        .shape-label {
            margin-top: 10px;
            font-weight: bold;
            color: #4a148c;
        }
        
        .square, .circle {
            margin: 5px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            transition: transform 0.2s;
        }
        
        .square {
            width: 35px;
            height: 35px;
            background: linear-gradient(45deg, #ff9a9e 0%, #fad0c4 99%, #fad0c4 100%);
        }
        
        .circle {
            width: 35px;
            height: 35px;
            background: linear-gradient(45deg, #a1c4fd 0%, #c2e9fb 100%);
            border-radius: 50%;
        }
        
        .drag-container {
            background-color: #f0f9ff;
            border-radius: 15px;
            padding: 20px;
            margin: 20px 0;
            box-shadow: inset 0 0 10px rgba(0,0,0,0.05);
        }
        
        .draggable-shapes {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 15px;
            margin: 20px 0;
            min-height: 80px;
        }
        
        .draggable {
            cursor: grab;
            transition: all 0.3s;
        }
        
        .draggable:hover {
            transform: scale(1.1);
        }
        
        .draggable:active {
            cursor: grabbing;
            transform: scale(1.15);
        }
        
        .controls {
            margin: 30px 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 15px;
        }
        
        .check-btn, .reset-btn {
            background: linear-gradient(to right, #4facfe 0%, #00f2fe 100%);
            color: white;
            border: none;
            padding: 15px 40px;
            font-size: 1.2rem;
            border-radius: 50px;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(79, 172, 254, 0.4);
            transition: all 0.3s;
        }
        
        .reset-btn {
            background: linear-gradient(to right, #ff9a9e 0%, #fad0c4 100%);
            box-shadow: 0 4px 15px rgba(255, 154, 158, 0.4);
            padding: 12px 30px;
            font-size: 1rem;
        }
        
        .check-btn:hover, .reset-btn:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 20px rgba(79, 172, 254, 0.6);
        }
        
        .check-btn:active, .reset-btn:active {
            transform: translateY(1px);
        }
        
        .feedback {
            margin-top: 25px;
            font-weight: bold;
            font-size: 1.3rem;
            min-height: 30px;
            padding: 15px;
            border-radius: 10px;
        }
        
        .correct {
            background-color: #e8f5e9;
            color: #2e7d32;
            border: 2px solid #66bb6a;
        }
        
        .incorrect {
            background-color: #ffebee;
            color: #c62828;
            border: 2px solid #ef5350;
        }
        
        .hidden {
            display: none;
        }
        
        .congratulations {
            background: linear-gradient(45deg, #4facfe 0%, #00f2fe 100%);
            color: white;
            padding: 30px;
            border-radius: 15px;
            margin-top: 30px;
            font-size: 1.8rem;
            box-shadow: 0 6px 20px rgba(0,0,0,0.15);
            animation: pulse 2s infinite;
        }
        
        @keyframes pulse {
            0% { transform: scale(1); }
            50% { transform: scale(1.03); }
            100% { transform: scale(1); }
        }
        
        .progress-container {
            background-color: #e0e0e0;
            border-radius: 10px;
            height: 20px;
            margin: 20px 0;
            overflow: hidden;
        }
        
        .progress-bar {
            height: 100%;
            background: linear-gradient(to right, #4facfe 0%, #00f2fe 100%);
            width: 0%;
            transition: width 0.5s;
            border-radius: 10px;
        }
        
        .question-counter {
            font-size: 1.2rem;
            color: #4a148c;
            margin-bottom: 10px;
        }
        
        @media (max-width: 768px) {
            .shapes-container {
                flex-direction: column;
                align-items: center;
            }
            
            .shape {
                width: 120px;
                min-height: 120px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>بازی الگوی اشکال</h1>
        
        <div class="question-counter">سوال ۱ از ۳</div>
        <div class="progress-container">
            <div class="progress-bar" id="progress"></div>
        </div>
        
        <div id="question1" class="question-container">
            <div class="question-header">سوال ۱: شکل بعدی را بساز</div>
            
            <div class="pattern-explanation">
                الگوی شکل‌ها را تشخیص دهید و شکل بعدی را بسازید.
            </div>
            
            <div class="shapes-container">
                <div class="shape-box">
                    <div class="shape">
                        <div class="square"></div>
                    </div>
                    <div class="shape-label">شکل اول</div>
                </div>
                
                <div class="shape-box">
                    <div class="shape">
                        <div class="square"></div>
                        <div class="square"></div>
                        <div class="square"></div>
                    </div>
                    <div class="shape-label">شکل دوم</div>
                </div>
                
                <div class="shape-box">
                    <div id="target1" class="shape shape-placeholder" ondrop="drop(event, 1)" ondragover="allowDrop(event)"></div>
                    <div class="shape-label">شکل سوم (جای خالی)</div>
                </div>
            </div>
            
            <div class="drag-container">
                <h3>مربع‌ها را به محل مورد نظر بکشید و رها کنید</h3>
                <div class="draggable-shapes" id="source1">
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq1-1"></div>
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq1-2"></div>
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq1-3"></div>
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq1-4"></div>
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq1-5"></div>
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq1-6"></div>
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq1-7"></div>
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq1-8"></div>
                </div>
            </div>
            
            <div class="controls">
                <button class="check-btn" onclick="checkAnswer(1)">بررسی پاسخ</button>
                <button class="reset-btn" onclick="resetQuestion(1)">شروع مجدد این سوال</button>
                <div id="feedback1" class="feedback"></div>
            </div>
        </div>
        
        <div id="question2" class="question-container hidden">
            <div class="question-header">سوال ۲: شکل بعدی را بساز</div>
            
            <div class="pattern-explanation">
                الگوی شکل‌ها را تشخیص دهید و شکل بعدی را بسازید.
            </div>
            
            <div class="shapes-container">
                <div class="shape-box">
                    <div class="shape">
                        <div class="circle"></div>
                        <div class="circle"></div>
                    </div>
                    <div class="shape-label">شکل اول</div>
                </div>
                
                <div class="shape-box">
                    <div class="shape">
                        <div class="circle"></div>
                        <div class="circle"></div>
                        <div class="circle"></div>
                        <div class="circle"></div>
                    </div>
                    <div class="shape-label">شکل دوم</div>
                </div>
                
                <div class="shape-box">
                    <div id="target2" class="shape shape-placeholder" ondrop="drop(event, 2)" ondragover="allowDrop(event)"></div>
                    <div class="shape-label">شکل سوم (جای خالی)</div>
                </div>
            </div>
            
            <div class="drag-container">
                <h3>دایره‌ها را به محل مورد نظر بکشید و رها کنید</h3>
                <div class="draggable-shapes" id="source2">
                    <div class="circle draggable" draggable="true" ondragstart="drag(event)" id="cr2-1"></div>
                    <div class="circle draggable" draggable="true" ondragstart="drag(event)" id="cr2-2"></div>
                    <div class="circle draggable" draggable="true" ondragstart="drag(event)" id="cr2-3"></div>
                    <div class="circle draggable" draggable="true" ondragstart="drag(event)" id="cr2-4"></div>
                    <div class="circle draggable" draggable="true" ondragstart="drag(event)" id="cr2-5"></div>
                    <div class="circle draggable" draggable="true" ondragstart="drag(event)" id="cr2-6"></div>
                    <div class="circle draggable" draggable="true" ondragstart="drag(event)" id="cr2-7"></div>
                    <div class="circle draggable" draggable="true" ondragstart="drag(event)" id="cr2-8"></div>
                    <div class="circle draggable" draggable="true" ondragstart="drag(event)" id="cr2-9"></div>
                </div>
            </div>
            
            <div class="controls">
                <button class="check-btn" onclick="checkAnswer(2)">بررسی پاسخ</button>
                <button class="reset-btn" onclick="resetQuestion(2)">شروع مجدد این سوال</button>
                <div id="feedback2" class="feedback"></div>
            </div>
        </div>
        
        <div id="question3" class="question-container hidden">
            <div class="question-header">سوال ۳: شکل بعدی را بساز</div>
            
            <div class="pattern-explanation">
                الگوی شکل‌ها را تشخیص دهید و شکل بعدی را بسازید.
            </div>
            
            <div class="shapes-container">
                <div class="shape-box">
                    <div class="shape">
                        <div class="square"></div>
                        <div class="square"></div>
                        <div class="square"></div>
                        <div class="square"></div>
                    </div>
                    <div class="shape-label">شکل اول</div>
                </div>
                
                <div class="shape-box">
                    <div class="shape">
                        <div class="square"></div>
                        <div class="square"></div>
                        <div class="square"></div>
                        <div class="square"></div>
                        <div class="square"></div>
                        <div class="square"></div>
                        <div class="square"></div>
                    </div>
                    <div class="shape-label">شکل دوم</div>
                </div>
                
                <div class="shape-box">
                    <div id="target3" class="shape shape-placeholder" ondrop="drop(event, 3)" ondragover="allowDrop(event)"></div>
                    <div class="shape-label">شکل سوم (جای خالی)</div>
                </div>
            </div>
            
            <div class="drag-container">
                <h3>مربع‌ها را به محل مورد نظر بکشید و رها کنید</h3>
                <div class="draggable-shapes" id="source3">
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq3-1"></div>
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq3-2"></div>
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq3-3"></div>
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq3-4"></div>
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq3-5"></div>
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq3-6"></div>
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq3-7"></div>
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq3-8"></div>
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq3-9"></div>
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq3-10"></div>
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq3-11"></div>
                    <div class="square draggable" draggable="true" ondragstart="drag(event)" id="sq3-12"></div>
                </div>
            </div>
            
            <div class="controls">
                <button class="check-btn" onclick="checkAnswer(3)">بررسی پاسخ</button>
                <button class="reset-btn" onclick="resetQuestion(3)">شروع مجدد این سوال</button>
                <div id="feedback3" class="feedback"></div>
            </div>
        </div>
        
        <div id="congratulations" class="congratulations hidden">
            تبریک! شما تمام سوالات را با موفقیت به پایان رساندید.
            <div style="margin-top: 20px;">
                <button class="reset-btn" onclick="resetGame()">شروع مجدد بازی</button>
            </div>
        </div>
    </div>

    <script>
        // متغیرهای وضعیت بازی
        let currentQuestion = 1;
        
        // تابع برای اجازه دادن به رها کردن اشیاء
        function allowDrop(ev) {
            ev.preventDefault();
        }
        
        // تابع برای شروع کشیدن
        function drag(ev) {
            ev.dataTransfer.setData("text", ev.target.id);
        }
        
        // تابع برای رها کردن
        function drop(ev, questionNum) {
            ev.preventDefault();
            var data = ev.dataTransfer.getData("text");
            
            // بررسی می‌کند که آیا المان قبلاً در جای دیگری قرار دارد یا نه
            var element = document.getElementById(data);
            
            // بررسی می‌کند که آیا شکل قبلاً در این ناحیه قرار گرفته است
            if (element.parentNode.id === "target" + questionNum) {
                return; // اگر شکل قبلاً اینجا قرار گرفته، کاری نکن
            }
            
            // بررسی می‌کند که آیا این عنصر یک شکل قابل کشیدن است
            if (element.classList.contains('draggable')) {
                // بررسی می‌کند که آیا در ناحیه هدف فضای خالی وجود دارد
                var target = document.getElementById("target" + questionNum);
                
                // اگر شکل در حال رها شدن روی شکل دیگری است، آن را قبول نکن
                if (ev.target.classList.contains('square') || ev.target.classList.contains('circle')) {
                    return;
                }
                
                // شکل را به ناحیه هدف اضافه کن
                target.appendChild(element);
                
                // موقعیت شکل را به صورت تصادفی در ناحیه هدف تنظیم کن تا از همپوشانی جلوگیری شود
                const shapes = target.getElementsByClassName('square').length + 
                              target.getElementsByClassName('circle').length;
                element.style.position = 'relative';
                element.style.left = (Math.random() * 20 - 10) + 'px';
                element.style.top = (Math.random() * 20 - 10) + 'px';
            }
        }
        
        // تابع برای بررسی پاسخ
        function checkAnswer(questionNum) {
            var target = document.getElementById("target" + questionNum);
            var feedback = document.getElementById("feedback" + questionNum);
            
            // تعداد مربع‌ها یا دایره‌های موجود در ناحیه هدف
            var shapesCount = target.getElementsByClassName("square").length + 
                             target.getElementsByClassName("circle").length;
            
            var correctCount;
            
            // تعیین تعداد صحیح بر اساس شماره سوال
            switch(questionNum) {
                case 1:
                    correctCount = 5;
                    break;
                case 2:
                    correctCount = 6;
                    break;
                case 3:
                    correctCount = 10;
                    break;
            }
            
            if (shapesCount === correctCount) {
                feedback.innerHTML = "آفرین! پاسخ شما صحیح است.";
                feedback.className = "feedback correct";
                
                // به‌روزرسانی نوار پیشرفت
                document.getElementById('progress').style.width = (questionNum * 33.33) + '%';
                
                // بعد از 2 ثانیه به سوال بعدی برو
                setTimeout(function() {
                    document.getElementById("question" + questionNum).classList.add("hidden");
                    
                    if (questionNum < 3) {
                        currentQuestion = questionNum + 1;
                        document.getElementById("question" + currentQuestion).classList.remove("hidden");
                        document.querySelector(".question-counter").textContent = "سوال " + currentQuestion + " از ۳";
                    } else {
                        document.getElementById("congratulations").classList.remove("hidden");
                        document.querySelector(".question-counter").textContent = "تکمیل شد!";
                    }
                }, 2000);
            } else {
                feedback.innerHTML = "پاسخ شما نادرست است. لطفا دوباره تلاش کنید.";
                feedback.className = "feedback incorrect";
            }
        }
        
        // تابع برای ریست کردن سوال فعلی
        function resetQuestion(questionNum) {
            var target = document.getElementById("target" + questionNum);
            var source = document.getElementById("source" + questionNum);
            var feedback = document.getElementById("feedback" + questionNum);
            
            // حذف تمام شکل‌ها از ناحیه هدف و بازگرداندن آنها به منبع
            while (target.firstChild) {
                var child = target.firstChild;
                target.removeChild(child);
                if (child.classList.contains('square') || child.classList.contains('circle')) {
                    source.appendChild(child);
                    child.style.position = 'static';
                }
            }
            
            // پاک کردن پیام بازخورد
            feedback.innerHTML = "";
            feedback.className = "feedback";
        }
        
        // تابع برای ریست کردن کل بازی
        function resetGame() {
            // ریست کردن تمام سوالات
            for (let i = 1; i <= 3; i++) {
                resetQuestion(i);
            }
            
            // پنهان کردن تبریک و نمایش سوال اول
            document.getElementById("congratulations").classList.add("hidden");
            document.querySelectorAll(".question-container").forEach(container => {
                container.classList.add("hidden");
            });
            document.getElementById("question1").classList.remove("hidden");
            
            // ریست کردن نوار پیشرفت
            document.getElementById('progress').style.width = '0%';
            document.querySelector(".question-counter").textContent = "سوال ۱ از ۳";
            currentQuestion = 1;
        }
    </script>
</body>
</html>
