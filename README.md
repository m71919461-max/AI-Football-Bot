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
