<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=yes">
  <title>أخبار السوق الكروي</title>
  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@400;700;800&display=swap" rel="stylesheet">
  <!-- Font Awesome (أيقونات) -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }

    body {
      font-family: 'Tajawal', sans-serif;
      background-color: #0b0e14;
      color: #f0f3f8;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 20px 16px 40px;
    }

    .container {
      max-width: 800px;
      width: 100%;
    }

    /* Header و البحث */
    .header {
      display: flex;
      flex-direction: column;
      gap: 20px;
      margin-bottom: 28px;
    }

    .main-title {
      font-size: 2.2rem;
      font-weight: 800;
      letter-spacing: -0.5px;
      background: linear-gradient(135deg, #f6d365 0%, #fda085 100%);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      text-shadow: 0 0 20px rgba(253, 160, 133, 0.2);
      text-align: center;
      line-height: 1.2;
    }

    .search-box {
      display: flex;
      align-items: center;
      background: #1e2430;
      border-radius: 60px;
      padding: 6px 18px 6px 6px;
      border: 1px solid #2e3748;
      transition: border 0.2s;
      box-shadow: 0 8px 16px rgba(0,0,0,0.4);
    }

    .search-box:focus-within {
      border-color: #f6d365;
      box-shadow: 0 0 0 3px rgba(246, 211, 101, 0.2);
    }

    .search-box i {
      color: #8896ab;
      font-size: 1.1rem;
      margin-left: 8px;
    }

    .search-box input {
      flex: 1;
      background: transparent;
      border: none;
      padding: 14px 0;
      color: #f0f3f8;
      font-size: 1rem;
      font-family: 'Tajawal', sans-serif;
      outline: none;
    }

    .search-box input::placeholder {
      color: #6b7a91;
      font-weight: 400;
    }

    /* بطاقات الأخبار (عرض الأخبار) */
    .news-section {
      background: #141a24;
      border-radius: 28px;
      padding: 20px 16px;
      margin-bottom: 30px;
      box-shadow: 0 12px 28px rgba(0,0,0,0.6);
      border: 1px solid #232b39;
    }

    .news-section h2 {
      font-size: 1.2rem;
      font-weight: 700;
      color: #f6d365;
      margin-bottom: 18px;
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .news-item {
      background: #1c2432;
      border-radius: 18px;
      padding: 16px 18px;
      margin-bottom: 14px;
      border-right: 4px solid #f6d365;
      transition: background 0.15s;
    }

    .news-item:last-child {
      margin-bottom: 0;
    }

    .news-item h3 {
      font-size: 1.1rem;
      font-weight: 700;
      margin-bottom: 6px;
      color: #ffffff;
    }

    .news-item p {
      color: #b6c4db;
      font-size: 0.95rem;
      line-height: 1.6;
    }

    .news-meta {
      display: flex;
      justify-content: space-between;
      margin-top: 12px;
      color: #7e8ca5;
      font-size: 0.85rem;
      border-top: 1px solid #2a3446;
      padding-top: 10px;
    }

    /* بوت المحادثة (Chatbot) */
    .chatbot-wrapper {
      background: #141a24;
      border-radius: 28px;
      padding: 20px 16px;
      border: 1px solid #232b39;
      box-shadow: 0 12px 28px rgba(0,0,0,0.6);
      margin-top: 8px;
    }

    .chatbot-header {
      display: flex;
      align-items: center;
      gap: 12px;
      margin-bottom: 18px;
    }

    .chatbot-header i {
      font-size: 1.8rem;
      color: #f6d365;
      background: #1e2636;
      padding: 8px;
      border-radius: 16px;
    }

    .chatbot-header h2 {
      font-size: 1.3rem;
      font-weight: 700;
      color: #f0f3f8;
    }

    .chatbot-header span {
      background: #2d8a4e;
      font-size: 0.7rem;
      padding: 2px 12px;
      border-radius: 40px;
      color: white;
      font-weight: 700;
      margin-right: auto;
    }

    .chat-input-area {
      display: flex;
      flex-direction: column;
      gap: 12px;
    }

    .chat-input-row {
      display: flex;
      align-items: center;
      background: #1e2430;
      border-radius: 60px;
      padding: 4px 4px 4px 18px;
      border: 1px solid #2e3748;
      transition: border 0.2s;
    }

    .chat-input-row:focus-within {
      border-color: #f6d365;
    }

    .chat-input-row input {
      flex: 1;
      background: transparent;
      border: none;
      padding: 14px 0;
      color: #f0f3f8;
      font-size: 1rem;
      font-family: 'Tajawal', sans-serif;
      outline: none;
    }

    .chat-input-row input::placeholder {
      color: #6b7a91;
    }

    .chat-input-row button {
      background: linear-gradient(145deg, #f6d365, #fda085);
      border: none;
      color: #0b0e14;
      font-weight: 700;
      padding: 10px 22px;
      border-radius: 60px;
      cursor: pointer;
      font-family: 'Tajawal', sans-serif;
      font-size: 0.95rem;
      display: flex;
      align-items: center;
      gap: 8px;
      transition: transform 0.1s, box-shadow 0.2s;
      box-shadow: 0 6px 14px rgba(253, 160, 133, 0.25);
    }

    .chat-input-row button:active {
      transform: scale(0.96);
    }

    .chat-input-row button i {
      font-size: 1rem;
    }

    /* مخرجات البوت */
    .chat-output {
      margin-top: 20px;
      background: #0e141e;
      border-radius: 24px;
      padding: 18px 20px;
      min-height: 80px;
      border: 1px solid #26303f;
      transition: all 0.2s;
    }

    .chat-output .response-placeholder {
      color: #6b7a91;
      font-size: 0.95rem;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .chat-output .response-placeholder i {
      color: #f6d365;
    }

    .chat-output .bot-answer {
      color: #eef3fc;
      line-height: 1.8;
      font-size: 1rem;
      white-space: pre-wrap;
      word-break: break-word;
    }

    .chat-output .bot-answer strong {
      color: #f6d365;
    }

    .loading-dots {
      display: flex;
      gap: 6px;
      align-items: center;
      color: #b6c4db;
    }

    .loading-dots span {
      width: 8px;
      height: 8px;
      background: #f6d365;
      border-radius: 50%;
      display: inline-block;
      animation: pulse 1.2s infinite;
    }

    .loading-dots span:nth-child(2) { animation-delay: 0.2s; }
    .loading-dots span:nth-child(3) { animation-delay: 0.4s; }

    @keyframes pulse {
      0%, 60%, 100% { opacity: 0.3; transform: scale(0.8); }
      30% { opacity: 1; transform: scale(1.2); }
    }

    /* تذييل بسيط */
    .footer-note {
      margin-top: 30px;
      font-size: 0.8rem;
      color: #4b5a72;
      text-align: center;
    }

    /* توافق الجوال */
    @media (max-width: 480px) {
      .main-title {
        font-size: 1.8rem;
      }
      .chat-input-row {
        flex-wrap: wrap;
        background: transparent;
        padding: 0;
        border: none;
        gap: 8px;
      }
      .chat-input-row input {
        background: #1e2430;
        border-radius: 60px;
        padding: 14px 18px;
        border: 1px solid #2e3748;
        width: 100%;
      }
      .chat-input-row button {
        width: 100%;
        justify-content: center;
        padding: 14px;
      }
      .news-item h3 {
        font-size: 1rem;
      }
    }
  </style>
</head>
<body>
  <div class="container">

    <!-- HEADER + البحث -->
    <div class="header">
      <h1 class="main-title"><i class="fas fa-futbol" style="margin-left: 10px; -webkit-text-fill-color: initial; color: #f6d365;"></i> أخبار السوق الكروي</h1>
      <div class="search-box">
        <i class="fas fa-search"></i>
        <input type="text" id="searchInput" placeholder="ابحث عن أخبار أو لاعب... (واجهة فقط)">
      </div>
    </div>

    <!-- عرض الأخبار (نموذجية) -->
    <div class="news-section">
      <h2><i class="fas fa-newspaper" style="color: #fda085;"></i> آخر الأخبار</h2>
      <div class="news-item">
        <h3>⚽ صفقة مدوية: نجم الهلال ينتقل إلى الدوري الإنجليزي</h3>
        <p>أعلن نادي الهلال السعودي عن رحيل نجمه الأول إلى أحد أندية البريميرليغ في صفقة تقدر بـ 80 مليون يورو.</p>
        <div class="news-meta"><span>منذ ساعة</span><span><i class="far fa-eye"></i> 2.4k</span></div>
      </div>
      <div class="news-item">
        <h3>🇪🇸 برشلونة يستهدف جناح الريدز في الميركاتو الصيفي</h3>
        <p>وفقاً لمصادر مقربة، وضع برشلونة الجناح المصري محمد صلاح على رأس قائمة التعاقدات للموسم القادم.</p>
        <div class="news-meta"><span>منذ ٣ ساعات</span><span><i class="far fa-eye"></i> 1.8k</span></div>
      </div>
      <div class="news-item">
        <h3>🏆 جائزة الكرة الذهبية: قائمة المرشحين النهائية</h3>
        <p>كشفت فرانس فوتبول عن القائمة المختصرة لجائزة الكرة الذهبية 2026 والتي تضم 5 نجوم كبار.</p>
        <div class="news-meta"><span>منذ ٥ ساعات</span><span><i class="far fa-eye"></i> 3.1k</span></div>
      </div>
    </div>

    <!-- بوت المحادثة Gemini -->
    <div class="chatbot-wrapper">
      <div class="chatbot-header">
        <i class="fas fa-robot"></i>
        <h2>بوت السوق الرياضي</h2>
        <span>Gemini AI</span>
      </div>

      <div class="chat-input-area">
        <div class="chat-input-row">
          <input type="text" id="userQuestion" placeholder="اسأل عن أخبار، انتقالات، أو أي سؤال رياضي...">
          <button id="sendQuestionBtn"><i class="fas fa-paper-plane"></i> إرسال</button>
        </div>
      </div>

      <!-- منطقة عرض الإجابة -->
      <div class="chat-output" id="chatOutput">
        <div class="response-placeholder" id="placeholderMsg">
          <i class="fas fa-comment-dots"></i> انتظر سؤالك الرياضي هنا...
        </div>
        <div id="botAnswerContainer"></div>
      </div>
    </div>

    <div class="footer-note">
      <i class="fas fa-shield-alt" style="margin-left: 6px;"></i> يعمل بواسطة Google Gemini API
    </div>
  </div>

  <script>
    (function() {
      // ============================================
      // 1. ضع مفتاح API الخاص بك هنا
      // ============================================
      const GEMINI_API_KEY = "YOUR_GEMINI_API_KEY";  // <-- استبدل بـ مفتاحك الحقيقي
      // نموذج Gemini (يفضل استخدام أحدث نموذج)
      const MODEL_NAME = "gemini-1.5-flash"; // أو gemini-1.5-pro

      // عناصر DOM
      const searchInput = document.getElementById('searchInput');
      const userQuestionInput = document.getElementById('userQuestion');
      const sendBtn = document.getElementById('sendQuestionBtn');
      const chatOutput = document.getElementById('chatOutput');
      const placeholderMsg = document.getElementById('placeholderMsg');
      const botAnswerContainer = document.getElementById('botAnswerContainer');

      // دالة مساعدة لإظهار حالة التحميل
      function showLoading() {
        placeholderMsg.style.display = 'none';
        botAnswerContainer.innerHTML = `
          <div class="loading-dots">
            <span></span><span></span><span></span>
            <span style="margin-right: 8px; color: #b6c4db;">يرسل إلى Gemini...</span>
          </div>
        `;
      }

      // دالة لعرض الإجابة من البوت
      function displayBotAnswer(answerText) {
        // إزالة أي تحميل أو رسائل سابقة
        placeholderMsg.style.display = 'none';
        // تنسيق الإجابة: إضافة بعض التنسيق البسيط (خط عريض للكلمات المفتاحية) اختياري
        const formatted = answerText
          .replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>')
          .replace(/\n/g, '<br>');
        botAnswerContainer.innerHTML = `<div class="bot-answer">${formatted}</div>`;
      }

      // دالة عرض خطأ بسيط
      function showError(message) {
        placeholderMsg.style.display = 'none';
        botAnswerContainer.innerHTML = `
          <div class="bot-answer" style="color: #fda085;">
            <i class="fas fa-exclamation-circle"></i> ${message}
          </div>
        `;
      }

      // الدالة الأساسية للاتصال بـ Gemini API
      async function askGemini(question) {
        // إذا لم يكن المفتاح صحيحاً
        if (!GEMINI_API_KEY || GEMINI_API_KEY === "YOUR_GEMINI_API_KEY") {
          showError('⚠️ يرجى إضافة مفتاح Gemini API في الكود (انظر الشرح).');
          return;
        }

        if (!question.trim()) {
          showError('الرجاء كتابة سؤال رياضي.');
          return;
        }

        // عرض حالة التحميل
        showLoading();

        try {
          // بناء جسم الطلب حسب وثائق Gemini API (v1)
          const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/${MODEL_NAME}:generateContent?key=${GEMINI_API_KEY}`;

          const payload = {
            contents: [
              {
                role: "user",
                parts: [
                  { text: `أنت بوت رياضي خبير في كرة القدم والأخبار الرياضية. أجب على السؤال التالي بشكل مختصر ومفيد: ${question}` }
                ]
              }
            ],
            generationConfig: {
              temperature: 0.7,
              maxOutputTokens: 400,
            }
          };

          const response = await fetch(apiUrl, {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json',
            },
            body: JSON.stringify(payload)
          });

          // معالجة الأخطاء
          if (!response.ok) {
            let errorMsg = `خطأ في الاتصال (${response.status})`;
            try {
              const errData = await response.json();
              if (errData.error && errData.error.message) {
                errorMsg += `: ${errData.error.message}`;
              }
            } catch (_) {}
            throw new Error(errorMsg);
          }

          const data = await response.json();

          // استخراج النص من الرد
          if (data.candidates && data.candidates.length > 0) {
            const candidate = data.candidates[0];
            if (candidate.content && candidate.content.parts && candidate.content.parts.length > 0) {
              const answerText = candidate.content.parts[0].text || 'لم أتلقَ إجابة. حاول مرة أخرى.';
              displayBotAnswer(answerText);
            } else {
              showError('لم يتم العثور على محتوى في الرد.');
            }
          } else {
            showError('الرد من Gemini لا يحتوي على مرشحين (candidates).');
          }

        } catch (error) {
          console.error('Gemini API error:', error);
          showError(`❌ فشل الاتصال: ${error.message || 'يرجى التحقق من المفتاح أو الاتصال.'}`);
        }
      }

      // مستمعات الأحداث
      sendBtn.addEventListener('click', function() {
        const question = userQuestionInput.value.trim();
        if (question) {
          askGemini(question);
        } else {
          // تنبيه بسيط
          placeholderMsg.style.display = 'flex';
          placeholderMsg.innerHTML = '<i class="fas fa-exclamation-triangle"></i> اكتب سؤالاً رياضياً أولاً.';
          botAnswerContainer.innerHTML = '';
        }
      });

      // إرسال بالضغط على Enter في حقل السؤال
      userQuestionInput.addEventListener('keydown', function(e) {
        if (e.key === 'Enter') {
          e.preventDefault();
          sendBtn.click();
        }
      });

      // (البحث في الأعلى مجرد واجهة - لا وظيفة حقيقية)
      searchInput.addEventListener('keydown', function(e) {
        if (e.key === 'Enter') {
          alert(`🔍 تم البحث عن: "${searchInput.value}" (واجهة فقط)`);
        }
      });

      // رسالة ترحيب في البداية
      setTimeout(() => {
        if (placeholderMsg) {
          placeholderMsg.innerHTML = '<i class="fas fa-futbol"></i> اسأل البوت عن أخبار الانتقالات، المباريات، أو أي سؤال رياضي!';
        }
      }, 300);
    })();
  </script>
</body>
</html>
