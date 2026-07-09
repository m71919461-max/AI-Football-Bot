// ============================================================
// 🔑 ضع مفتاحك المجاني من football-data.org هنا
// ============================================================
const API_KEY = 'bd01eb568cc742e29ef9d187db92d334'; // ⬅️ استبدل هذا بمفتاحك

// ============================================================
// 1. التبديل بين التبويبات
// ============================================================
const tabs = document.querySelectorAll('.tab-btn');
const contents = document.querySelectorAll('.tab-content');

tabs.forEach(tab => {
    tab.addEventListener('click', () => {
        tabs.forEach(t => t.classList.remove('active'));
        contents.forEach(c => c.classList.remove('active'));
        tab.classList.add('active');
        document.getElementById(tab.dataset.tab).classList.add('active');
    });
});

// ============================================================
// 2. جلب الأخبار عبر RSS مجاني
// ============================================================
async function fetchNews() {
    const container = document.getElementById('news-container');
    try {
        const rssUrl = 'https://www.fcbarcelonanoticias.com/rss';
        const proxy = 'https://api.rss2json.com/v1/api.json?rss_url=';
        const response = await fetch(proxy + encodeURIComponent(rssUrl));
        const data = await response.json();

        if (data.status === 'ok' && data.items.length > 0) {
            container.innerHTML = data.items.slice(0, 10).map(item => `
                <div class="news-card">
                    <h3>${item.title}</h3>
                    <p>${item.description.replace(/<[^>]+>/g, '').slice(0, 160)}...</p>
                    <small>📅 ${new Date(item.pubDate).toLocaleDateString('ar-EG')}</small>
                    <br><a href="${item.link}" target="_blank">📖 اقرأ المزيد</a>
                </div>
            `).join('');
        } else {
            container.innerHTML = '⚠️ لا توجد أخبار حالياً. حاول لاحقاً.';
        }
    } catch (error) {
        container.innerHTML = '❌ تعذر تحميل الأخبار. تأكد من اتصال الإنترنت.';
        console.error('News error:', error);
    }
}

// ============================================================
// 3. جلب الانتقالات (بيانات ثابتة + قابل للتحديث)
// ============================================================
async function fetchTransfers() {
    const container = document.getElementById('transfers-container');
    try {
        // يمكنك تحديث هذه القائمة يدوياً أو جلبها من RSS آخر
        const transfers = [
            { player: 'جوليس كوندي', from: 'إشبيلية', to: 'برشلونة', status: '✅ تم التعاقد' },
            { player: 'رافينيا', from: 'ليدز يونايتد', to: 'برشلونة', status: '✅ تم التعاقد' },
            { player: 'روبرت ليفاندوفسكي', from: 'بايرن ميونخ', to: 'برشلونة', status: '✅ تم التعاقد' },
            { player: 'فرانك كيسيي', from: 'ميلان', to: 'برشلونة', status: '✅ تم التعاقد' },
            { player: 'أندرياس كريستنسن', from: 'تشيلسي', to: 'برشلونة', status: '✅ تم التعاقد' },
            { player: 'عثمان ديمبيلي', from: 'برشلونة', to: 'باريس سان جيرمان', status: '❌ رحل' },
            { player: 'ميمفيس ديباي', from: 'برشلونة', to: 'أتلتيكو مدريد', status: '❌ رحل' },
        ];
        container.innerHTML = transfers.map(t => `
            <div class="transfer-card">
                <strong style="font-size:1.1rem;">${t.player}</strong>
                <span style="color:#555;">من</span>
                <span style="color:#003366; font-weight:600;">${t.from}</span>
                <span style="color:#555;">إلى</span>
                <span style="color:#a50044; font-weight:600;">${t.to}</span>
                <span style="background:${t.status.includes('✅') ? '#27ae60' : '#e74c3c'}; 
                     color:white; padding:4px 16px; border-radius:50px; font-size:0.85rem; 
                     display:inline-block; margin-top:6px;">
                    ${t.status}
                </span>
            </div>
        `).join('');
    } catch (error) {
        container.innerHTML = '❌ تعذر تحميل الانتقالات.';
        console.error('Transfers error:', error);
    }
}

// ============================================================
// 4. جلب الترتيب عبر football-data.org
// ============================================================
async function fetchStandings() {
    const container = document.getElementById('standings-container');
    try {
        const response = await fetch('https://api.football-data.org/v4/competitions/PD/standings', {
            headers: { 'X-Auth-Token': API_KEY }
        });
        
        if (!response.ok) throw new Error(`HTTP ${response.status}`);
        const data = await response.json();

        if (data.standings && data.standings[0]?.table) {
            const table = data.standings[0].table;
            let rows = table.map(team => `
                <tr class="${team.team.name.includes('Barcelona') ? 'barca-row' : ''}">
                    <td>${team.position}</td>
                    <td style="text-align:right; font-weight:${team.team.name.includes('Barcelona') ? '700' : '400'};">${team.team.name}</td>
                    <td>${team.playedGames}</td>
                    <td>${team.won}</td>
                    <td>${team.draw}</td>
                    <td>${team.lost}</td>
                    <td>${team.goalsFor}</td>
                    <td>${team.goalsAgainst}</td>
                    <td><strong style="font-size:1.1rem; color:#003366;">${team.points}</strong></td>
                </tr>
            `).join('');

            container.innerHTML = `
                <div style="overflow-x:auto;">
                    <table class="standings-table">
                        <thead><tr>
                            <th>#</th><th>النادي</th><th>لعب</th><th>فوز</th>
                            <th>تعادل</th><th>خسارة</th><th>له</th><th>عليه</th><th>نقاط</th>
                        </tr></thead>
                        <tbody>${rows}</tbody>
                    </table>
                </div>
                <p style="margin-top:18px; color:#888; font-size:0.9rem;">🔵 صف برشلونة باللون الأزرق الفاتح</p>
                <p style="color:#aaa; font-size:0.8rem;">📊 آخر تحديث: ${new Date().toLocaleString('ar-EG')}</p>
            `;
        } else {
            container.innerHTML = '⚠️ لا توجد بيانات ترتيب حالياً.';
        }
    } catch (error) {
        container.innerHTML = `❌ تعذر تحميل الترتيب. ${error.message.includes('429') ? 'تجاوزت حد الطلبات، انتظر دقيقة.' : 'تأكد من المفتاح.'}`;
        console.error('Standings error:', error);
    }
}

// ============================================================
// 5. جلب المباريات القادمة
// ============================================================
async function fetchMatches() {
    const container = document.getElementById('matches-container');
    try {
        const response = await fetch('https://api.football-data.org/v4/teams/81/matches?status=SCHEDULED&limit=8', {
            headers: { 'X-Auth-Token': API_KEY }
        });
        
        if (!response.ok) throw new Error(`HTTP ${response.status}`);
        const data = await response.json();

        if (data.matches && data.matches.length > 0) {
            container.innerHTML = data.matches.map(m => `
                <div class="match-card">
                    <span class="teams">${m.homeTeam.name} 🆚 ${m.awayTeam.name}</span>
                    <span class="date">📅 ${new Date(m.utcDate).toLocaleDateString('ar-EG')} 
                          ⏰ ${new Date(m.utcDate).toLocaleTimeString('ar-EG', {hour:'2-digit', minute:'2-digit'})}</span>
                    <span class="competition">${m.competition.name}</span>
                </div>
            `).join('');
        } else {
            container.innerHTML = '⚠️ لا توجد مباريات قادمة مجدولة حالياً.';
        }
    } catch (error) {
        container.innerHTML = `❌ تعذر تحميل المباريات. ${error.message.includes('429') ? 'تجاوزت حد الطلبات، انتظر دقيقة.' : ''}`;
        console.error('Matches error:', error);
    }
}

// ============================================================
// 6. تشغيل الكل عند تحميل الصفحة
// ============================================================
document.addEventListener('DOMContentLoaded', () => {
    fetchNews();
    fetchTransfers();
    fetchStandings();
    fetchMatches();

    // تحديث الترتيب والمباريات كل 5 دقائق (تجنب تجاوز الحد)
    setInterval(() => {
        fetchStandings();
        fetchMatches();
    }, 300000);
});
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

body {
    background: #f0f2f5;
    color: #1a1a1a;
}

header {
    background: linear-gradient(135deg, #003366, #a50044);
    color: white;
    text-align: center;
    padding: 35px 20px;
    border-bottom: 5px solid #ffd700;
    box-shadow: 0 4px 15px rgba(0,0,0,0.2);
}

header h1 {
    font-size: 3rem;
    letter-spacing: 3px;
    text-shadow: 2px 2px 4px rgba(0,0,0,0.3);
}
header p {
    font-size: 1.3rem;
    opacity: 0.9;
    margin-top: 8px;
}

.tabs {
    display: flex;
    justify-content: center;
    gap: 12px;
    background: white;
    padding: 18px 20px;
    flex-wrap: wrap;
    border-bottom: 3px solid #ddd;
    position: sticky;
    top: 0;
    z-index: 100;
    box-shadow: 0 2px 8px rgba(0,0,0,0.06);
}

.tab-btn {
    background: #e8ecf1;
    border: none;
    padding: 12px 30px;
    font-size: 1.1rem;
    border-radius: 50px;
    cursor: pointer;
    transition: 0.3s ease;
    font-weight: 600;
    color: #333;
}
.tab-btn:hover {
    background: #d0d7e0;
    transform: translateY(-2px);
}
.tab-btn.active {
    background: #003366;
    color: white;
    box-shadow: 0 4px 12px rgba(0,51,102,0.4);
}

main {
    max-width: 1100px;
    margin: 35px auto;
    padding: 0 20px;
}

.tab-content {
    display: none;
    background: white;
    padding: 30px;
    border-radius: 16px;
    box-shadow: 0 6px 20px rgba(0,0,0,0.07);
    animation: fadeIn 0.4s ease;
}
.tab-content.active {
    display: block;
}

@keyframes fadeIn {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
}

h2 {
    color: #003366;
    margin-bottom: 25px;
    border-right: 6px solid #a50044;
    padding-right: 18px;
    font-size: 1.8rem;
}

/* بطاقات الأخبار */
.news-card, .transfer-card {
    background: #f8f9fb;
    padding: 18px 22px;
    margin-bottom: 16px;
    border-radius: 12px;
    border-right: 5px solid #a50044;
    transition: 0.25s ease;
    box-shadow: 0 2px 6px rgba(0,0,0,0.04);
}
.news-card:hover, .transfer-card:hover {
    background: #f0f2f7;
    transform: translateX(-4px);
    box-shadow: 0 4px 12px rgba(0,0,0,0.08);
}
.news-card h3 {
    color: #003366;
    font-size: 1.25rem;
    margin-bottom: 8px;
}
.news-card p {
    color: #555;
    line-height: 1.6;
}
.news-card small {
    color: #999;
    display: block;
    margin-top: 10px;
    font-size: 0.85rem;
}
.news-card a {
    color: #a50044;
    text-decoration: none;
    font-weight: 600;
    font-size: 0.95rem;
}
.news-card a:hover {
    text-decoration: underline;
}

/* جدول الترتيب */
.standings-table {
    width: 100%;
    border-collapse: collapse;
    font-size: 0.95rem;
}
.standings-table th {
    background: #003366;
    color: white;
    padding: 14px 10px;
    text-align: center;
}
.standings-table td {
    padding: 13px 10px;
    text-align: center;
    border-bottom: 1px solid #e8ecf1;
}
.standings-table tr:hover {
    background: #f5f7fa;
}
.barca-row {
    background: #dce8f5 !important;
    font-weight: 700;
    border-right: 4px solid #a50044;
}

/* المباريات */
.match-card {
    background: #f8f9fb;
    padding: 18px 22px;
    margin-bottom: 14px;
    border-radius: 12px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    flex-wrap: wrap;
    gap: 12px;
    transition: 0.25s ease;
    border-left: 4px solid #003366;
}
.match-card:hover {
    background: #f0f2f7;
    transform: scale(1.01);
}
.match-card .teams {
    font-size: 1.2rem;
    font-weight: 700;
    color: #1a1a1a;
}
.match-card .date {
    color: #666;
    font-size: 0.95rem;
}
.match-card .competition {
    background: #003366;
    color: white;
    padding: 5px 14px;
    border-radius: 50px;
    font-size: 0.8rem;
    font-weight: 600;
}

footer {
    text-align: center;
    padding: 30px;
    background: #1a1a1a;
    color: #aaa;
    margin-top: 50px;
    border-top: 4px solid #a50044;
}

/* استجابة الجوال */
@media (max-width: 650px) {
    header h1 { font-size: 2.2rem; }
    .tab-btn { padding: 8px 18px; font-size: 0.85rem; }
    .match-card { flex-direction: column; align-items: flex-start; gap: 6px; }
    .tab-content { padding: 18px; }
    h2 { font-size: 1.4rem; }
    .standings-table { font-size: 0.75rem; }
    .standings-table th, .standings-table td { padding: 8px 4px; }
}
<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>برشلونة - الأخبار والانتقالات</title>
    <link rel="stylesheet" href="style.css" />
</head>
<body>

    <header>
        <h1>🔵🔴 برشلونة</h1>
        <p>آخر الأخبار، الانتقالات، والترتيب</p>
    </header>

    <nav class="tabs">
        <button class="tab-btn active" data-tab="news">📰 الأخبار</button>
        <button class="tab-btn" data-tab="transfers">🔄 الانتقالات</button>
        <button class="tab-btn" data-tab="standings">🏆 الترتيب</button>
        <button class="tab-btn" data-tab="matches">📅 المباريات</button>
    </nav>

    <main>
        <section id="news" class="tab-content active">
            <h2>📰 آخر أخبار برشلونة</h2>
            <div id="news-container">⏳ جاري التحميل...</div>
        </section>

        <section id="transfers" class="tab-content">
            <h2>🔄 سوق الانتقالات</h2>
            <div id="transfers-container">⏳ جاري التحميل...</div>
        </section>

        <section id="standings" class="tab-content">
            <h2>🏆 ترتيب الدوري الإسباني</h2>
            <div id="standings-container">⏳ جاري التحميل...</div>
        </section>

        <section id="matches" class="tab-content">
            <h2>📅 مباريات برشلونة القادمة</h2>
            <div id="matches-container">⏳ جاري التحميل...</div>
        </section>
    </main>

    <footer>
        <p>جميع الحقوق محفوظة © 2026 | مصادر مجانية</p>
    </footer>

    <script src="script.js"></script>
</body>
</html>
