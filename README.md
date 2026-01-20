<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>junz413 | Bomberman-Style GitHub Profile</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: #0d1117;
            color: #c9d1d9;
            min-height: 100vh;
            overflow-x: hidden;
            position: relative;
        }
        
        /* Bomberman Game Grid Background */
        .grid-background {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-image: 
                linear-gradient(rgba(13, 17, 23, 0.9), rgba(13, 17, 23, 0.9)),
                repeating-linear-gradient(0deg, transparent, transparent 19px, rgba(33, 133, 208, 0.05) 19px, rgba(33, 133, 208, 0.05) 20px),
                repeating-linear-gradient(90deg, transparent, transparent 19px, rgba(33, 133, 208, 0.05) 19px, rgba(33, 133, 208, 0.05) 20px);
            z-index: -2;
        }
        
        /* Pixelated Bomberman Characters */
        .bomberman {
            position: fixed;
            width: 40px;
            height: 40px;
            z-index: -1;
            image-rendering: pixelated;
            opacity: 0.7;
        }
        
        .bomberman-1 {
            top: 10%;
            left: 5%;
            animation: float 20s infinite linear;
        }
        
        .bomberman-2 {
            top: 70%;
            right: 10%;
            animation: float 25s infinite linear reverse;
        }
        
        /* Explosions */
        .explosion {
            position: fixed;
            width: 60px;
            height: 60px;
            background: radial-gradient(circle, rgba(255,100,100,0.7) 0%, rgba(255,50,50,0) 70%);
            border-radius: 50%;
            z-index: -1;
            opacity: 0;
        }
        
        .explosion-1 {
            top: 20%;
            right: 15%;
            animation: explode 8s infinite;
        }
        
        .explosion-2 {
            top: 60%;
            left: 20%;
            animation: explode 10s infinite 2s;
        }
        
        .explosion-3 {
            top: 85%;
            right: 30%;
            animation: explode 12s infinite 4s;
        }
        
        /* Main container */
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
            position: relative;
            z-index: 1;
        }
        
        /* Header Section */
        .header {
            display: flex;
            flex-wrap: wrap;
            align-items: center;
            justify-content: space-between;
            margin-bottom: 40px;
            padding: 20px;
            background: rgba(22, 27, 34, 0.8);
            border-radius: 15px;
            border: 2px solid #30363d;
            box-shadow: 0 0 20px rgba(33, 133, 208, 0.3);
            animation: pulse 4s infinite;
        }
        
        .profile {
            display: flex;
            align-items: center;
            gap: 20px;
        }
        
        .avatar {
            width: 120px;
            height: 120px;
            border-radius: 50%;
            border: 4px solid #238636;
            padding: 5px;
            background: #0d1117;
            box-shadow: 0 0 15px rgba(35, 134, 54, 0.5);
            animation: rotate 20s linear infinite;
        }
        
        .profile-info h1 {
            font-size: 2.5rem;
            color: #58a6ff;
            margin-bottom: 5px;
            text-shadow: 0 0 10px rgba(88, 166, 255, 0.5);
        }
        
        .profile-info p {
            font-size: 1.2rem;
            color: #8b949e;
            margin-bottom: 10px;
        }
        
        /* Badges */
        .badges {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 10px;
        }
        
        .badge {
            padding: 5px 12px;
            background: #238636;
            border-radius: 20px;
            font-size: 0.9rem;
            font-weight: bold;
            color: white;
        }
        
        .badge.learning {
            background: linear-gradient(45deg, #6f42c1, #d73a49);
        }
        
        .badge.collab {
            background: linear-gradient(45deg, #005cc5, #28a745);
        }
        
        /* Sections */
        .section {
            background: rgba(22, 27, 34, 0.8);
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 30px;
            border: 2px solid #30363d;
            box-shadow: 0 0 15px rgba(33, 133, 208, 0.2);
            transition: transform 0.3s, box-shadow 0.3s;
        }
        
        .section:hover {
            transform: translateY(-5px);
            box-shadow: 0 5px 25px rgba(33, 133, 208, 0.4);
        }
        
        .section-title {
            color: #58a6ff;
            font-size: 1.8rem;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 2px solid #30363d;
            display: flex;
            align-items: center;
            gap: 10px;
        }
        
        .section-title i {
            color: #f78166;
        }
        
        /* Inventory Book System Section */
        .inventory-system {
            background: rgba(13, 17, 23, 0.9);
            border: 3px solid #238636;
            box-shadow: 0 0 25px rgba(35, 134, 54, 0.4);
        }
        
        .inventory-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        
        .inventory-status {
            padding: 8px 15px;
            background: #238636;
            border-radius: 5px;
            font-weight: bold;
            color: white;
            animation: blink 2s infinite;
        }
        
        .books-container {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .book {
            background: rgba(33, 38, 45, 0.9);
            border-radius: 10px;
            padding: 15px;
            border-left: 5px solid #f78166;
            transition: all 0.3s;
            cursor: pointer;
        }
        
        .book:hover {
            transform: scale(1.05);
            border-left-color: #58a6ff;
            box-shadow: 0 5px 15px rgba(88, 166, 255, 0.3);
        }
        
        .book-title {
            font-weight: bold;
            color: #58a6ff;
            margin-bottom: 5px;
        }
        
        .book-status {
            font-size: 0.9rem;
            color: #8b949e;
            display: flex;
            align-items: center;
            gap: 5px;
        }
        
        .status-dot {
            width: 10px;
            height: 10px;
            border-radius: 50%;
            display: inline-block;
        }
        
        .completed {
            background-color: #238636;
        }
        
        .in-progress {
            background-color: #d29922;
            animation: pulse 1.5s infinite;
        }
        
        .planned {
            background-color: #8b949e;
        }
        
        /* Languages & Tools */
        .tools-container {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 15px;
        }
        
        .tool {
            padding: 10px 20px;
            background: rgba(33, 38, 45, 0.9);
            border-radius: 8px;
            display: flex;
            align-items: center;
            gap: 10px;
            transition: all 0.3s;
            border: 1px solid #30363d;
        }
        
        .tool:hover {
            background: rgba(56, 139, 253, 0.1);
            border-color: #58a6ff;
            transform: translateY(-3px);
        }
        
        .tool-icon {
            font-size: 1.5rem;
        }
        
        /* Stats Section */
        .stats-container {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        
        .stat-box {
            background: rgba(33, 38, 45, 0.9);
            border-radius: 10px;
            padding: 20px;
            text-align: center;
            border-top: 4px solid #58a6ff;
        }
        
        .stat-number {
            font-size: 2.5rem;
            font-weight: bold;
            color: #58a6ff;
            margin: 10px 0;
        }
        
        /* Contact Links */
        .contact-links {
            display: flex;
            flex-wrap: wrap;
            gap: 15px;
            margin-top: 20px;
        }
        
        .contact-link {
            padding: 10px 20px;
            background: rgba(33, 38, 45, 0.9);
            border-radius: 8px;
            display: flex;
            align-items: center;
            gap: 10px;
            text-decoration: none;
            color: #c9d1d9;
            transition: all 0.3s;
            border: 1px solid #30363d;
        }
        
        .contact-link:hover {
            background: rgba(56, 139, 253, 0.1);
            color: #58a6ff;
            transform: translateY(-3px);
            border-color: #58a6ff;
        }
        
        .contact-link.instagram {
            border-color: #e1306c;
        }
        
        .contact-link.instagram:hover {
            background: rgba(225, 48, 108, 0.1);
            color: #e1306c;
        }
        
        /* Footer */
        .footer {
            text-align: center;
            margin-top: 40px;
            padding: 20px;
            color: #8b949e;
            border-top: 1px solid #30363d;
            font-size: 0.9rem;
        }
        
        /* Animations */
        @keyframes float {
            0% { transform: translateY(0) translateX(0); }
            25% { transform: translateY(-20px) translateX(20px); }
            50% { transform: translateY(0) translateX(40px); }
            75% { transform: translateY(20px) translateX(20px); }
            100% { transform: translateY(0) translateX(0); }
        }
        
        @keyframes explode {
            0% { opacity: 0; transform: scale(0.1); }
            10% { opacity: 1; transform: scale(1); }
            20% { opacity: 0; transform: scale(1.5); }
            100% { opacity: 0; transform: scale(1.5); }
        }
        
        @keyframes pulse {
            0% { box-shadow: 0 0 20px rgba(33, 133, 208, 0.3); }
            50% { box-shadow: 0 0 30px rgba(33, 133, 208, 0.6); }
            100% { box-shadow: 0 0 20px rgba(33, 133, 208, 0.3); }
        }
        
        @keyframes blink {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }
        
        @keyframes rotate {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        /* Responsive Design */
        @media (max-width: 768px) {
            .header {
                flex-direction: column;
                text-align: center;
                gap: 20px;
            }
            
            .profile {
                flex-direction: column;
            }
            
            .avatar {
                width: 100px;
                height: 100px;
            }
            
            .profile-info h1 {
                font-size: 2rem;
            }
            
            .books-container {
                grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
            }
        }
    </style>
</head>
<body>
    <!-- Bomberman Game Background -->
    <div class="grid-background"></div>
    
    <!-- Bomberman Characters -->
    <div class="bomberman bomberman-1">💣</div>
    <div class="bomberman bomberman-2">👤</div>
    
    <!-- Explosions -->
    <div class="explosion explosion-1"></div>
    <div class="explosion explosion-2"></div>
    <div class="explosion explosion-3"></div>
    
    <!-- Main Content -->
    <div class="container">
        <!-- Header Section -->
        <header class="header">
            <div class="profile">
                <div class="avatar">👤</div>
                <div class="profile-info">
                    <h1>👋 Hi, I'm @junz413</h1>
                    <p>Programming & Building Cool Things</p>
                    <div class="badges">
                        <div class="badge learning">Currently Learning</div>
                        <div class="badge collab">Open to Collaborate</div>
                    </div>
                </div>
            </div>
            <div class="fun-fact">
                <h3>⚡ Fun Fact</h3>
                <p>I love eating 🍔🍕 & playing retro games!</p>
            </div>
        </header>
        
        <!-- Inventory Book System Section -->
        <section class="section inventory-system">
            <div class="inventory-header">
                <h2 class="section-title"><i class="fas fa-book"></i> 📚 Inventory Book System</h2>
                <div class="inventory-status">In Development</div>
            </div>
            <p>Currently building an inventory management system for books with the following features:</p>
            
            <div class="books-container">
                <div class="book">
                    <div class="book-title">Database Design</div>
                    <div class="book-status">
                        <span class="status-dot completed"></span> Completed
                    </div>
                    <p>MySQL schema for book inventory</p>
                </div>
                
                <div class="book">
                    <div class="book-title">User Interface</div>
                    <div class="book-status">
                        <span class="status-dot in-progress"></span> In Progress
                    </div>
                    <p>React frontend for management</p>
                </div>
                
                <div class="book">
                    <div class="book-title">Backend API</div>
                    <div class="book-status">
                        <span class="status-dot in-progress"></span> In Progress
                    </div>
                    <p>Python Flask REST API</p>
                </div>
                
                <div class="book">
                    <div class="book-title">Reporting System</div>
                    <div class="book-status">
                        <span class="status-dot planned"></span> Planned
                    </div>
                    <p>Generate inventory reports</p>
                </div>
            </div>
        </section>
        
        <!-- About Section -->
        <section class="section">
            <h2 class="section-title"><i class="fas fa-user"></i> About Me</h2>
            <p><strong>🌱 Currently learning:</strong> Basic programming fundamentals & advanced concepts</p>
            <p><strong>💞️ Looking to collaborate on:</strong> Programs in <em>any</em> language - from Python to JavaScript to Go!</p>
            <p><strong>🎯 Focus:</strong> Building practical applications and improving problem-solving skills</p>
        </section>
        
        <!-- Languages & Tools -->
        <section class="section">
            <h2 class="section-title"><i class="fas fa-tools"></i> Languages & Tools</h2>
            <div class="tools-container">
                <div class="tool">
                    <span class="tool-icon">🐍</span>
                    <span>Python</span>
                </div>
                <div class="tool">
                    <span class="tool-icon"><i class="fab fa-html5"></i></span>
                    <span>HTML5</span>
                </div>
                <div class="tool">
                    <span class="tool-icon"><i class="fab fa-css3-alt"></i></span>
                    <span>CSS3</span>
                </div>
                <div class="tool">
                    <span class="tool-icon"><i class="fab fa-js"></i></span>
                    <span>JavaScript</span>
                </div>
                <div class="tool">
                    <span class="tool-icon"><i class="fab fa-git-alt"></i></span>
                    <span>Git</span>
                </div>
                <div class="tool">
                    <span class="tool-icon"><i class="fas fa-database"></i></span>
                    <span>MySQL</span>
                </div>
            </div>
        </section>
        
        <!-- GitHub Stats -->
        <section class="section">
            <h2 class="section-title"><i class="fas fa-chart-bar"></i> GitHub Stats</h2>
            <div class="stats-container">
                <div class="stat-box">
                    <h3>Repositories</h3>
                    <div class="stat-number">12</div>
                    <p>Public projects</p>
                </div>
                <div class="stat-box">
                    <h3>Contributions</h3>
                    <div class="stat-number">156</div>
                    <p>Last year</p>
                </div>
                <div class="stat-box">
                    <h3>Streak</h3>
                    <div class="stat-number">7</div>
                    <p>Current days</p>
                </div>
            </div>
        </section>
        
        <!-- Goals Section -->
        <section class="section">
            <h2 class="section-title"><i class="fas fa-flag"></i> Goals</h2>
            <ul style="padding-left: 20px; line-height: 1.8;">
                <li>Improve problem-solving skills</li>
                <li>Build real-world projects (like the Inventory Book System)</li>
                <li>Collaborate with other developers</li>
                <li>Learn multiple programming languages</li>
                <li>Contribute to open-source projects</li>
            </ul>
        </section>
        
        <!-- Contact Section -->
        <section class="section">
            <h2 class="section-title"><i class="fas fa-envelope"></i> Contact Me</h2>
            <p>Feel free to reach out for collaboration, questions, or just to chat about programming!</p>
            <div class="contact-links">
                <a href="https://instagram.com/richard_junz" class="contact-link instagram" target="_blank">
                    <i class="fab fa-instagram"></i> Instagram: @richard_junz
                </a>
                <a href="https://github.com/junz413" class="contact-link" target="_blank">
                    <i class="fab fa-github"></i> GitHub: junz413
                </a>
                <div class="contact-link">
                    <i class="fas fa-code"></i> Open to collaborate on any project!
                </div>
            </div>
        </section>
        
        <!-- Footer -->
        <footer class="footer">
            <p>⭐ Feel free to check out my repositories and collaborate with me!</p>
            <p>Made with 💻 and retro game vibes | Inspired by Bomberman</p>
        </footer>
    </div>

    <script>
        // Create more bomberman characters dynamically
        document.addEventListener('DOMContentLoaded', function() {
            const bombermanChars = ['💣', '👤', '🔥', '💥', '🎮'];
            const body = document.body;
            
            // Add more bomberman characters
            for (let i = 0; i < 5; i++) {
                const bomberman = document.createElement('div');
                bomberman.className = `bomberman bomberman-${i+3}`;
                bomberman.textContent = bombermanChars[Math.floor(Math.random() * bombermanChars.length)];
                bomberman.style.top = `${Math.random() * 80 + 10}%`;
                bomberman.style.left = `${Math.random() * 80 + 10}%`;
                bomberman.style.animationDuration = `${Math.random() * 15 + 10}s`;
                bomberman.style.animationDelay = `${Math.random() * 5}s`;
                body.appendChild(bomberman);
            }
            
            // Add more explosions
            for (let i = 0; i < 3; i++) {
                const explosion = document.createElement('div');
                explosion.className = `explosion explosion-${i+4}`;
                explosion.style.top = `${Math.random() * 80 + 10}%`;
                explosion.style.left = `${Math.random() * 80 + 10}%`;
                explosion.style.animationDuration = `${Math.random() * 10 + 8}s`;
                explosion.style.animationDelay = `${Math.random() * 6}s`;
                body.appendChild(explosion);
            }
            
            // Book click animation
            const books = document.querySelectorAll('.book');
            books.forEach(book => {
                book.addEventListener('click', function() {
                    this.style.transform = 'scale(0.95)';
                    setTimeout(() => {
                        this.style.transform = 'scale(1.05)';
                    }, 150);
                });
            });
            
            // Add typing effect to the status
            const status = document.querySelector('.inventory-status');
            const originalText = status.textContent;
            const texts = ['In Development', 'Coding...', 'Building...', 'Designing...'];
            let textIndex = 0;
            let charIndex = 0;
            let isDeleting = false;
            let typeSpeed = 100;
            
            function typeEffect() {
                const currentText = texts[textIndex];
                
                if (isDeleting) {
                    status.textContent = currentText.substring(0, charIndex - 1);
                    charIndex--;
                    typeSpeed = 50;
                } else {
                    status.textContent = currentText.substring(0, charIndex + 1);
                    charIndex++;
                    typeSpeed = 100;
                }
                
                if (!isDeleting && charIndex === currentText.length) {
                    isDeleting = true;
                    typeSpeed = 1000; // pause at end
                } else if (isDeleting && charIndex === 0) {
                    isDeleting = false;
                    textIndex = (textIndex + 1) % texts.length;
                    typeSpeed = 500; // pause before starting new word
                }
                
                setTimeout(typeEffect, typeSpeed);
            }
            
            // Start typing effect after a delay
            setTimeout(typeEffect, 1000);
        });
    </script>
</body>
</html>
