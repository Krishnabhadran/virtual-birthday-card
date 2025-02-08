<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🎉 Ultimate Virtual Birthday Card Generator 🎂</title>
    <link href="https://fonts.googleapis.com/css2?family=Pacifico&family=Poppins:wght@300;500;700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        /* Advanced CSS with Theme Switching */
        :root {
            --primary: #ff3366;
            --secondary: #ff99cc;
            --accent: #ff6b6b;
            --bg-gradient: linear-gradient(135deg, #ff99cc 0%, #ff66b2 100%);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            transition: all 0.3s ease;
        }

        body {
            font-family: 'Poppins', sans-serif;
            background: var(--bg-gradient);
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }

        /* Professional Container Design */
        .container {
            max-width: 600px;
            margin: 2rem auto;
            background: rgba(255, 255, 255, 0.95);
            padding: 2rem;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
            backdrop-filter: blur(10px);
            position: relative;
            z-index: 10;
        }

        /* Animated Header */
        .header {
            text-align: center;
            margin-bottom: 2rem;
            position: relative;
        }

        .header h1 {
            font-family: 'Pacifico', cursive;
            color: var(--primary);
            font-size: 2.5rem;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
            animation: float 3s ease-in-out infinite;
        }

        /* Enhanced Form Elements */
        .form-group {
            margin: 1.5rem 0;
        }

        input, textarea, select {
            width: 100%;
            padding: 1rem;
            border: 2px solid #eee;
            border-radius: 10px;
            font-size: 1rem;
            margin: 0.5rem 0;
        }

        input:focus, textarea:focus, select:focus {
            border-color: var(--primary);
            box-shadow: 0 0 8px rgba(255, 51, 102, 0.2);
        }

        /* Premium Button Styles */
        .btn {
            background: var(--primary);
            color: white;
            padding: 1rem 2rem;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 1px;
            position: relative;
            overflow: hidden;
        }

        .btn:after {
            content: '';
            position: absolute;
            top: -50%;
            right: -50%;
            bottom: -50%;
            left: -50%;
            background: linear-gradient(45deg, transparent, rgba(255,255,255,0.3), transparent);
            transform: rotateZ(60deg) translate(-5em, 7.5em);
        }

        .btn:hover:after {
            animation: sheen 1.5s forwards;
        }

        /* Advanced Card Design */
        .card {
            display: none;
            position: relative;
            text-align: center;
        }

        .animated-text {
            font-size: 2.5rem;
            margin: 1rem 0;
            animation: textPop 1s infinite alternate;
        }

        /* Professional Share Options */
        .share-panel {
            display: flex;
            gap: 1rem;
            justify-content: center;
            margin: 2rem 0;
        }

        .share-btn {
            padding: 0.8rem 1.5rem;
            border-radius: 30px;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }

        /* Enhanced Animations */
        @keyframes float {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-10px); }
        }

        @keyframes sheen {
            100% { transform: rotateZ(60deg) translate(1em, -9em); }
        }

        /* Particle Effects */
        .particle {
            position: absolute;
            pointer-events: none;
            animation: float 3s infinite;
        }

        /* Music Player Controls */
        .music-controls {
            position: fixed;
            bottom: 20px;
            right: 20px;
            z-index: 100;
        }

        /* Mobile Optimization */
        @media (max-width: 768px) {
            .container {
                margin: 1rem;
                padding: 1rem;
            }
            
            .animated-text {
                font-size: 1.8rem;
            }
        }
    </style>
</head>
<body>
    <!-- Loading Screen -->
    <div class="loader">
        <div class="spinner"></div>
    </div>

    <div class="container" id="formContainer">
        <!-- Advanced Form -->
        <div class="header">
            <h1>🎂 Create Magic Birthday Card ✨</h1>
        </div>
        
        <div class="form-group">
            <input type="text" id="name" placeholder="Recipient's Name" class="input-field">
        </div>
        
        <div class="form-group">
            <select id="quoteType" class="styled-select">
                <option value="funny">😂 Funny Quote</option>
                <option value="inspirational">💪 Inspirational Quote</option>
                <option value="custom">✏️ Custom Message</option>
            </select>
        </div>

        <div class="form-group">
            <textarea id="message" placeholder="Your Personal Message" rows="4"></textarea>
        </div>

        <div class="form-group">
            <input type="file" id="photo" accept="image/*" class="upload-btn">
        </div>

        <button class="btn" onclick="generateCard()">Create Magic Card ✨</button>
    </div>

    <!-- Generated Card -->
    <div class="container card" id="birthdayCard">
        <div class="header">
            <h1 class="animated-text" contenteditable="true">🎉 Happy Birthday! 🎂</h1>
        </div>
        
        <div class="photo-frame">
            <img id="uploadedPhoto" src="" alt="Birthday Photo">
        </div>

        <div class="editable-message" contenteditable="true">
            Your personalized message appears here...
        </div>

        <!-- Share Panel -->
        <div class="share-panel">
            <button class="btn share-btn" onclick="copyLink()">
                <i class="fas fa-link"></i> Copy Link
            </button>
            <button class="btn share-btn" onclick="shareEmail()">
                <i class="fas fa-envelope"></i> Email
            </button>
            <button class="btn share-btn" onclick="shareSMS()">
                <i class="fas fa-sms"></i> SMS
            </button>
        </div>
    </div>

    <!-- Music Controls -->
    <div class="music-controls">
        <audio id="birthdayAudio" controls>
            <source src="birthday.mp3" type="audio/mpeg">
        </audio>
    </div>

    <!-- Confetti Library -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.4.0/dist/confetti.browser.min.js"></script>

    <script>
        // Advanced Configuration
        const quotes = {
            funny: [
                "🎉 Aging like fine wine!",
                "🍰 Calories don't count today!",
                "🎈 You're not old, you're vintage!"
            ],
            inspirational: [
                "✨ The best is yet to come!",
                "🌟 Make your year amazing!",
                "🚀 Reach for the stars!"
            ]
        };

        // Professional Functions
        function generateCard() {
            // Validation
            const name = document.getElementById('name').value.trim();
            if (!name) {
                showError('Please enter a name!');
                return;
            }

            // Generate particles
            createParticles(50);

            // Show card
            document.getElementById('formContainer').style.display = 'none';
            document.getElementById('birthdayCard').style.display = 'block';

            // Play music
            document.getElementById('birthdayAudio').play();

            // Trigger confetti
            confetti({
                particleCount: 100,
                spread: 70,
                origin: { y: 0.6 }
            });
        }

        // Share Functions
        function copyLink() {
            navigator.clipboard.writeText(window.location.href)
                .then(() => showToast('Link copied! 🎉'))
                .catch(err => showError('Failed to copy link'));
        }

        function shareEmail() {
            window.location.href = `mailto:?subject=Birthday Card&body=Check out this card: ${window.location.href}`;
        }

        function shareSMS() {
            window.location.href = `sms:?body=Check out this birthday card: ${window.location.href}`;
        }

        // Utility Functions
        function createParticles(count) {
            // Particle creation logic
        }

        function showToast(message) {
            // Toast notification implementation
        }

        // Initialize
        document.addEventListener('DOMContentLoaded', () => {
            // Initialization code
        });
    </script>
</body>
</html>
