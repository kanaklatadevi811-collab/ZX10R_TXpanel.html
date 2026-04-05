<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover, user-scalable=no">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="theme-color" content="#0a0e27">
    <title>Color Predictor Pro | Indian Standard Time (IST)</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
            background: linear-gradient(135deg, #0a0e27 0%, #0f1322 100%);
            min-height: 100vh;
            padding: 16px;
            position: relative;
        }

        /* Mobile Container */
        .app-container {
            max-width: 500px;
            width: 100%;
            margin: 0 auto;
        }

        /* Main Card */
        .main-card {
            background: rgba(20, 30, 50, 0.95);
            backdrop-filter: blur(20px);
            border-radius: 48px;
            padding: 24px 20px;
            border: 1px solid rgba(0, 212, 255, 0.2);
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
        }

        /* Header */
        .header {
            text-align: center;
            margin-bottom: 30px;
        }

        .header h1 {
            font-size: 28px;
            font-weight: 700;
            background: linear-gradient(135deg, #00d4ff, #ff6b6b, #c084fc);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            letter-spacing: -0.5px;
            margin-bottom: 8px;
        }

        .subtitle {
            color: #8892b0;
            font-size: 12px;
            font-weight: 500;
        }

        /* Timer Section */
        .timer-section {
            background: rgba(0, 0, 0, 0.4);
            border-radius: 28px;
            padding: 16px;
            margin-bottom: 24px;
            text-align: center;
            border: 1px solid rgba(0, 212, 255, 0.15);
        }

        .world-time {
            font-size: 13px;
            color: #ffd43b;
            margin-bottom: 8px;
            letter-spacing: 0.5px;
            font-weight: 600;
        }

        .countdown-timer {
            font-size: 52px;
            font-weight: 800;
            font-family: 'Courier New', monospace;
            color: #00d4ff;
            text-shadow: 0 0 10px rgba(0, 212, 255, 0.5);
            letter-spacing: 4px;
        }

        .timer-label {
            font-size: 11px;
            color: #8892b0;
            margin-top: 6px;
            text-transform: uppercase;
        }

        /* Prediction Display Area */
        .prediction-area {
            background: rgba(0, 0, 0, 0.4);
            border-radius: 32px;
            padding: 24px 20px;
            margin-bottom: 24px;
            text-align: center;
            transition: all 0.3s ease;
        }

        .color-label {
            font-size: 13px;
            text-transform: uppercase;
            letter-spacing: 2px;
            color: #8892b0;
            margin-bottom: 12px;
        }

        .predicted-color {
            font-size: 44px;
            font-weight: 800;
            padding: 28px 20px;
            border-radius: 28px;
            margin: 12px 0;
            transition: all 0.3s ease;
            text-shadow: 0 2px 10px rgba(0, 0, 0, 0.3);
        }

        /* Color backgrounds */
        .color-red {
            background: linear-gradient(135deg, #ff6b6b, #c92a2a);
            box-shadow: 0 8px 32px rgba(255, 107, 107, 0.3);
            color: white;
        }

        .color-green {
            background: linear-gradient(135deg, #51cf66, #2b8a3e);
            box-shadow: 0 8px 32px rgba(81, 207, 102, 0.3);
            color: white;
        }

        .color-violet {
            background: linear-gradient(135deg, #c084fc, #7c3aed);
            box-shadow: 0 8px 32px rgba(192, 132, 252, 0.3);
            color: white;
        }

        .color-default {
            background: rgba(255, 255, 255, 0.1);
            color: #e0e0e0;
        }

        /* Big/Small Display */
        .big-small-container {
            margin-top: 20px;
            padding-top: 20px;
            border-top: 1px solid rgba(255, 255, 255, 0.1);
        }

        .big-small-label {
            font-size: 13px;
            text-transform: uppercase;
            letter-spacing: 2px;
            color: #8892b0;
            margin-bottom: 10px;
        }

        .big-small-result {
            font-size: 32px;
            font-weight: 800;
            padding: 18px;
            border-radius: 24px;
            transition: all 0.3s ease;
        }

        .result-big {
            background: linear-gradient(135deg, #ffd43b, #f59f00);
            color: #0a0e27;
            box-shadow: 0 8px 32px rgba(255, 212, 59, 0.3);
        }

        .result-small {
            background: linear-gradient(135deg, #4dabf7, #1c7ed6);
            color: white;
            box-shadow: 0 8px 32px rgba(77, 171, 247, 0.3);
        }

        /* Buttons */
        .predict-btn {
            width: 100%;
            background: linear-gradient(135deg, #00d4ff, #7b2f9d);
            border: none;
            padding: 16px 28px;
            border-radius: 60px;
            color: white;
            font-size: 18px;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 10px;
        }

        .predict-btn.disabled {
            opacity: 0.5;
            cursor: not-allowed;
            transform: none;
        }

        .predict-btn.disabled:active {
            transform: none;
        }

        .admin-btn {
            width: 100%;
            background: linear-gradient(135deg, #2d2d44, #1a1a2e);
            border: 1px solid #ffd43b;
            padding: 12px 24px;
            border-radius: 60px;
            color: #ffd43b;
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            display: flex;
            align-items: center;
            justify-content: center;
            gap: 8px;
        }

        .admin-btn:active, .predict-btn:active {
            transform: scale(0.97);
        }

        /* Admin Panel Modal */
        .admin-modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            backdrop-filter: blur(10px);
            z-index: 1000;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .admin-modal.active {
            display: flex;
        }

        .admin-modal-content {
            background: linear-gradient(135deg, #1a1a2e, #0f1322);
            border-radius: 32px;
            padding: 32px 24px;
            max-width: 400px;
            width: 100%;
            border: 2px solid #ffd43b;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5);
        }

        .admin-modal h2 {
            color: #ffd43b;
            text-align: center;
            margin-bottom: 20px;
            font-size: 24px;
        }

        .admin-key-input {
            width: 100%;
            padding: 16px;
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid #ffd43b;
            border-radius: 16px;
            color: white;
            font-size: 18px;
            text-align: center;
            letter-spacing: 2px;
            margin-bottom: 20px;
            outline: none;
        }

        .admin-key-input:focus {
            border-color: #00d4ff;
            box-shadow: 0 0 10px rgba(0, 212, 255, 0.3);
        }

        .admin-verify-btn {
            width: 100%;
            background: linear-gradient(135deg, #ffd43b, #f59f00);
            border: none;
            padding: 14px;
            border-radius: 16px;
            color: #0a0e27;
            font-weight: bold;
            font-size: 16px;
            cursor: pointer;
            margin-bottom: 12px;
        }

        .close-modal-btn {
            width: 100%;
            background: rgba(255, 255, 255, 0.1);
            border: 1px solid rgba(255, 255, 255, 0.2);
            padding: 12px;
            border-radius: 16px;
            color: #8892b0;
            cursor: pointer;
        }

        /* Live Prediction Panel */
        .live-prediction-panel {
            background: rgba(0, 0, 0, 0.6);
            border-radius: 24px;
            padding: 16px;
            margin-top: 16px;
            border: 1px solid rgba(255, 212, 59, 0.3);
            display: none;
        }

        .live-prediction-panel.active {
            display: block;
            animation: slideUp 0.3s ease;
        }

        .live-prediction-title {
            color: #ffd43b;
            font-size: 14px;
            font-weight: bold;
            margin-bottom: 12px;
            text-align: center;
        }

        .live-buttons {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            margin-bottom: 12px;
        }

        .live-color-btn {
            padding: 12px;
            border-radius: 16px;
            font-weight: bold;
            border: none;
            cursor: pointer;
            transition: transform 0.2s;
        }

        .live-color-btn:active {
            transform: scale(0.95);
        }

        .live-bigsmall {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
        }

        .live-bs-btn {
            padding: 12px;
            border-radius: 16px;
            font-weight: bold;
            border: none;
            cursor: pointer;
        }

        /* Stats Section */
        .stats-section {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            margin-top: 20px;
        }

        .stat-card {
            background: rgba(0, 0, 0, 0.3);
            border-radius: 20px;
            padding: 10px;
            text-align: center;
        }

        .stat-value {
            font-size: 22px;
            font-weight: 800;
            color: #00d4ff;
        }

        .stat-label {
            font-size: 10px;
            color: #8892b0;
            margin-top: 4px;
            text-transform: uppercase;
        }

        /* History Section */
        .history-section {
            margin-top: 20px;
            background: rgba(20, 30, 50, 0.6);
            border-radius: 28px;
            padding: 16px;
        }

        .history-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 12px;
            padding: 0 4px;
        }

        .history-title {
            font-size: 13px;
            font-weight: 600;
            color: #00d4ff;
        }

        .clear-btn {
            background: none;
            border: none;
            color: #ff6b6b;
            font-size: 12px;
            cursor: pointer;
            padding: 4px 8px;
        }

        .history-list {
            max-height: 200px;
            overflow-y: auto;
        }

        .history-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            margin-bottom: 6px;
            background: rgba(0, 0, 0, 0.3);
            border-radius: 14px;
        }

        .history-color {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .color-dot {
            width: 20px;
            height: 20px;
            border-radius: 10px;
        }

        .admin-badge {
            background: #ffd43b;
            color: #0a0e27;
            padding: 2px 8px;
            border-radius: 12px;
            font-size: 9px;
            font-weight: bold;
        }

        @keyframes slideUp {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .animate {
            animation: slideUp 0.3s ease-out;
        }

        /* Timezone indicator */
        .timezone-indicator {
            font-size: 10px;
            color: #4ecdc4;
            margin-top: 4px;
        }

        /* Cooldown indicator */
        .cooldown-indicator {
            font-size: 11px;
            color: #ffd43b;
            margin-top: 8px;
            text-align: center;
        }
    </style>
</head>
<body>
    <div class="app-container">
        <div class="main-card">
            <!-- Header -->
            <div class="header">
                <h1>🎨 Color Predictor Pro</h1>
                <div class="subtitle">Indian Standard Time (IST - Kolkata) | One Prediction Per Minute</div>
            </div>

            <!-- Timer Section with Indian Time -->
            <div class="timer-section">
                <div class="world-time" id="indianTime">Loading Indian Time...</div>
                <div class="countdown-timer" id="countdownTimer">01:00</div>
                <div class="timer-label">Next Auto Prediction</div>
                <div class="timezone-indicator">🇮🇳 Indian Standard Time (IST - GMT+5:30) | Kolkata</div>
            </div>

            <!-- Prediction Display Area -->
            <div class="prediction-area" id="predictionArea">
                <div class="color-label">PREDICTED COLOR</div>
                <div class="predicted-color color-default" id="predictedColor">--</div>
                
                <div class="big-small-container">
                    <div class="big-small-label">BIG / SMALL</div>
                    <div class="big-small-result" id="bigSmallResult">--</div>
                </div>
            </div>

            <!-- Predict Button -->
            <button class="predict-btn" id="predictBtn">
                <span>🔮</span>
                <span>PREDICT NEXT</span>
                <span>✨</span>
            </button>
            <div class="cooldown-indicator" id="cooldownIndicator"></div>

            <!-- Admin Panel Button -->
            <button class="admin-btn" id="adminPanelBtn">
                <span>👑</span>
                <span>ADMIN PANEL</span>
                <span>🔐</span>
            </button>

            <!-- Live Prediction Panel (shows after admin login) -->
            <div class="live-prediction-panel" id="livePredictionPanel">
                <div class="live-prediction-title">👑 LIVE PREDICTION OVERRIDE</div>
                <div class="live-buttons">
                    <button class="live-color-btn" style="background: #ff6b6b; color: white;" onclick="setLiveColor('Red')">🔴 RED</button>
                    <button class="live-color-btn" style="background: #51cf66; color: white;" onclick="setLiveColor('Green')">🟢 GREEN</button>
                    <button class="live-color-btn" style="background: #c084fc; color: white;" onclick="setLiveColor('Violet')">🟣 VIOLET</button>
                </div>
                <div class="live-bigsmall">
                    <button class="live-bs-btn" style="background: #ffd43b; color: #0a0e27;" onclick="setLiveBigSmall('Big')">🔴 BIG (5-9)</button>
                    <button class="live-bs-btn" style="background: #4dabf7; color: white;" onclick="setLiveBigSmall('Small')">🔵 SMALL (0-4)</button>
                </div>
                <div style="text-align: center; margin-top: 10px;">
                    <button class="admin-btn" style="background: #ff6b6b; padding: 8px; font-size: 12px;" onclick="submitLivePrediction()">✅ SUBMIT LIVE PREDICTION</button>
                </div>
            </div>

            <!-- Statistics Section -->
            <div class="stats-section">
                <div class="stat-card">
                    <div class="stat-value" id="totalPredictions">0</div>
                    <div class="stat-label">Total</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="bigCount">0</div>
                    <div class="stat-label">Big</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="smallCount">0</div>
                    <div class="stat-label">Small</div>
                </div>
            </div>
        </div>

        <!-- History Section -->
        <div class="history-section">
            <div class="history-header">
                <div class="history-title">📜 Prediction History</div>
                <button class="clear-btn" id="clearHistoryBtn">Clear All</button>
            </div>
            <div class="history-list" id="historyList">
                <div style="text-align: center; color: #8892b0; padding: 20px;">
                    No predictions yet
                </div>
            </div>
        </div>
    </div>

    <!-- Admin Modal -->
    <div class="admin-modal" id="adminModal">
        <div class="admin-modal-content">
            <h2>🔐 ADMIN ACCESS</h2>
            <input type="password" id="adminKeyInput" class="admin-key-input" placeholder="Enter Admin Key" autocomplete="off">
            <button class="admin-verify-btn" onclick="verifyAdminKey()">VERIFY & UNLOCK</button>
            <button class="close-modal-btn" onclick="closeAdminModal()">CANCEL</button>
        </div>
    </div>

    <script>
        // Colors and options
        const colors = ['Red', 'Green', 'Violet'];
        const colorGradients = {
            'Red': 'color-red',
            'Green': 'color-green',
            'Violet': 'color-violet'
        };
        const colorHex = {
            'Red': '#ff6b6b',
            'Green': '#51cf66',
            'Violet': '#c084fc'
        };

        // Data storage
        let predictions = [];
        let stats = {
            total: 0,
            big: 0,
            small: 0,
            colorCounts: { Red: 0, Green: 0, Violet: 0 }
        };

        // Timer variables
        let timeLeft = 60;
        let timerInterval = null;
        let isAdminLoggedIn = false;
        
        // Prediction cooldown
        let canPredict = true;
        let cooldownTimeout = null;
        
        // Live prediction variables
        let liveColor = null;
        let liveBigSmall = null;
        let isLiveModeActive = false;

        // DOM Elements
        const predictedColorEl = document.getElementById('predictedColor');
        const bigSmallResultEl = document.getElementById('bigSmallResult');
        const predictBtn = document.getElementById('predictBtn');
        const adminPanelBtn = document.getElementById('adminPanelBtn');
        const adminModal = document.getElementById('adminModal');
        const livePredictionPanel = document.getElementById('livePredictionPanel');
        const countdownTimerEl = document.getElementById('countdownTimer');
        const indianTimeEl = document.getElementById('indianTime');
        const cooldownIndicator = document.getElementById('cooldownIndicator');

        // Get Indian Time (IST - GMT+5:30)
        function getIndianTime() {
            const now = new Date();
            // Convert to IST (GMT+5:30)
            const istOffset = 5.5 * 60 * 60 * 1000; // 5.5 hours in milliseconds
            const utcTime = now.getTime() + (now.getTimezoneOffset() * 60 * 1000);
            const istTime = new Date(utcTime + istOffset);
            
            return istTime;
        }

        // Format Indian Time
        function formatIndianTime(date) {
            const options = {
                hour: '2-digit',
                minute: '2-digit',
                second: '2-digit',
                day: '2-digit',
                month: '2-digit',
                year: 'numeric',
                hour12: true
            };
            return date.toLocaleString('en-IN', options);
        }

        // Update Indian Time Display
        function updateIndianTime() {
            const istTime = getIndianTime();
            const formattedTime = formatIndianTime(istTime);
            const dayName = istTime.toLocaleString('en-IN', { weekday: 'long' });
            indianTimeEl.innerHTML = `🇮🇳 KOLKATA | ${dayName}, ${formattedTime} IST`;
        }

        // Get remaining seconds to next minute boundary
        function getSecondsToNextMinute() {
            const istTime = getIndianTime();
            const seconds = istTime.getSeconds();
            const milliseconds = istTime.getMilliseconds();
            return 60 - seconds - (milliseconds / 1000);
        }

        // Sync timer with Indian clock
        function syncTimerWithIndianClock() {
            const secondsToNextMinute = getSecondsToNextMinute();
            
            // Set timeLeft based on seconds remaining in current minute
            timeLeft = Math.ceil(secondsToNextMinute);
            
            // Ensure timeLeft is between 1-60
            if (timeLeft <= 0) timeLeft = 60;
            if (timeLeft > 60) timeLeft = 60;
            
            // Update display immediately
            updateTimerDisplay();
            
            // Clear existing interval
            if (timerInterval) clearInterval(timerInterval);
            
            // Start new timer that ticks every second
            timerInterval = setInterval(() => {
                if (timeLeft <= 1) {
                    // Time's up! Auto prediction at minute boundary
                    if (!isLiveModeActive && canPredict) {
                        makePrediction();
                        disablePredictButton();
                    }
                    // Reset to 60 seconds
                    timeLeft = 60;
                } else {
                    timeLeft--;
                }
                
                updateTimerDisplay();
            }, 1000);
        }

        // Update timer display with visual effects
        function updateTimerDisplay() {
            const minutes = Math.floor(timeLeft / 60);
            const seconds = timeLeft % 60;
            countdownTimerEl.textContent = `${minutes.toString().padStart(2, '0')}:${seconds.toString().padStart(2, '0')}`;
            
            // Visual effect for last 10 seconds
            if (timeLeft <= 10) {
                countdownTimerEl.style.color = '#ff6b6b';
                countdownTimerEl.style.textShadow = '0 0 15px rgba(255, 107, 107, 0.5)';
            } else {
                countdownTimerEl.style.color = '#00d4ff';
                countdownTimerEl.style.textShadow = '0 0 10px rgba(0, 212, 255, 0.5)';
            }
        }

        // Load saved data
        function loadData() {
            const savedPredictions = localStorage.getItem('colorPredictionsIST');
            const savedStats = localStorage.getItem('colorStatsIST');
            
            if (savedPredictions) {
                predictions = JSON.parse(savedPredictions);
                renderHistory();
            }
            if (savedStats) {
                stats = JSON.parse(savedStats);
                updateStatsDisplay();
            }
        }

        // Save data
        function saveData() {
            localStorage.setItem('colorPredictionsIST', JSON.stringify(predictions));
            localStorage.setItem('colorStatsIST', JSON.stringify(stats));
        }

        // Update stats display
        function updateStatsDisplay() {
            document.getElementById('totalPredictions').textContent = stats.total;
            document.getElementById('bigCount').textContent = stats.big;
            document.getElementById('smallCount').textContent = stats.small;
        }

        // Generate random prediction
        function generatePrediction() {
            const randomColor = colors[Math.floor(Math.random() * colors.length)];
            const randomBigSmall = Math.random() < 0.5 ? 'Big' : 'Small';
            return { color: randomColor, bigSmall: randomBigSmall };
        }

        // Update display
        function updateDisplay(prediction) {
            predictedColorEl.textContent = prediction.color;
            predictedColorEl.className = `predicted-color ${colorGradients[prediction.color]}`;
            
            bigSmallResultEl.textContent = prediction.bigSmall;
            bigSmallResultEl.className = `big-small-result ${prediction.bigSmall === 'Big' ? 'result-big' : 'result-small'}`;
            
            document.getElementById('predictionArea').classList.add('animate');
            setTimeout(() => {
                document.getElementById('predictionArea').classList.remove('animate');
            }, 300);
        }

        // Add to history with Indian timestamp
        function addToHistory(prediction, isAdmin = false) {
            const istTime = getIndianTime();
            const historyItem = {
                ...prediction,
                timestamp: istTime.toLocaleTimeString('en-IN', { hour12: true }),
                date: istTime.toLocaleDateString('en-IN'),
                istTime: istTime.toISOString(),
                isAdmin: isAdmin
            };
            
            predictions.unshift(historyItem);
            if (predictions.length > 20) predictions.pop();
            renderHistory();
        }

        // Render history
        function renderHistory() {
            if (predictions.length === 0) {
                document.getElementById('historyList').innerHTML = '<div style="text-align: center; color: #8892b0; padding: 20px;">No predictions yet</div>';
                return;
            }
            
            document.getElementById('historyList').innerHTML = predictions.map(pred => `
                <div class="history-item">
                    <div class="history-color">
                        <div class="color-dot" style="background: ${colorHex[pred.color]}"></div>
                        <span style="font-weight: 600;">${pred.color}</span>
                        ${pred.isAdmin ? '<span class="admin-badge">ADMIN</span>' : ''}
                    </div>
                    <div class="history-big-small" style="background: ${pred.bigSmall === 'Big' ? 'rgba(255, 212, 59, 0.2)' : 'rgba(77, 171, 247, 0.2)'}">
                        ${pred.bigSmall}
                    </div>
                    <div class="history-time">${pred.timestamp}</div>
                </div>
            `).join('');
        }

        // Update stats
        function updateStats(prediction) {
            stats.total++;
            if (prediction.bigSmall === 'Big') stats.big++;
            else stats.small++;
            stats.colorCounts[prediction.color]++;
            updateStatsDisplay();
        }

        // Enable predict button
        function enablePredictButton() {
            canPredict = true;
            predictBtn.classList.remove('disabled');
            predictBtn.style.opacity = '1';
            cooldownIndicator.innerHTML = '';
        }

        // Disable predict button with cooldown
        function disablePredictButton() {
            canPredict = false;
            predictBtn.classList.add('disabled');
            predictBtn.style.opacity = '0.5';
            
            // Show cooldown indicator
            cooldownIndicator.innerHTML = '⏳ Please wait until next minute for prediction ⏳';
            
            // Clear existing timeout
            if (cooldownTimeout) clearTimeout(cooldownTimeout);
            
            // Calculate time until next minute boundary
            const secondsToNextMinute = getSecondsToNextMinute();
            const waitTime = Math.ceil(secondsToNextMinute) * 1000;
            
            // Set timeout to enable button at next minute boundary
            cooldownTimeout = setTimeout(() => {
                enablePredictButton();
            }, waitTime);
        }

        // Main prediction function
        function makePrediction(isAdminPrediction = false, adminColor = null, adminBigSmall = null) {
            // Check if prediction is allowed (unless admin override)
            if (!canPredict && !isAdminPrediction) {
                showNotification('❌ Please wait for next minute! Only one prediction per minute!', '#ff6b6b');
                return false;
            }
            
            let prediction;
            
            if (isAdminPrediction && adminColor && adminBigSmall) {
                prediction = { color: adminColor, bigSmall: adminBigSmall };
                addToHistory(prediction, true);
                updateStats(prediction);
                updateDisplay(prediction);
                saveData();
                
                // Show admin notification
                showNotification('👑 Admin Live Prediction Submitted!', '#ffd43b');
                
                // Reset live mode
                isLiveModeActive = false;
                liveColor = null;
                liveBigSmall = null;
            } else {
                prediction = generatePrediction();
                addToHistory(prediction, false);
                updateStats(prediction);
                updateDisplay(prediction);
                saveData();
            }
            
            // Reset timer to remaining seconds in current minute
            timeLeft = Math.ceil(getSecondsToNextMinute());
            updateTimerDisplay();
            
            // Disable predict button (cooldown starts)
            if (!isAdminPrediction) {
                disablePredictButton();
            }
            
            // Haptic feedback
            if (window.navigator && window.navigator.vibrate) {
                window.navigator.vibrate(50);
            }
            
            return true;
        }

        // Show notification
        function showNotification(message, color = '#00d4ff') {
            const notification = document.createElement('div');
            notification.textContent = message;
            notification.style.cssText = `
                position: fixed;
                bottom: 80px;
                left: 50%;
                transform: translateX(-50%);
                background: ${color};
                color: #0a0e27;
                padding: 10px 20px;
                border-radius: 30px;
                font-weight: bold;
                z-index: 1000;
                animation: slideUp 0.3s ease-out;
                font-size: 14px;
            `;
            document.body.appendChild(notification);
            setTimeout(() => notification.remove(), 2000);
        }

        // Admin verification
        function verifyAdminKey() {
            const keyInput = document.getElementById('adminKeyInput');
            const adminKey = keyInput.value;
            
            if (adminKey === 'ZX_BHAIYA_JI') {
                isAdminLoggedIn = true;
                closeAdminModal();
                livePredictionPanel.classList.add('active');
                showNotification('✅ Admin Access Granted! Live prediction mode active', '#51cf66');
                
                // Auto-focus keyboard for mobile
                setTimeout(() => {
                    const firstBtn = document.querySelector('.live-color-btn');
                    if (firstBtn) firstBtn.focus();
                }, 100);
            } else {
                showNotification('❌ Invalid Admin Key! Access Denied', '#ff6b6b');
                keyInput.value = '';
                keyInput.style.borderColor = '#ff6b6b';
                setTimeout(() => {
                    keyInput.style.borderColor = '#ffd43b';
                }, 1000);
            }
        }

        // Set live color
        function setLiveColor(color) {
            liveColor = color;
            showNotification(`Color selected: ${color}`, colorHex[color]);
            
            // Visual feedback
            const btns = document.querySelectorAll('.live-color-btn');
            btns.forEach(btn => btn.style.opacity = '0.6');
            event.target.style.opacity = '1';
        }

        // Set live big/small
        function setLiveBigSmall(value) {
            liveBigSmall = value;
            showNotification(`${value} selected`, value === 'Big' ? '#ffd43b' : '#4dabf7');
            
            const btns = document.querySelectorAll('.live-bs-btn');
            btns.forEach(btn => btn.style.opacity = '0.6');
            event.target.style.opacity = '1';
        }

        // Submit live prediction
        function submitLivePrediction() {
            if (!isAdminLoggedIn) {
                showNotification('Please login as admin first!', '#ff6b6b');
                return;
            }
            
            if (!liveColor || !liveBigSmall) {
                showNotification('Please select both color and Big/Small!', '#ffd43b');
                return;
            }
            
            // Admin prediction bypasses cooldown
            makePrediction(true, liveColor, liveBigSmall);
            isLiveModeActive = false;
            
            // Reset selection
            liveColor = null;
            liveBigSmall = null;
        }

        // Admin modal functions
        function openAdminModal() {
            adminModal.classList.add('active');
            document.getElementById('adminKeyInput').focus();
            
            // Auto open keyboard on mobile
            if (window.innerWidth <= 768) {
                document.getElementById('adminKeyInput').click();
            }
        }
        
        function closeAdminModal() {
            adminModal.classList.remove('active');
            document.getElementById('adminKeyInput').value = '';
        }
        
        function clearHistory() {
            if (confirm('Clear all prediction history?')) {
                predictions = [];
                stats = { total: 0, big: 0, small: 0, colorCounts: { Red: 0, Green: 0, Violet: 0 } };
                renderHistory();
                updateStatsDisplay();
                saveData();
                showNotification('History cleared!', '#8892b0');
            }
        }

        // Event listeners
        predictBtn.addEventListener('click', () => {
            if (!canPredict) {
                showNotification('❌ Please wait for next minute! Only one prediction per minute!', '#ff6b6b');
                return;
            }
            
            if (!isLiveModeActive) {
                makePrediction(false);
            } else {
                showNotification('Live mode active! Use admin panel to submit', '#ffd43b');
            }
        });
        
        adminPanelBtn.addEventListener('click', openAdminModal);
        document.getElementById('clearHistoryBtn').addEventListener('click', clearHistory);
        
        // Close modal on escape
        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape' && adminModal.classList.contains('active')) {
                closeAdminModal();
            }
            if (e.key === 'Enter' && adminModal.classList.contains('active')) {
                verifyAdminKey();
            }
        });

        // Initialize
        function init() {
            loadData();
            syncTimerWithIndianClock();
            updateIndianTime();
            setInterval(updateIndianTime, 1000);
            enablePredictButton();
        }
        
        init();
    </script>
</body>
</html>
