
<html lang="fa">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>بازی الگوی اشکال</title>
    <style>
        @font-face {
            font-family: 'Vazir';
            src: url('https://cdn.fontcdn.ir/Font/Persian/Vazir/Vazir.eot');
            src: url('https://cdn.fontcdn.ir/Font/Persian/Vazir/Vazir.eot?#iefix') format('embedded-opentype'),
                 url('https://cdn.fontcdn.ir/Font/Persian/Vazir/Vazir.woff2') format('woff2'),
                 url('https://cdn.fontcdn.ir/Font/Persian/Vazir/Vazir.woff') format('woff'),
                 url('https://cdn.fontcdn.ir/Font/Persian/Vazir/Vazir.ttf') format('truetype');
            font-weight: normal;
            font-style: normal;
        }
        
        body {
            font-family: 'Vazir', sans-serif;
            direction: rtl;
            text-align: center;
            background-color: #f5f5f5;
            margin: 0;
            padding: 20px;
            color: #333;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        
        .game-logo {
            max-width: 180px;
            height: auto;
            margin-bottom: 20px;
            border-radius: 10px;
            box-shadow: 0 4px 8px rgba(0,0,0,0.1);
        }
        
        h1 {
            color: #4CAF50;
            margin-top: 10px;
        }
        
        .question-container {
            margin: 20px 0;
        }
        
        .shapes-container {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            margin: 20px 0;
            gap: 20px;
        }
        
        .shape {
            display: flex;
            flex-wrap: wrap;
            width: 120px;
            min-height: 120px;
            border: 2px dashed #ccc;
            padding: 10px;
            justify-content: center;
            align-items: center;
            border-radius: 8px;
        }
        
        .shape-placeholder {
            background-color: #f9f9f9;
            min-height: 120px;
            cursor: pointer;
        }
        
        .square, .circle {
            margin: 3px;
            cursor: pointer;
            transition: transform 0.2s;
        }
        
        .square:hover, .circle:hover {
            transform: scale(1.1);
        }
        
        .square {
            width: 30px;
            height: 30px;
            background-color: #4CAF50;
        }
        
        .circle {
            width: 30px;
            height: 30px;
            background-color: #2196F3;
            border-radius: 50%;
        }
        
        .drag-container {
            margin: 20px 0;
        }
        
        .draggable-shapes {
            display: flex;
            justify-content: center;
            flex-wrap: wrap;
            gap: 10px;
            margin: 15px 0;
            min-height: 50px;
        }
        
        .controls {
            display: flex;
            justify-content: center;
            gap: 15px;
            flex-wrap: wrap;
            margin-top: 20px;
        }
        
        .check-btn, .reset-btn {
            background-color: #4CAF50;
            color: white;
            border: none;
            padding: 12px 24px;
            font-size: 16px;
            border-radius: 5px;
            cursor: pointer;
            font-family: 'Vazir', sans-serif;
            transition: background-color 0.3s;
        }
        
        .reset-btn {
            background-color: #FF9800;
        }
        
        .check-btn:hover {
            background-color: #45a049;
        }
        
        .reset-btn:hover {
            background-color: #e68a00;
        }
        
        .feedback {
            margin-top: 20px;
            font-weight: bold;
            font-size: 18px;
            padding: 10px;
            border-radius: 5px;
        }
        
        .correct {
            color: #4CAF50;
            background-color: #e8f5e9;
        }
        
        .incorrect {
            color: #F44336;
            background-color: #ffebee;
        }
        
        .hidden {
            display: none;
        }
        
        .congratulations {
            color: #4CAF50;
            font-size: 24px;
            font-weight: bold;
            margin-top: 30px;
            padding: 20px;
            background-color: #e8f5e9;
            border-radius: 10px;
        }
        
        /* طراحی واکنش‌گرا برای موبایل */
        @media (max-width: 600px) {
            .container {
                padding: 15px;
            }
            
            .shapes-container {
                gap: 15px;
            }
            
            .shape {
                width: 100px;
                min-height: 100px;
            }
            
            .game-logo {
                max-width: 140px;
            }
            
            h1 {
                font-size: 1.5rem;
            }
            
            .check-btn, .reset-btn {
                padding: 10px 20px;
                font-size: 14px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <img src="https://raw.githubusercontent.com/Riazzuu/logo/main/8.png" alt="لوگوی بازی" class="game-logo">
        <h1>بازی الگوی اشکال</h1>
        
        <div id="question1" class="question-container">
            <h2>سوال ۱: شکل بعدی را بساز</h2>
            
            <div class="shapes-container">
                <div class="shape">
                    <div class="square"></div>
                </div>
                <div class="shape">
                    <div class="square"></div>
                    <div class="square"></div>
                    <div class="square"></div>
                </div>
                <div id="target1" class="shape shape-placeholder"></div>
            </div>
            
            <div class="drag-container">
                <p>روی مربع‌ها کلیک کنید تا به محل مورد نظر منتقل شوند:</p>
                <div class="draggable-shapes" id="source1">
                    <div class="square" onclick="moveShape(this, 1)" id="sq1-1"></div>
                    <div class="square" onclick="moveShape(this, 1)" id="sq1-2"></div>
                    <div class="square" onclick="moveShape(this, 1)" id="sq1-3"></div>
                    <div class="square" onclick="moveShape(this, 1)" id="sq1-4"></div>
                    <div class="square" onclick="moveShape(this, 1)" id="sq1-5"></div>
                    <div class="square" onclick="moveShape(this, 1)" id="sq1-6"></div>
                    <div class="square" onclick="moveShape(this, 1)" id="sq1-7"></div>
                    <div class="square" onclick="moveShape(this, 1)" id="sq1-8"></div>
                </div>
            </div>
            
            <div class="controls">
                <button class="check-btn" onclick="checkAnswer(1)">بررسی پاسخ</button>
                <button class="reset-btn" onclick="resetQuestion(1)">شروع مجدد</button>
            </div>
            <div id="feedback1" class="feedback"></div>
        </div>
        
        <div id="question2" class="question-container hidden">
            <h2>سوال ۲: شکل بعدی را بساز</h2>
            
            <div class="shapes-container">
                <div class="shape">
                    <div class="circle"></div>
                    <div class="circle"></div>
                </div>
                <div class="shape">
                    <div class="circle"></div>
                    <div class="circle"></div>
                    <div class="circle"></div>
                    <div class="circle"></div>
                </div>
                <div id="target2" class="shape shape-placeholder"></div>
            </div>
            
            <div class="drag-container">
                <p>روی دایره‌ها کلیک کنید تا به محل مورد نظر منتقل شوند:</p>
                <div class="draggable-shapes" id="source2">
                    <div class="circle" onclick="moveShape(this, 2)" id="cr2-1"></div>
                    <div class="circle" onclick="moveShape(this, 2)" id="cr2-2"></div>
                    <div class="circle" onclick="moveShape(this, 2)" id="cr2-3"></div>
                    <div class="circle" onclick="moveShape(this, 2)" id="cr2-4"></div>
                    <div class="circle" onclick="moveShape(this, 2)" id="cr2-5"></div>
                    <div class="circle" onclick="moveShape(this, 2)" id="cr2-6"></div>
                    <div class="circle" onclick="moveShape(this, 2)" id="cr2-7"></div>
                    <div class="circle" onclick="moveShape(this, 2)" id="cr2-8"></div>
                    <div class="circle" onclick="moveShape(this, 2)" id="cr2-9"></div>
                </div>
            </div>
            
            <div class="controls">
                <button class="check-btn" onclick="checkAnswer(2)">بررسی پاسخ</button>
                <button class="reset-btn" onclick="resetQuestion(2)">شروع مجدد</button>
            </div>
            <div id="feedback2" class="feedback"></div>
        </div>
        
        <div id="question3" class="question-container hidden">
            <h2>سوال ۳: شکل بعدی را بساز</h2>
            
            <div class="shapes-container">
                <div class="shape">
                    <div class="square"></div>
                    <div class="square"></div>
                    <div class="square"></div>
                    <div class="square"></div>
                </div>
                <div class="shape">
                    <div class="square"></div>
                    <div class="square"></div>
                    <div class="square"></div>
                    <div class="square"></div>
                    <div class="square"></div>
                    <div class="square"></div>
                    <div class="square"></div>
                </div>
                <div id="target3" class="shape shape-placeholder"></div>
            </div>
            
            <div class="drag-container">
                <p>روی مربع‌ها کلیک کنید تا به محل مورد نظر منتقل شوند:</p>
                <div class="draggable-shapes" id="source3">
                    <div class="square" onclick="moveShape(this, 3)" id="sq3-1"></div>
                    <div class="square" onclick="moveShape(this, 3)" id="sq3-2"></div>
                    <div class="square" onclick="moveShape(this, 3)" id="sq3-3"></div>
                    <div class="square" onclick="moveShape(this, 3)" id="sq3-4"></div>
                    <div class="square" onclick="moveShape(this, 3)" id="sq3-5"></div>
                    <div class="square" onclick="moveShape(this, 3)" id="sq3-6"></div>
                    <div class="square" onclick="moveShape(this, 3)" id="sq3-7"></div>
                    <div class="square" onclick="moveShape(this, 3)" id="sq3-8"></div>
                    <div class="square" onclick="moveShape(this, 3)" id="sq3-9"></div>
                    <div class="square" onclick="moveShape(this, 3)" id="sq3-10"></div>
                    <div class="square" onclick="moveShape(this, 3)" id="sq3-11"></div>
                    <div class="square" onclick="moveShape(this, 3)" id="sq3-12"></div>
                </div>
            </div>
            
            <div class="controls">
                <button class="check-btn" onclick="checkAnswer(3)">بررسی پاسخ</button>
                <button class="reset-btn" onclick="resetQuestion(3)">شروع مجدد</button>
            </div>
            <div id="feedback3" class="feedback"></div>
        </div>
        
        <div id="congratulations" class="congratulations hidden">
            تبریک! شما تمام سوالات را با موفقیت به پایان رساندید.
            <div style="margin-top: 20px;">
                <button class="reset-btn" onclick="resetGame()">شروع مجدد بازی</button>
            </div>
        </div>
    </div>

    <script>
        // تابع برای انتقال شکل با کلیک
        function moveShape(element, questionNum) {
            var target = document.getElementById("target" + questionNum);
            
            // اگر شکل قبلاً در ناحیه هدف است، آن را برگردان
            if (element.parentNode.id === "target" + questionNum) {
                var source = document.getElementById("source" + questionNum);
                source.appendChild(element);
            } else {
                // در غیر این صورت، شکل را به ناحیه هدف منتقل کن
                target.appendChild(element);
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
                
                // بعد از 2 ثانیه به سوال بعدی برو
                setTimeout(function() {
                    document.getElementById("question" + questionNum).classList.add("hidden");
                    
                    if (questionNum < 3) {
                        document.getElementById("question" + (questionNum + 1)).classList.remove("hidden");
                    } else {
                        document.getElementById("congratulations").classList.remove("hidden");
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
        }
    </script>
</body>
</html>
