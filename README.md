# steelhub
All news and information about steel
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>OreTrack - Real-time Iron Ore Market Intelligence</title>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;500;700&family=Montserrat:wght@600;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
    <style>
        :root {
            --primary: #2c3e50;
            --secondary: #e74c3c;
            --accent: #3498db;
            --success: #27ae60;
            --warning: #f39c12;
            --dark: #1a2530;
            --light: #f8f9fa;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Roboto', sans-serif;
            background: linear-gradient(135deg, #f5f7fa 0%, #e4e7eb 100%);
            color: #333;
            line-height: 1.6;
        }
        
        .container {
            width: 100%;
            max-width: 1400px;
            margin: 0 auto;
            padding: 0 20px;
        }
        
        /* Header Styles */
        header {
            background: linear-gradient(90deg, var(--primary) 0%, var(--dark) 100%);
            color: white;
            padding: 15px 0;
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
            position: sticky;
            top: 0;
            z-index: 100;
        }
        
        .header-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .logo {
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .logo h1 {
            font-family: 'Montserrat', sans-serif;
            font-weight: 700;
            font-size: 1.8rem;
        }
        
        .logo i {
            color: var(--accent);
            font-size: 1.8rem;
        }
        
        .last-update {
            background: rgba(255,255,255,0.1);
            padding: 5px 12px;
            border-radius: 20px;
            font-size: 0.9rem;
        }
        
        .last-update span {
            color: var(--accent);
            font-weight: 500;
        }
        
        /* Hero Section */
        .hero {
            background: url('https://images.unsplash.com/photo-1547996160-81dfa63595aa?ixlib=rb-4.0.3&auto=format&fit=crop&w=1950&q=80') no-repeat center center;
            background-size: cover;
            padding: 60px 0;
            position: relative;
            color: white;
            text-align: center;
        }
        
        .hero::after {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(44, 62, 80, 0.85);
        }
        
        .hero-content {
            position: relative;
            z-index: 2;
            max-width: 800px;
            margin: 0 auto;
            padding: 0 20px;
        }
        
        .hero h2 {
            font-family: 'Montserrat', sans-serif;
            font-size: 2.8rem;
            margin-bottom: 20px;
            line-height: 1.2;
        }
        
        .hero p {
            font-size: 1.2rem;
            margin-bottom: 30px;
            opacity: 0.9;
        }
        
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin-top: 30px;
        }
        
        .stat-card {
            background: rgba(255,255,255,0.1);
            border-radius: 10px;
            padding: 15px;
            backdrop-filter: blur(5px);
        }
        
        .stat-value {
            font-size: 1.8rem;
            font-weight: 700;
            margin-bottom: 5px;
        }
        
        .stat-label {
            font-size: 0.9rem;
            opacity: 0.8;
        }
        
        .trend-up {
            color: var(--success);
        }
        
        .trend-down {
            color: var(--secondary);
        }
        
        /* Main Content */
        .dashboard {
            padding: 40px 0;
        }
        
        .section-title {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 25px;
            border-bottom: 2px solid var(--accent);
            padding-bottom: 10px;
        }
        
        .section-title h2 {
            font-family: 'Montserrat', sans-serif;
            font-size: 1.8rem;
            color: var(--primary);
        }
        
        .section-title i {
            color: var(--accent);
            margin-right: 10px;
        }
        
        .card-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 25px;
            margin-bottom: 40px;
        }
        
        .card {
            background: white;
            border-radius: 12px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.05);
            overflow: hidden;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        
        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.1);
        }
        
        .card-header {
            background: var(--primary);
            color: white;
            padding: 15px 20px;
            font-weight: 500;
        }
        
        .card-body {
            padding: 20px;
        }
        
        .price-display {
            font-size: 2.2rem;
            font-weight: 700;
            text-align: center;
            margin: 15px 0;
            color: var(--primary);
        }
        
        .price-change {
            text-align: center;
            font-weight: 500;
            margin-bottom: 15px;
        }
        
        .chart-container {
            height: 250px;
            position: relative;
            margin: 20px 0;
        }
        
        .api-status {
            display: flex;
            align-items: center;
            padding: 8px 15px;
            border-radius: 20px;
            font-size: 0.9rem;
            margin-top: 15px;
        }
        
        .api-active {
            background: rgba(39, 174, 96, 0.1);
            color: var(--success);
        }
        
        .api-inactive {
            background: rgba(231, 76, 60, 0.1);
            color: var(--secondary);
        }
        
        .status-indicator {
            width: 10px;
            height: 10px;
            border-radius: 50%;
            margin-right: 8px;
        }
        
        .active {
            background: var(--success);
        }
        
        .inactive {
            background: var(--secondary);
        }
        
        /* Market Feed */
        .market-feed {
            background: white;
            border-radius: 12px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.05);
            overflow: hidden;
            margin-bottom: 40px;
        }
        
        .feed-header {
            background: var(--primary);
            color: white;
            padding: 15px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        
        .feed-container {
            max-height: 400px;
            overflow-y: auto;
        }
        
        .feed-item {
            padding: 15px 20px;
            border-bottom: 1px solid #eee;
            display: flex;
        }
        
        .feed-item:last-child {
            border-bottom: none;
        }
        
        .feed-icon {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            margin-right: 15px;
            flex-shrink: 0;
        }
        
        .news-icon {
            background: rgba(52, 152, 219, 0.1);
            color: var(--accent);
        }
        
        .price-icon {
            background: rgba(39, 174, 96, 0.1);
            color: var(--success);
        }
        
        .alert-icon {
            background: rgba(231, 76, 60, 0.1);
            color: var(--secondary);
        }
        
        .feed-content {
            flex-grow: 1;
        }
        
        .feed-title {
            font-weight: 500;
            margin-bottom: 5px;
        }
        
        .feed-time {
            font-size: 0.85rem;
            color: #777;
        }
        
        /* Footer */
        footer {
            background: var(--dark);
            color: white;
            padding: 50px 0 20px;
        }
        
        .footer-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 30px;
            margin-bottom: 30px;
        }
        
        .footer-col h3 {
            font-family: 'Montserrat', sans-serif;
            margin-bottom: 20px;
            font-size: 1.3rem;
            position: relative;
            padding-bottom: 10px;
        }
        
        .footer-col h3::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 50px;
            height: 2px;
            background: var(--accent);
        }
        
        .footer-links {
            list-style: none;
        }
        
        .footer-links li {
            margin-bottom: 12px;
        }
        
        .footer-links a {
            color: #ddd;
            text-decoration: none;
            transition: color 0.3s;
            display: flex;
            align-items: center;
        }
        
        .footer-links a:hover {
            color: var(--accent);
        }
        
        .footer-links i {
            margin-right: 10px;
            width: 20px;
            text-align: center;
        }
        
        .social-links {
            display: flex;
            gap: 15px;
            margin-top: 20px;
        }
        
        .social-icon {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            background: rgba(255,255,255,0.1);
            color: white;
            font-size: 1.2rem;
            transition: all 0.3s;
        }
        
        .social-icon:hover {
            background: var(--accent);
            transform: translateY(-3px);
        }
        
        .copyright {
            text-align: center;
            padding-top: 20px;
            border-top: 1px solid rgba(255,255,255,0.1);
            font-size: 0.9rem;
            color: #aaa;
        }
        
        /* Responsive */
        @media (max-width: 768px) {
            .header-container {
                flex-direction: column;
                gap: 15px;
            }
            
            .hero h2 {
                font-size: 2.2rem;
            }
            
            .price-display {
                font-size: 1.8rem;
            }
        }
    </style>
</head>
<body>
    <!-- Header -->
    <header>
        <div class="container header-container">
            <div class="logo">
                <i class="fas fa-chart-line"></i>
                <h1>OreTrack</h1>
            </div>
            <div class="last-update">
                Last update: <span id="update-time">Just now</span>
            </div>
        </div>
    </header>

    <!-- Hero Section -->
    <section class="hero">
        <div class="hero-content">
            <h2>Real-time Iron Ore Market Intelligence</h2>
            <p>Track 65% Fe lump prices with live data feeds, predictive analytics, and market insights</p>
            
            <div class="stats-grid">
                <div class="stat-card">
                    <div class="stat-value" id="current-price">₹9,300</div>
                    <div class="stat-label">Current Price (Ex-mines)</div>
                    <div class="price-change trend-up">+1.2% <i class="fas fa-arrow-up"></i></div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">₹9,500</div>
                    <div class="stat-label">August Forecast Avg</div>
                    <div class="price-change">± ₹1,300 range</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">22.5%</div>
                    <div class="stat-label">Premium over 62% Fe</div>
                    <div class="price-change trend-up">+3.1% <i class="fas fa-arrow-up"></i></div>
                </div>
                <div class="stat-card">
                    <div class="stat-value">35%</div>
                    <div class="stat-label">Supply Disruption</div>
                    <div class="price-change trend-down">Due to Monsoon</div>
                </div>
            </div>
        </div>
    </section>

    <!-- Dashboard -->
    <section class="dashboard container">
        <div class="section-title">
            <h2><i class="fas fa-tachometer-alt"></i> Market Dashboard</h2>
            <div class="api-status api-active">
                <span class="status-indicator active"></span>
                LIVE: Connected to Market Data API
            </div>
        </div>
        
        <div class="card-grid">
            <!-- Price Card -->
            <div class="card">
                <div class="card-header">Current Spot Price</div>
                <div class="card-body">
                    <div class="price-display" id="spot-price">₹9,300/MT</div>
                    <div class="price-change trend-up">+1.2% today</div>
                    <div class="chart-container">
                        <canvas id="spotChart"></canvas>
                    </div>
                    <div class="api-status api-active">
                        <span class="status-indicator active"></span>
                        Receiving live updates from Platts API
                    </div>
                </div>
            </div>
            
            <!-- Regional Prices -->
            <div class="card">
                <div class="card-header">Regional Price Variations</div>
                <div class="card-body">
                    <div class="chart-container">
                        <canvas id="regionalChart"></canvas>
                    </div>
                    <div class="price-change">
                        Odisha: ₹9,450 | Karnataka: ₹8,950
                    </div>
                    <div class="api-status api-active">
                        <span class="status-indicator active"></span>
                        Synced with SteelMint India regional data
                    </div>
                </div>
            </div>
            
            <!-- Market Forecast -->
            <div class="card">
                <div class="card-header">August 2025 Forecast</div>
                <div class="card-body">
                    <div class="price-display">₹9,200 ± ₹1,300</div>
                    <div class="chart-container">
                        <canvas id="forecastChart"></canvas>
                    </div>
                    <div class="api-status api-active">
                        <span class="status-indicator active"></span>
                        Updated with latest NMDC projections
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Market Feed -->
        <div class="section-title">
            <h2><i class="fas fa-rss"></i> Real-time Market Feed</h2>
            <div class="api-status api-active">
                <span class="status-indicator active"></span>
                Streaming market events
            </div>
        </div>
        
        <div class="market-feed">
            <div class="feed-header">
                <div>Live Market Events & News</div>
                <div><i class="fas fa-sync-alt"></i> Auto-updating</div>
            </div>
            <div class="feed-container" id="market-feed">
                <!-- Feed items will be populated by JavaScript -->
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer>
        <div class="container">
            <div class="footer-grid">
                <div class="footer-col">
                    <h3>OreTrack</h3>
                    <p>Specialized market intelligence for the iron ore industry with real-time data integration and predictive analytics.</p>
                    <div class="social-links">
                        <a href="#" class="social-icon"><i class="fab fa-twitter"></i></a>
                        <a href="#" class="social-icon"><i class="fab fa-linkedin-in"></i></a>
                        <a href="#" class="social-icon"><i class="fab fa-facebook-f"></i></a>
                        <a href="#" class="social-icon"><i class="fab fa-youtube"></i></a>
                    </div>
                </div>
                
                <div class="footer-col">
                    <h3>Data Sources</h3>
                    <ul class="footer-links">
                        <li><a href="#"><i class="fas fa-database"></i> Platts IODEX API</a></li>
                        <li><a href="#"><i class="fas fa-database"></i> SteelMint India</a></li>
                        <li><a href="#"><i class="fas fa-database"></i> NMDC Auction Data</a></li>
                        <li><a href="#"><i class="fas fa-database"></i> Global Iron Ore Index</a></li>
                        <li><a href="#"><i class="fas fa-database"></i> Mining Ministry Reports</a></li>
                    </ul>
                </div>
                
                <div class="footer-col">
                    <h3>Resources</h3>
                    <ul class="footer-links">
                        <li><a href="#"><i class="fas fa-chart-line"></i> Market Analysis</a></li>
                        <li><a href="#"><i class="fas fa-file-pdf"></i> Monthly Reports</a></li>
                        <li><a href="#"><i class="fas fa-calendar-alt"></i> Event Calendar</a></li>
                        <li><a href="#"><i class="fas fa-book"></i> Industry Glossary</a></li>
                        <li><a href="#"><i class="fas fa-calculator"></i> Price Calculators</a></li>
                    </ul>
                </div>
                
                <div class="footer-col">
                    <h3>Contact</h3>
                    <ul class="footer-links">
                        <li><a href="#"><i class="fas fa-envelope"></i> support@oretrack.com</a></li>
                        <li><a href="#"><i class="fas fa-phone"></i> +91 22 1234 5678</a></li>
                        <li><a href="#"><i class="fas fa-map-marker-alt"></i> Mumbai, India</a></li>
                        <li><a href="#"><i class="fas fa-headset"></i> Client Support</a></li>
                        <li><a href="#"><i class="fas fa-comments"></i> API Documentation</a></li>
                    </ul>
                </div>
            </div>
            
            <div class="copyright">
                &copy; 2025 OreTrack Market Intelligence. All rights reserved. Data provided by third-party APIs is subject to their respective terms of use.
            </div>
        </div>
    </footer>

    <script>
        // Simulated API integration for real-time data
        document.addEventListener('DOMContentLoaded', function() {
            // Update timestamp
            function updateTimestamp() {
                const now = new Date();
                const timeStr = now.toLocaleTimeString([], {hour: '2-digit', minute:'2-digit'});
                document.getElementById('update-time').textContent = timeStr;
            }
            
            updateTimestamp();
            setInterval(updateTimestamp, 60000);
            
            // Initialize charts
            const spotCtx = document.getElementById('spotChart').getContext('2d');
            const spotChart = new Chart(spotCtx, {
                type: 'line',
                data: {
                    labels: ['9:00', '10:00', '11:00', '12:00', '13:00', '14:00', '15:00'],
                    datasets: [{
                        label: 'Spot Price (₹/MT)',
                        data: [9250, 9280, 9300, 9320, 9350, 9320, 9300],
                        borderColor: '#3498db',
                        backgroundColor: 'rgba(52, 152, 219, 0.1)',
                        borderWidth: 3,
                        tension: 0.2,
                        fill: true
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: false,
                            grid: {
                                color: 'rgba(0,0,0,0.05)'
                            }
                        },
                        x: {
                            grid: {
                                display: false
                            }
                        }
                    }
                }
            });
            
            const regionalCtx = document.getElementById('regionalChart').getContext('2d');
            const regionalChart = new Chart(regionalCtx, {
                type: 'bar',
                data: {
                    labels: ['Odisha', 'Chhattisgarh', 'Jharkhand', 'Karnataka'],
                    datasets: [{
                        label: 'Price (₹/MT)',
                        data: [9450, 9200, 9100, 8950],
                        backgroundColor: [
                            'rgba(52, 152, 219, 0.7)',
                            'rgba(46, 204, 113, 0.7)',
                            'rgba(155, 89, 182, 0.7)',
                            'rgba(241, 196, 15, 0.7)'
                        ],
                        borderColor: [
                            'rgba(52, 152, 219, 1)',
                            'rgba(46, 204, 113, 1)',
                            'rgba(155, 89, 182, 1)',
                            'rgba(241, 196, 15, 1)'
                        ],
                        borderWidth: 1
                    }]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    plugins: {
                        legend: {
                            display: false
                        }
                    },
                    scales: {
                        y: {
                            beginAtZero: false,
                            grid: {
                                color: 'rgba(0,0,0,0.05)'
                            }
                        }
                    }
                }
            });
            
            const forecastCtx = document.getElementById('forecastChart').getContext('2d');
            const forecastChart = new Chart(forecastCtx, {
                type: 'line',
                data: {
                    labels: ['Jul 15', 'Jul 25', 'Aug 5', 'Aug 15', 'Aug 25', 'Sep 5'],
                    datasets: [
                        {
                            label: 'Actual Price',
                            data: [8900, 9000, 9250, null, null, null],
                            borderColor: '#2ecc71',
                            borderWidth: 3,
                            tension: 0.1,
                            pointRadius: 5
                        },
                        {
                            label: 'Forecast',
                            data: [null, null, null, 9300, 9400, 9350],
                            borderColor: '#f39c12',
                            borderWidth: 3,
                            borderDash: [5, 5],
                            tension: 0.1,
                            pointRadius: 5
                        },
                        {
                            label: 'Upper Range',
                            data: [null, null, null, 9800, 10000, 10200],
                            borderColor: '#e74c3c',
                            borderWidth: 1,
                            tension: 0.1,
                            pointRadius: 0
                        },
                        {
                            label: 'Lower Range',
                            data: [null, null, null, 8800, 8700, 8600],
                            borderColor: '#3498db',
                            borderWidth: 1,
                            tension: 0.1,
                            pointRadius: 0
                        }
                    ]
                },
                options: {
                    responsive: true,
                    maintainAspectRatio: false,
                    scales: {
                        y: {
                            beginAtZero: false,
                            grid: {
                                color: 'rgba(0,0,0,0.05)'
                            }
                        },
                        x: {
                            grid: {
                                display: false
                            }
                        }
                    }
                }
            });
            
            // Market feed data
            const feedData = [
                {
                    type: 'price',
                    title: 'Spot price increased to ₹9,320/MT',
                    content: '65% Fe lump ore price increased by 0.2% in last hour',
                    time: '2 mins ago'
                },
                {
                    type: 'news',
                    title: 'Monsoon disrupts mining in Odisha',
                    content: '12 mines temporarily closed due to heavy rainfall',
                    time: '25 mins ago'
                },
                {
                    type: 'alert',
                    title: 'Export duty maintained at 50%',
                    content: 'Government extends current export policy through 2025',
                    time: '1 hour ago'
                },
                {
                    type: 'price',
                    title: 'NMDC auction premium at 14.5%',
                    content: 'Higher premium indicates strong domestic demand',
                    time: '2 hours ago'
                },
                {
                    type: 'news',
                    title: 'Chinese steel output increases',
                    content: 'July production up 3.2% year-on-year',
                    time: '3 hours ago'
                }
            ];
            
            const feedContainer = document.getElementById('market-feed');
            
            function renderFeedItem(item) {
                const feedItem = document.createElement('div');
                feedItem.className = 'feed-item';
                
                let iconClass = 'news-icon';
                if (item.type === 'price') iconClass = 'price-icon';
                if (item.type === 'alert') iconClass = 'alert-icon';
                
                feedItem.innerHTML = `
                    <div class="feed-icon ${iconClass}">
                        <i class="fas fa-${item.type === 'price' ? 'rupee-sign' : item.type === 'alert' ? 'exclamation-triangle' : 'newspaper'}"></i>
                    </div>
                    <div class="feed-content">
                        <div class="feed-title">${item.title}</div>
                        <div class="feed-desc">${item.content}</div>
                        <div class="feed-time">${item.time}</div>
                    </div>
                `;
                
                return feedItem;
            }
            
            // Render initial feed
            feedData.forEach(item => {
                feedContainer.appendChild(renderFeedItem(item));
            });
            
            // Simulate live updates
            let updateCount = 0;
            setInterval(() => {
                const updateTypes = ['price', 'news', 'alert'];
                const type = updateTypes[Math.floor(Math.random() * 3)];
                
                const updates = [
                    {
                        type: type,
                        title: type === 'price' ? `Minor price adjustment to ₹${9300 + Math.floor(Math.random() * 50)}/MT` : 
                               type === 'news' ? 'New infrastructure projects announced' : 
                               'Railway freight rates revised',
                        content: type === 'price' ? 'Market responding to supply changes' : 
                                type === 'news' ? 'Government plans could boost steel demand' : 
                                'Transportation costs affecting regional prices',
                        time: 'Just now'
                    }
                ];
                
                // Add to top of feed
                feedContainer.insertBefore(renderFeedItem(updates[0]), feedContainer.firstChild);
                
                // Limit feed to 15 items
                if (feedContainer.children.length > 15) {
                    feedContainer.removeChild(feedContainer.lastChild);
                }
                
                // Update count for simulation
                updateCount++;
                
                // Occasionally update price display
                if (updateCount % 5 === 0) {
                    const currentPrice = document.getElementById('current-price');
                    const spotPrice = document.getElementById('spot-price');
                    const newPrice = 9300 + Math.floor(Math.random() * 50) - 25;
                    currentPrice.textContent = `₹${newPrice}`;
                    spotPrice.textContent = `₹${newPrice}/MT`;
                    
                    // Update chart
                    const newData = [...spotChart.data.datasets[0].data];
                    newData.shift();
                    newData.push(newPrice);
                    spotChart.data.datasets[0].data = newData;
                    spotChart.update();
                }
            }, 10000);
        });
    </script>
</body>
</html>
