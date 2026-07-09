<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
    <title>دينار - منصة العملات الرقمية</title>
    <!-- Chart.js مجاني -->
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js">
    </script>
    <!-- Font Awesome -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background: #0b0e1a;
            color: #e0e4f0;
            padding: 20px;
        }

        .container {
            max-width: 1300px;
            margin: 0 auto;
        }

        /* Header */
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            flex-wrap: wrap;
            gap: 20px;
            background: #141a2b;
            padding: 15px 25px;
            border-radius: 24px;
            margin-bottom: 30px;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.6);
        }

        .logo h1 {
            font-size: 28px;
            color: #f5b041;
            letter-spacing: 1px;
        }

        .logo span {
            color: #fff;
            font-weight: 300;
        }

        .prices {
            display: flex;
            flex-wrap: wrap;
            gap: 18px;
            font-size: 14px;
        }

        .price-item {
            background: #1e263b;
            padding: 6px 14px;
            border-radius: 30px;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .price-item .coin {
            font-weight: 600;
        }

        .green {
            color: #2ecc71;
        }
        .red {
            color: #e74c3c;
        }

        .btn-all {
            background: #2a334a;
            padding: 8px 18px;
            border-radius: 30px;
            color: #fff;
            text-decoration: none;
            font-size: 14px;
            transition: 0.3s;
        }
        .btn-all:hover {
            background: #3a455f;
        }

        /* Grid */
        .grid-2col {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 25px;
            margin-bottom: 30px;
        }

        .card {
            background: #141a2b;
            border-radius: 24px;
            padding: 22px 25px;
            box-shadow: 0 8px 20px rgba(0, 0, 0, 0.5);
            transition: 0.2s;
        }

        .card h3 {
            font-size: 18px;
            margin-bottom: 16px;
            color: #f5b041;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .card h3 i {
            color: #f1c40f;
        }

        /* newsletter */
        .newsletter {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            align-items: center;
        }
        .newsletter input {
            flex: 1;
            padding: 12px 18px;
            border-radius: 40px;
            border: none;
            background: #1e263b;
            color: #fff;
            font-size: 14px;
            min-width: 180px;
        }
        .newsletter input::placeholder {
            color: #7a85a3;
        }
        .newsletter button {
            background: #f5b041;
            border: none;
            padding: 12px 28px;
            border-radius: 40px;
            font-weight: 600;
            color: #0b0e1a;
            cursor: pointer;
            transition: 0.3s;
        }
        .newsletter button:hover {
            background: #e6a035;
        }

        .social-icons a {
            color: #aab3d0;
            margin-left: 12px;
            font-size: 20px;
            transition: 0.3s;
        }
        .social-icons a:hover {
            color: #f5b041;
        }

        /* stats */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
            gap: 15px;
            margin-top: 10px;
        }
        .stat-box {
            background: #1e263b;
            padding: 14px 10px;
            border-radius: 16px;
            text-align: center;
        }
        .stat-box .number {
            font-size: 22px;
            font-weight: 700;
            color: #fff;
        }
        .stat-box .label {
            font-size: 12px;
            color: #8d98b9;
            margin-top: 4px;
        }

        /* latest news */
        .news-item {
            background: #1a2236;
            padding: 14px 18px;
            border-radius: 16px;
            margin-bottom: 12px;
            display: flex;
            justify-content: space-between;
            flex-wrap: wrap;
            align-items: center;
        }
        .news-item .tag {
            background: #2a334a;
            padding: 4px 14px;
            border-radius: 20px;
            font-size: 12px;
            color: #f5b041;
        }
        .news-item .date {
            color: #7a85a3;
            font-size: 13px;
        }

        /* ICO / إدراج جديد */
        .ico-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 12px;
            margin-top: 10px;
        }
        .ico-card {
            background: #1e263b;
            padding: 14px 12px;
            border-radius: 16px;
            text-align: center;
        }
        .ico-card .name {
            font-weight: 600;
        }
        .ico-card .chain {
            font-size: 12px;
            color: #8d98b9;
        }
        .ico-card .amount {
            color: #2ecc71;
            font-weight: 600;
        }
        .ico-card .badge {
            background: #2a334a;
            padding: 2px 12px;
            border-radius: 30px;
            font-size: 11px;
            color: #f5b041;
            display: inline-block;
            margin-top: 4px;
        }

        /* chart wrapper */
        .chart-wrapper {
            margin-top: 20px;
            background: #0f1525;
            padding: 15px;
            border-radius: 20px;
            height: 200px;
            position: relative;
        }
        .chart-wrapper canvas {
            width: 100% !important;
            height: 100% !important;
        }

        /* footer */
        .footer {
            text-align: center;
            color: #5a6582;
            font-size: 14px;
            margin-top: 40px;
            border-top: 1px solid #1e263b;
            padding-top: 25px;
        }

        @media (max-width: 800px) {
            .grid-2col {
                grid-template-columns: 1fr;
            }
            .header {
                flex-direction: column;
                align-items: stretch;
            }
            .prices {
                justify-content: center;
            }
        }
    </style>
</head>
<body>
    <div class="container">

        <!-- HEADER -->
        <header class="header">
            <div class="logo">
                <h1>دينار <span>|</span> Dinar</h1>
            </div>
            <div class="prices" id="livePrices">
                <!-- سيتم ملؤها بواسطة JS -->
            </div>
            <a href="#" class="btn-all"><i class="fas fa-arrow-left"></i> عرض جميع العملات</a>
        </header>

        <!-- GRID 2 COL -->
        <div class="grid-2col">

            <!-- العمود الأيمن: نشرة + إحصائيات + رسم بياني -->
            <div class="card">
                <h3><i class="fas fa-envelope"></i> اشتراك في نشرتنا البريدية</h3>
                <div class="newsletter">
                    <input type="email" placeholder="أدخل بريدك الإلكتروني" />
                    <button>اشتراك</button>
                </div>
                <div style="margin: 18px 0 6px;">
                    <span class="social-icons">
                        <a href="#"><i class="fab fa-twitter"></i></a>
                        <a href="#"><i class="fab fa-telegram"></i></a>
                        <a href="#"><i class="fab fa-youtube"></i></a>
                        <a href="#"><i class="fab fa-discord"></i></a>
                    </span>
                </div>

                <hr style="border-color: #1e263b; margin: 20px 0;" />

                <h3><i class="fas fa-chart-pie"></i> كل ما تحتاجه في عالم العملات الرقمية</h3>
                <div class="stats-grid">
                    <div class="stat-box"><div class="number">$2.45T</div><div class="label">إجمالي حجم السوق</div></div>
                    <div class="stat-box"><div class="number">78,560</div><div class="label">إجمالي المستخدمين</div></div>
                    <div class="stat-box"><div class="number">142</div><div class="label">إجمالي الاتصالات</div></div>
                    <div class="stat-box"><div class="number">2,458</div><div class="label">إجمالي العملات</div></div>
                </div>

                <!-- رسم بياني (شموع محاكاة) -->
                <div style="margin-top: 18px;">
                    <h3 style="font-size:15px;"><i class="fas fa-chart-line"></i> حركة السوق (BTC)</h3>
                    <div class="chart-wrapper">
                        <canvas id="btcChart"></canvas>
                    </div>
                </div>
            </div>

            <!-- العمود الأيسر: آخر الأخبار + الاتصالات الحالية + إدراج جديد -->
            <div class="card">
                <h3><i class="fas fa-newspaper"></i> آخر الأخبار</h3>
                <div class="news-item">
                    <span><span class="tag">AI</span> مشروع Binance: كفاءة الاستطلاع</span>
                    <span class="date">مايو 2024</span>
                </div>
                <div class="news-item">
                    <span><span class="tag">DeFi</span> إطلاق منصة جديدة للرهن</span>
                    <span class="date">مايو 2024</span>
                </div>
                <div class="news-item">
                    <span><span class="tag">BTC</span> تحليل: اتجاه صاعد قوي</span>
                    <span class="date">أبريل 2024</span>
                </div>

                <hr style="border-color: #1e263b; margin: 20px 0;" />

                <h3><i class="fas fa-link"></i> الاتصالات الحالية</h3>
                <div class="ico-grid">
                    <div class="ico-card"><div class="name">DeFi Plus</div><div class="chain">متعدد السلسل</div><div class="amount">$1.78M</div><span class="badge">جديد</span></div>
                    <div class="ico-card"><div class="name">DeFi</div><div class="chain">متعدد السلسل</div><div class="amount">$4.00M</div></div>
                    <div class="ico-card"><div class="name">Gaming</div><div class="chain">متعدد السلسل</div><div class="amount">$2.00M</div></div>
                    <div class="ico-card"><div class="name">MetaGame</div><div class="chain">متعدد السلسل</div><div class="amount">$960K</div></div>
                    <div class="ico-card"><div class="name">GreenChain</div><div class="chain">متعدد السلسل</div><div class="amount">$1.12M</div></div>
                    <div class="ico-card"><div class="name">ERC-20</div><div class="chain">متعدد السلسل</div><div class="amount">37%</div></div>
                </div>

                <!-- إعلان إدراج جديد (مصدر مجاني) -->
                <div style="margin-top: 18px; background: #1e263b; border-radius: 16px; padding: 12px 18px; border-right: 4px solid #f5b041;">
                    <p style="display: flex; align-items: center; gap: 10px;">
                        <i class="fas fa-bullhorn" style="color: #f5b041;"></i>
                        <strong>🆕 إدراج جديد:</strong> <span style="color: #f1c40f;">Asteroid Token</span> 
                        <span style="background: #2a334a; padding: 2px 14px; border-radius: 30px; font-size: 12px;">IDO قادم</span>
                    </p>
                    <p style="font-size: 13px; color: #aab3d0; margin-top: 4px;">مصدر: CoinGecko • ١٥ مايو ٢٠٢٤</p>
                </div>
            </div>
        </div>

        <!-- مقالات مجانية عن حركة السوق -->
        <div class="card" style="margin-top: 10px;">
            <h3><i class="fas fa-feather-alt"></i> مقالات مجانية عن حركة السوق</h3>
            <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 15px;">
                <div style="background: #1a2236; padding: 14px; border-radius: 16px;">
                    <h4 style="color: #f5b041;">BTC يتجاوز 68K</h4>
                    <p style="font-size: 13px; color: #bcc3dc;">تحليل فني: الاختراق قادم مع حجم تداول مرتفع.</p>
                    <span style="color: #7a85a3; font-size: 12px;"><i class="far fa-clock"></i> ٢ ساعة</span>
                </div>
                <div style="background: #1a2236; padding: 14px; border-radius: 16px;">
                    <h4 style="color: #f5b041;">Altcoin موسم</h4>
                    <p style="font-size: 13px; color: #bcc3dc;">السيولة تتدفق إلى العملات البديلة، ننصح بالمتابعة.</p>
                    <span style="color: #7a85a3; font-size: 12px;"><i class="far fa-clock"></i> ٥ ساعات</span>
                </div>
                <div style="background: #1a2236; padding: 14px; border-radius: 16px;">
                    <h4 style="color: #f5b041;">تحليل السوق الأسبوعي</h4>
                    <p style="font-size: 13px; color: #bcc3dc;">تقرير شامل عن حركة BTC و ETH وBNB.</p>
                    <span style="color: #7a85a3; font-size: 12px;"><i class="far fa-clock"></i> ١ يوم</span>
                </div>
            </div>
        </div>

        <footer class="footer">
            <p>جميع الحقوق محفوظة © 2024 دينار - منصة العملات الرقمية</p>
            <p style="font-size: 12px; margin-top: 6px;">بيانات مجانية من CoinGecko API • تصميم احترافي</p>
        </footer>
    </div>

    <script>
        // ========== 1. أسعار العملات الحية (CoinGecko مجاني) ==========
        async function fetchPrices() {
            try {
                const ids = 'bitcoin,ethereum,binancecoin,solana,ripple';
                const url =
                    `https://api.coingecko.com/api/v3/simple/price?ids=${ids}&vs_currencies=usd&include_24hr_change=true`;
                const res = await fetch(url);
                const data = await res.json();

                const map = {
                    bitcoin: { symbol: 'BTC', name: 'BTC' },
                    ethereum: { symbol: 'ETH', name: 'ETH' },
                    binancecoin: { symbol: 'BNB', name: 'BNB' },
                    solana: { symbol: 'SOL', name: 'SOL' },
                    ripple: { symbol: 'XRP', name: 'XRP' }
                };

                let html = '';
                for (const [key, coin] of Object.entries(map)) {
                    const info = data[key];
                    if (info) {
                        const price = info.usd.toFixed(2);
                        const change = info.usd_24h_change.toFixed(2);
                        const cls = change >= 0 ? 'green' : 'red';
                        const arrow = change >= 0 ? '▲' : '▼';
                        html += `
                            <div class="price-item">
                                <span class="coin">${coin.symbol}</span>
                                $${price} 
                                <span class="${cls}">${arrow} ${Math.abs(change)}%</span>
                            </div>
                        `;
                    }
                }
                document.getElementById('livePrices').innerHTML = html;
            } catch (e) {
                console.warn('API غير متاحة، نعرض بيانات افتراضية');
                // بيانات احتياطية
                document.getElementById('livePrices').innerHTML = `
                    <div class="price-item"><span class="coin">BTC</span> $67,842.21 <span class="green">▲ 1.35%</span></div>
                    <div class="price-item"><span class="coin">ETH</span> $3,512.18 <span class="green">▲ 2.41%</span></div>
                    <div class="price-item"><span class="coin">BNB</span> $592.72 <span class="green">▲ 0.98%</span></div>
                    <div class="price-item"><span class="coin">SOL</span> $166.35 <span class="red">▼ 1.23%</span></div>
                    <div class="price-item"><span class="coin">XRP</span> $0.5221 <span class="green">▲ 0.65%</span></div>
                `;
            }
        }
        fetchPrices();

        // ========== 2. رسم بياني (شموع محاكاة باستخدام Chart.js) ==========
        const ctx = document.getElementById('btcChart').getContext('2d');

        // بيانات محاكاة لشكل يشبه الشموع (استخدمنا خط مع نقاط لإعطاء إحساس)
        const labels = ['أبريل', 'مايو', 'يونيو', 'يوليو', 'أغسطس', 'سبتمبر', 'أكتوبر'];
        const dataPoints = [62000, 64500, 63000, 67000, 68500, 66000, 67842];

        new Chart(ctx, {
            type: 'line',
            data: {
                labels: labels,
                datasets: [{
                    label: 'BTC/USD',
                    data: dataPoints,
                    borderColor: '#f5b041',
                    backgroundColor: 'rgba(245, 176, 65, 0.05)',
                    borderWidth: 3,
                    pointBackgroundColor: '#f5b041',
                    pointRadius: 4,
                    tension: 0.2,
                    fill: true,
                }]
            },
            options: {
                responsive: true,
                maintainAspectRatio: false,
                plugins: {
                    legend: { display: false },
                    tooltip: { enabled: true }
                },
                scales: {
                    x: {
                        grid: { color: '#1e263b' },
                        ticks: { color: '#7a85a3' }
                    },
                    y: {
                        grid: { color: '#1e263b' },
                        ticks: { color: '#7a85a3' }
                    }
                }
            }
        });

        // ========== 3. عرض كمية التداول وقيمة العملة (إضافي) ==========
        // نضيف معلومات إضافية أسفل الرسم البياني (حجم تداول)
        const extraInfo = document.createElement('div');
        extraInfo.style.cssText = `
            display: flex; justify-content: space-between; flex-wrap: wrap;
            background: #1a2236; padding: 12px 18px; border-radius: 16px;
            margin-top: 15px; font-size: 14px;
        `;
        extraInfo.innerHTML = `
            <span><strong>💰 قيمة BTC:</strong> $67,842.21</span>
            <span><strong>📊 حجم تداول 24h:</strong> $28.4B</span>
            <span><strong>🔄 كمية التداول:</strong> 412,500 BTC</span>
        `;
        // نضيفه بعد الرسم البياني
        const chartWrapper = document.querySelector('.chart-wrapper');
        chartWrapper.parentNode.insertBefore(extraInfo, chartWrapper.nextSibling);

        // ========== 4. مصدر مجاني لإعلان الإدراج الجديد (تم إضافته في HTML) ==========

        // ========== 5. مقالات مجانية (موجودة في HTML) ==========

        console.log('✅ موقع دينار جاهز مع رسم بياني وأسعار حية وإدراج جديد!');
    </script>

</body>
</html>
