<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Nisa Chatbot</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" rel="stylesheet">
    <style>
:root {
    --primary-color: #FF0090;
    --secondary-color: #FDB931;
    --background-dark: #1a1a1f;
    --text-light: #ffffff;
    --text-dark: #000000;
    --accent-gradient: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
    --error-color: #ff4444;
    --success-color: #00C851;
}

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
    background-color: var(--background-dark);
    color: var(--text-light);
    line-height: 1.6;
    min-height: 100vh;
    overflow-x: hidden;
}

.header {
    padding: 8px 16px;
    background: rgba(26, 26, 31, 0.95);
    position: fixed;
    width: 100%;
    top: 0;
    left: 0;
    z-index: 30;
    border-bottom: 2px solid var(--primary-color);
    backdrop-filter: blur(10px);
    height: 60px;
}

.header-content {
    max-width: 1400px;
    margin: 0 auto;
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 100%;
}

.logo {
    font-size: 1.8em;
    font-weight: 900;
    background: var(--accent-gradient);
    -webkit-background-clip: text;
    color: transparent;
    letter-spacing: 1.2px;
}

.wallet {
    padding: 10px 20px;
    background: var(--accent-gradient);
    border: none;
    border-radius: 50px;
    color: #fff;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
    font-size: 0.95em;
}

.filter-container {
    position: fixed;
    top: 60px;
    left: 0;
    right: 0;
    padding: 10px 0;
    background: rgba(26, 26, 31, 0.95);
    overflow-x: auto;
    white-space: nowrap;
    scrollbar-width: none;
    -ms-overflow-style: none;
    z-index: 20;
}

.filter-container::-webkit-scrollbar {
    display: none;
}

.filter-buttons {
    display: inline-flex;
    gap: 10px;
    padding: 0 20px;
}

.filter-btn {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    padding: 8px 16px;
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 215, 0, 0.2);
    border-radius: 50px;
    color: var(--text-light);
    cursor: pointer;
    transition: all 0.3s ease;
    font-size: 0.9em;
    white-space: nowrap;
}

.filter-btn:hover {
    background: rgba(255, 215, 0, 0.1);
    border-color: var(--secondary-color);
}

.filter-btn.active {
    background: var(--accent-gradient);
    color: #fffffff6;
    font-weight: 600;
}

.filter-btn i {
    font-size: 16px;
}

.chatbot-container {
    position: fixed;
    top: 120px;
    left: 0;
    right: 0;
    bottom: 60px;
    background: rgba(26, 26, 31, 0.95);
    display: flex;
    flex-direction: column;
}

.chat-header {
    padding: 15px;
    background: linear-gradient(135deg, rgba(255, 215, 0, 0.1), rgba(253, 185, 49, 0.1));
    border-bottom: 1px solid rgba(255, 215, 0, 0.2);
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.chat-status {
    display: flex;
    align-items: center;
    color: #fff;
    font-weight: 600;
}

.status-dot {
    width: 8px;
    height: 8px;
    background: var(--primary-color);
    border-radius: 50%;
    margin-right: 8px;
    animation: pulse 2s infinite;
}

.chat-messages {
    flex: 1;
    overflow-y: auto;
    padding: 20px;
    scroll-behavior: smooth;
}

.message {
    display: flex;
    gap: 10px;
    max-width: 85%;
    margin-bottom: 16px;
    animation: messageSlide 0.3s ease-out;
}

.bot-message {
    align-self: flex-start;
}

.user-message {
    align-self: flex-end;
    flex-direction: row-reverse;
}

.message-avatar {
    width: 36px;
    height: 36px;
    min-width: 36px;
    min-height: 36px;
    background: rgba(255, 215, 0, 0.1);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #ffffff;
    flex-shrink: 0; /* Prevents shrinking */
}

.message {
    display: flex;
    gap: 10px;
    max-width: 90%; /* Increased for better mobile visibility */
    margin-bottom: 16px;
    animation: messageSlide 0.3s ease-out;
    align-items: flex-start; /* Aligns avatar with message top */
}

.message-content {
    background: rgba(255, 255, 255, 0.05);
    padding: 12px 16px;
    border-radius: 16px;
    color: var(--text-light);
}

.user-message .message-content {
    background: rgba(255, 215, 0, 0.1);
}

.chat-input-container {
    padding: 20px;
    background: rgba(26, 26, 31, 0.98);
    border-top: 1px solid rgba(255, 215, 0, 0.1);
    display: flex;
    gap: 12px;
    align-items: center;
}

#chatInput {
    flex: 1;
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid rgba(255, 215, 0, 0.2);
    border-radius: 12px;
    padding: 20px 20px;
    color: var(--text-light);
    font-size: 0.95em;
}

.input-actions {
    display: flex;
    gap: 8px;
}

.input-actions button {
    padding: 20px 24px;
            background: var(--accent-gradient);
            border: none;
            border-radius: 8px;
            color: #fff;
            cursor: pointer;
        }

        .bottom-nav {
    position: fixed;
    bottom: 0;
    left: 0;
    right: 0;
    height: 60px;
    background: rgba(26, 26, 31, 0.98);
    padding: 8px 0;
    border-top: 1px solid rgba(255, 215, 0, 0.2);
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
}

.nav-container {
    display: flex;
    justify-content: space-around;
    align-items: center;
    height: 100%;
    max-width: 600px;
    margin: 0 auto;
}

.nav-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-decoration: none;
    color: #fff;
    transition: all 0.3s ease;
    padding: 5px;
    cursor: pointer;
    position: relative;
}

.nav-item i {
    color: #fff;
    font-size: 24px;
    margin-bottom: 4px;
    transition: color 0.3s ease, transform 0.3s ease;
}

.nav-item span {
    font-size: 12px;
}

.nav-item::after {
    content: '';
    position: absolute;
    bottom: -2px;
    left: 50%;
    width: 0;
    height: 2px;
    background: #ffe1a6;
    transition: width 0.3s ease, left 0.3s ease;
}

.nav-item:hover i {
    color: #ffd000;
    transform: scale(1.2);
}

.nav-item:hover::after {
    width: 100%;
    left: 0;
}

.nav-item.active::after {
    width: 100%;
    left: 0;
}

@keyframes pulse {
    0% { opacity: 1; }
    50% { opacity: 0.5; }
    100% { opacity: 1; }
}

@keyframes messageSlide {
    from { opacity: 0; transform: translateY(10px); }
    to { opacity: 1; transform: translateY(0); }
}

@media (max-width: 768px) {
    .message { max-width: 90%; }
}

/* Hide default headings */
body > h1:first-of-type:not(.heading) {
    display: none !important;
}

.markdown-body h1:first-child {
    display: none !important;
}

.position-relative h1:first-child {
    display: none !important;
}

    </style>
</head>
<body>
    <header class="header">
        <div class="header-content">
            <div class="logo">Nisa</div>
            <button class="wallet">
                <i class="fas fa-wallet"></i>
                Wallet
            </button>
        </div>
    </header>

    <div class="filter-container">
        <div class="filter-buttons">
            <button class="filter-btn active" data-filter="crypto">
                <i class="fab fa-bitcoin"></i>Crypto
            </button>
            <button class="filter-btn" data-filter="nft">
                <i class="fas fa-image"></i>NFT
            </button>
            <button class="filter-btn" data-filter="atm">
                <i class="fas fa-money-check-alt"></i>ATM
            </button>
            <button class="filter-btn" data-filter="metaverse">
                <i class="fas fa-vr-cardboard"></i>Metaverse
            </button>
            <button class="filter-btn" data-filter="defi">
                <i class="fas fa-chart-line"></i>DeFi
            </button>
            <button class="filter-btn" data-filter="web3">
                <i class="fas fa-globe"></i>Web3
            </button>
            <button class="filter-btn" data-filter="more">
                <i class="fas fa-ellipsis-h"></i>More
            </button>
        </div>
    </div>

    <div class="chatbot-container">
        <div class="chat-header">
            <div class="chat-status">
                <span class="status-dot"></span>
                Nisa AI Assistant
            </div>
        </div>

        <div class="chat-messages" id="chatMessages">
            <div class="message bot-message">
                <div class="message-avatar">
                    <i class="fas fa-robot"></i>
                </div>
                <div class="message-content">
                    <p>Hello! I'm your Web3 assistant. Select a category or ask a question!</p>
                </div>
            </div>
        </div>
        
        <div class="chat-input-container">
            <input type="text" id="chatInput" placeholder="Search or ask a question..." />
            <div class="input-actions">
                <button class="send-message" id="sendButton">
                    <i class="fas fa-paper-plane"></i>
                </button>
            </div>
        </div>
    </div>

    <nav class="bottom-nav">
        <div class="nav-container">
            <div class="nav-item" data-page="subscription">
                <a href="https://nysaabhi.github.io/chat">
                    <i class="fas fa-envelope-open-text"></i>
                </a>
                <span>Marketplace</span>
            </div>
            <div class="nav-item" data-page="shopping">
                <a href="https://nysaabhi.github.io/mymom">
                    <i class="fas fa-tshirt"></i>
                </a>
                <span>Merchandise</span>
            </div>
            <div class="nav-item" data-page="rent">
                <a href="booking.html">
                    <i class="fas fa-vr-cardboard"></i>
                </a>
                <span>Metaverse</span>
            </div>
            <div class="nav-item" data-page="location">
                <a href="location.html">
                    <i class="fas fa-map-marker-alt"></i>
                </a>
                <span>Map</span>
            </div>
            <div class="nav-item" data-page="listings">
                <a href="listings.html">
                    <i class="fas fa-tasks"></i>
                </a>
                <span>Listing</span>
            </div>
        </div>
    </nav>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const filterButtons = document.querySelectorAll('.filter-btn');
            const chatMessages = document.getElementById('chatMessages');
            
            filterButtons.forEach(button => {
                button.addEventListener('click', () => {
                    // Remove active class from all buttons
                    filterButtons.forEach(btn => btn.classList.remove('active'));
                    
                    // Add active class to clicked button
                    button.classList.add('active');
                    
                    // Get filter category
                    const filterCategory = button.getAttribute('data-filter');
                                                            
                    // Scroll to the bottom
                    chatMessages.scrollTop = chatMessages.scrollHeight;
                });
            });
        });
    </script>
</body>
</html>
