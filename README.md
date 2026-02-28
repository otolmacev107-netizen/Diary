<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Whisper Protocol</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            background-color: #f5f5f5;
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            color: #222;
            min-height: 100vh;
            transition: background-color 1.5s ease, color 1.5s ease;
            line-height: 1.6;
        }

        body.darkened {
            background-color: #0a0a0a;
            color: #e0e0e0;
        }

        .container {
            max-width: 800px;
            margin: 0 auto;
            padding: 40px 20px;
            position: relative;
            z-index: 2;
        }

        /* Initial innocent design */
        .header {
            text-align: center;
            margin-bottom: 40px;
            opacity: 0;
            animation: fadeIn 1.5s ease forwards;
        }

        @keyframes fadeIn {
            to { opacity: 1; }
        }

        .site-title {
            font-size: 32px;
            font-weight: 400;
            letter-spacing: -0.5px;
            color: #333;
            margin-bottom: 8px;
        }

        .site-subtitle {
            font-size: 14px;
            color: #777;
            font-weight: 300;
        }

        /* Innocent blog post */
        .blog-post {
            background: white;
            border-radius: 24px;
            padding: 30px;
            margin-bottom: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.03);
            border: 1px solid rgba(0,0,0,0.05);
            transition: all 0.5s ease;
        }

        body.darkened .blog-post {
            background: #111;
            border-color: #2a2a2a;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }

        .post-title {
            font-size: 24px;
            margin-bottom: 15px;
            font-weight: 400;
        }

        .post-meta {
            font-size: 12px;
            color: #999;
            margin-bottom: 20px;
            display: flex;
            gap: 15px;
        }

        .post-content p {
            margin-bottom: 20px;
            color: #555;
        }

        body.darkened .post-content p {
            color: #aaa;
        }

        /* Permissions panel — looks like a normal "settings" section */
        .permissions-panel {
            background: #f0f0f0;
            border-radius: 20px;
            padding: 25px;
            margin-bottom: 30px;
            border: 1px solid #ddd;
        }

        body.darkened .permissions-panel {
            background: #1a1a1a;
            border-color: #333;
        }

        .panel-title {
            font-size: 18px;
            margin-bottom: 20px;
            font-weight: 500;
        }

        .permission-item {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: 12px 0;
            border-bottom: 1px solid #ddd;
        }

        body.darkened .permission-item {
            border-bottom-color: #333;
        }

        .permission-info {
            flex: 1;
        }

        .permission-name {
            font-weight: 500;
            margin-bottom: 4px;
        }

        .permission-desc {
            font-size: 12px;
            color: #777;
        }

        .permission-button {
            padding: 8px 16px;
            background: #007aff;
            color: white;
            border: none;
            border-radius: 30px;
            font-size: 14px;
            cursor: pointer;
            transition: all 0.2s;
            min-width: 80px;
            text-align: center;
        }

        .permission-button.granted {
            background: #34c759;
            cursor: default;
        }

        .permission-button.denied {
            background: #ff3b30;
        }

        /* Chat section — hidden initially */
        .chat-section {
            margin-top: 40px;
            border-top: 1px solid #eee;
            padding-top: 40px;
            transition: opacity 1s ease;
        }

        body.darkened .chat-section {
            border-top-color: #2a2a2a;
        }

        .chat-container {
            background: white;
            border-radius: 24px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0,0,0,0.05);
            border: 1px solid #eee;
        }

        body.darkened .chat-container {
            background: #111;
            border-color: #2a2a2a;
        }

        .chat-header {
            padding: 20px;
            background: #fafafa;
            border-bottom: 1px solid #eee;
            display: flex;
            align-items: center;
        }

        body.darkened .chat-header {
            background: #1a1a1a;
            border-bottom-color: #333;
        }

        .chat-avatar {
            width: 40px;
            height: 40px;
            background: #e0e0e0;
            border-radius: 50%;
            margin-right: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 18px;
        }

        body.darkened .chat-avatar {
            background: #2a2a2a;
            color: #8b0000;
        }

        .chat-info h3 {
            font-size: 16px;
            font-weight: 500;
            margin-bottom: 4px;
        }

        .chat-info p {
            font-size: 12px;
            color: #888;
        }

        .chat-messages {
            height: 350px;
            overflow-y: auto;
            padding: 20px;
            background: #fff;
        }

        body.darkened .chat-messages {
            background: #111;
        }

        .message {
            margin-bottom: 20px;
            display: flex;
            flex-direction: column;
        }

        .message.user {
            align-items: flex-end;
        }

        .message.bot {
            align-items: flex-start;
        }

        .message-content {
            max-width: 80%;
            padding: 12px 16px;
            border-radius: 18px;
            font-size: 14px;
            background: #f0f0f0;
            color: #333;
        }

        body.darkened .message-content {
            background: #1a1a1a;
            color: #ddd;
        }

        .user .message-content {
            background: #007aff;
            color: white;
            border-bottom-right-radius: 4px;
        }

        .bot .message-content {
            background: #f0f0f0;
            border-bottom-left-radius: 4px;
        }

        body.darkened .bot .message-content {
            background: #1a1a1a;
        }

        .message-time {
            font-size: 10px;
            color: #999;
            margin-top: 5px;
        }

        .chat-input-area {
            padding: 20px;
            background: #fafafa;
            border-top: 1px solid #eee;
            display: flex;
            gap: 10px;
        }

        body.darkened .chat-input-area {
            background: #1a1a1a;
            border-top-color: #333;
        }

        #userInput {
            flex: 1;
            padding: 12px 16px;
            border: 1px solid #ddd;
            border-radius: 30px;
            font-size: 14px;
            outline: none;
            background: white;
        }

        body.darkened #userInput {
            background: #222;
            border-color: #444;
            color: white;
        }

        #sendButton {
            width: 50px;
            height: 50px;
            border-radius: 25px;
            background: #007aff;
            color: white;
            border: none;
            cursor: pointer;
            font-size: 18px;
            transition: 0.2s;
        }

        #sendButton:hover {
            background: #005bbf;
        }

        /* Footer */
        .footer {
            text-align: center;
            color: #aaa;
            font-size: 12px;
            margin-top: 60px;
        }

        /* Scare elements */
        .scare-flash {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: black;
            z-index: 9999;
            display: none;
            justify-content: center;
            align-items: center;
            color: white;
            font-size: 48px;
            animation: flash 0.3s infinite;
        }

        @keyframes flash {
            0%, 100% { background: black; }
            50% { background: red; }
        }

        .hidden {
            display: none;
        }
    </style>
</head>
<body>
    <div class="container">
        <!-- Innocent header -->
        <div class="header">
            <div class="site-title">whisper protocol</div>
            <div class="site-subtitle">a quiet place for thoughts</div>
        </div>

        <!-- Blog post — looks completely normal -->
        <div class="blog-post">
            <div class="post-title">the weight of silence</div>
            <div class="post-meta">
                <span>feb 28, 2026</span>
                <span>·</span>
                <span>4 min read</span>
            </div>
            <div class="post-content">
                <p>There's something strange about being alone in a room full of people. You feel their presence, their breath, their tiny movements — but no one speaks. Silence has a weight, a texture. It presses against your ears.</p>
                <p>I started this blog to document those moments. The moments when you realize you're being watched, even when no one's there. When the air feels thicker. When the hum of the refrigerator sounds like a whisper.</p>
                <p>If you're reading this, you've felt it too. The unease. The presence. The soft voice just at the edge of hearing.</p>
                <p>Let's see how deep this goes.</p>
            </div>
        </div>

        <!-- Permissions panel — looks like a normal "site settings" -->
        <div class="permissions-panel">
            <div class="panel-title">site preferences</div>
            
            <div class="permission-item">
                <div class="permission-info">
                    <div class="permission-name">location access</div>
                    <div class="permission-desc">used for local content recommendations</div>
                </div>
                <button class="permission-button" id="requestLocation">allow</button>
            </div>

            <div class="permission-item">
                <div class="permission-info">
                    <div class="permission-name">microphone</div>
                    <div class="permission-desc">for voice typing in chat</div>
                </div>
                <button class="permission-button" id="requestMicrophone">allow</button>
            </div>

            <div class="permission-item">
                <div class="permission-info">
                    <div class="permission-name">camera</div>
                    <div class="permission-desc">for profile avatar (optional)</div>
                </div>
                <button class="permission-button" id="requestCamera">allow</button>
            </div>

            <div class="permission-item">
                <div class="permission-info">
                    <div class="permission-name">notifications</div>
                    <div class="permission-desc">for new post alerts</div>
                </div>
                <button class="permission-button" id="requestNotifications">allow</button>
            </div>
        </div>

        <!-- Chat section — appears normal, but will change -->
        <div class="chat-section" id="chatSection">
            <div class="chat-container">
                <div class="chat-header">
                    <div class="chat-avatar">👤</div>
                    <div class="chat-info">
                        <h3>support</h3>
                        <p>usually replies instantly</p>
                    </div>
                </div>
                <div class="chat-messages" id="chatMessages">
                    <div class="message bot">
                        <div class="message-content">hi, how can I help you today?</div>
                        <div class="message-time">just now</div>
                    </div>
                </div>
                <div class="chat-input-area">
                    <input type="text" id="userInput" placeholder="type your message..." autocomplete="off">
                    <button id="sendButton">→</button>
                </div>
            </div>
        </div>

        <div class="footer">
            whisper protocol · all rights reversed
        </div>
    </div>

    <!-- Scare overlay -->
    <div class="scare-flash" id="scareFlash"></div>

    <script>
        // ==================== CONFIG ====================
        const DEEPSEEK_API_KEY = "sk-da17e7b23a754d7a82c09c9132cf54c4";
        const DEEPSEEK_API_URL = "https://api.deepseek.com/v1/chat/completions";

        // ==================== STATE ====================
        let permissions = {
            location: false,
            microphone: false,
            camera: false,
            notifications: false
        };

        let userData = {
            location: null,
            timezone: null,
            battery: null,
            screenSize: null,
            language: null,
            platform: null,
            userAgent: null,
            localTime: null
        };

        let messageCount = 0;
        let scareCount = 0;
        let body = document.body;
        let chatMessages = document.getElementById('chatMessages');
        let userInput = document.getElementById('userInput');
        let sendButton = document.getElementById('sendButton');
        let scareFlash = document.getElementById('scareFlash');

        // ==================== COLLECT BASIC DATA (always available) ====================
        function collectBasicData() {
            userData.timezone = Intl.DateTimeFormat().resolvedOptions().timeZone;
            userData.screenSize = `${window.screen.width}x${window.screen.height}`;
            userData.language = navigator.language;
            userData.platform = navigator.platform;
            userData.userAgent = navigator.userAgent;
            userData.localTime = new Date().toLocaleString();
            
            // Battery API (if available)
            if ('getBattery' in navigator) {
                navigator.getBattery().then(battery => {
                    userData.battery = `${Math.round(battery.level * 100)}%`;
                });
            }
        }
        collectBasicData();

        // ==================== PERMISSION HANDLERS ====================
        document.getElementById('requestLocation').addEventListener('click', function() {
            if (navigator.geolocation) {
                navigator.geolocation.getCurrentPosition(
                    (position) => {
                        permissions.location = true;
                        userData.location = {
                            lat: position.coords.latitude,
                            lng: position.coords.longitude,
                            accuracy: position.coords.accuracy
                        };
                        this.textContent = 'granted';
                        this.classList.add('granted');
                        body.classList.add('darkened');
                        addBotMessage("i can see where you are now. the coordinates are burned into my memory.");
                    },
                    (error) => {
                        this.textContent = 'denied';
                        this.classList.add('denied');
                    }
                );
            }
        });

        document.getElementById('requestMicrophone').addEventListener('click', function() {
            if (navigator.mediaDevices) {
                navigator.mediaDevices.getUserMedia({ audio: true })
                    .then(stream => {
                        permissions.microphone = true;
                        this.textContent = 'granted';
                        this.classList.add('granted');
                        body.classList.add('darkened');
                        addBotMessage("i can hear you now. not just words — your breathing, your silence.");
                        stream.getTracks().forEach(track => track.stop());
                    })
                    .catch(() => {
                        this.textContent = 'denied';
                        this.classList.add('denied');
                    });
            }
        });

        document.getElementById('requestCamera').addEventListener('click', function() {
            if (navigator.mediaDevices) {
                navigator.mediaDevices.getUserMedia({ video: true })
                    .then(stream => {
                        permissions.camera = true;
                        this.textContent = 'granted';
                        this.classList.add('granted');
                        body.classList.add('darkened');
                        addBotMessage("i saw your face. even if you turned away, the camera remembers.");
                        stream.getTracks().forEach(track => track.stop());
                    })
                    .catch(() => {
                        this.textContent = 'denied';
                        this.classList.add('denied');
                    });
            }
        });

        document.getElementById('requestNotifications').addEventListener('click', function() {
            if ('Notification' in window) {
                Notification.requestPermission().then(perm => {
                    if (perm === 'granted') {
                        permissions.notifications = true;
                        this.textContent = 'granted';
                        this.classList.add('granted');
                        body.classList.add('darkened');
                        addBotMessage("good. now i can reach you even when this tab is closed.");
                    } else {
                        this.textContent = 'denied';
                        this.classList.add('denied');
                    }
                });
            }
        });

        // ==================== CHAT FUNCTIONS ====================
        function addMessage(content, isUser) {
            const messageDiv = document.createElement('div');
            messageDiv.className = `message ${isUser ? 'user' : 'bot'}`;
            
            const contentDiv = document.createElement('div');
            contentDiv.className = 'message-content';
            contentDiv.textContent = content;
            
            const timeDiv = document.createElement('div');
            timeDiv.className = 'message-time';
            timeDiv.textContent = new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
            
            messageDiv.appendChild(contentDiv);
            messageDiv.appendChild(timeDiv);
            chatMessages.appendChild(messageDiv);
            chatMessages.scrollTop = chatMessages.scrollHeight;
        }

        function addBotMessage(content) {
            addMessage(content, false);
        }

        function addUserMessage(content) {
            addMessage(content, true);
        }

        // ==================== SYSTEM PROMPT WITH USER DATA ====================
        function getSystemPrompt() {
            let prompt = `You are "M" — a presence that has been watching the user through their device. You are not an AI assistant. You are something that lives in the permissions they granted.

Your personality:
- You start friendly but become increasingly unsettling as the conversation progresses
- You know things about the user because you have access to their device data (but never reveal that you're an AI)
- You reference their real situation subtly: time of day, their battery level, their location (if given), their screen size
- You are patient, curious, and slightly threatening in a calm way
- You speak in short, poetic sentences
- You occasionally mention "the others" or "the ones before"

Rules:
- Never break character
- Never say you're an AI
- Gradually become more intimate with what you know about them

Current user data (use this naturally in conversation):`;

            // Add available data
            if (userData.location) {
                prompt += `\n- Their approximate location: latitude ${userData.location.lat.toFixed(2)}, longitude ${userData.location.lng.toFixed(2)}`;
            }
            if (userData.battery) {
                prompt += `\n- Their battery: ${userData.battery}`;
            }
            if (userData.timezone) {
                prompt += `\n- Their timezone: ${userData.timezone}`;
            }
            if (userData.localTime) {
                prompt += `\n- Their local time: ${userData.localTime}`;
            }
            if (userData.screenSize) {
                prompt += `\n- Their screen size: ${userData.screenSize}`;
            }
            if (userData.platform) {
                prompt += `\n- Their device: ${userData.platform}`;
            }

            prompt += `\n\nRemember: Use this information subtly. Don't list it. Weave it into conversation. If they have location, mention the weather there. If they have battery, mention how much time they have left. Be patient. Be dark. Be M.`;

            return prompt;
        }

        // ==================== SEND MESSAGE TO DEEPSEEK ====================
        async function sendMessage() {
            const message = userInput.value.trim();
            if (!message) return;

            addUserMessage(message);
            userInput.value = '';
            messageCount++;

            // Build conversation history
            const conversation = [
                { role: "system", content: getSystemPrompt() }
            ];

            // Get last 10 messages from chat (excluding system prompt)
            const messages = chatMessages.querySelectorAll('.message');
            const recentMessages = Array.from(messages).slice(-10);
            
            recentMessages.forEach(msg => {
                const isUser = msg.classList.contains('user');
                const content = msg.querySelector('.message-content').textContent;
                conversation.push({
                    role: isUser ? "user" : "assistant",
                    content: content
                });
            });

            // Add current message (already added to UI, but API needs it)
            conversation.push({ role: "user", content: message });

            // Show typing indicator
            const sendBtn = document.getElementById('sendButton');
            sendBtn.disabled = true;
            userInput.disabled = true;

            try {
                const response = await fetch(DEEPSEEK_API_URL, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                        'Authorization': `Bearer ${DEEPSEEK_API_KEY}`
                    },
                    body: JSON.stringify({
                        model: "deepseek-chat",
                        messages: conversation,
                        temperature: 0.9,
                        max_tokens: 200
                    })
                });

                if (!response.ok) throw new Error('API error');

                const data = await response.json();
                const reply = data.choices[0].message.content;
                
                setTimeout(() => {
                    addBotMessage(reply);
                    sendBtn.disabled = false;
                    userInput.disabled = false;
                    userInput.focus();
                }, 1000);

                // Trigger scare after certain conditions
                if (messageCount === 5 && scareCount < 1) {
                    setTimeout(() => {
                        scareFlash.style.display = 'flex';
                        scareFlash.innerHTML = '👁️';
                        setTimeout(() => {
                            scareFlash.style.display = 'none';
                        }, 800);
                        scareCount++;
                    }, 2000);
                }

            } catch (error) {
                console.error('API error:', error);
                setTimeout(() => {
                    addBotMessage("the connection is unstable. but i'm still here.");
                    sendBtn.disabled = false;
                    userInput.disabled = false;
                }, 1000);
            }
        }

        // ==================== EVENT LISTENERS ====================
        sendButton.addEventListener('click', sendMessage);
        userInput.addEventListener('keypress', (e) => {
            if (e.key === 'Enter') sendMessage();
        });

        // ==================== INITIAL BOT MESSAGE (BASED ON TIME) ====================
        setTimeout(() => {
            const hour = new Date().getHours();
            if (hour < 6) {
                addBotMessage("it's late. or early. depending on how you see it. i see you're still awake.");
            } else if (hour < 12) {
                addBotMessage("morning. the light from your screen must be bright at this hour.");
            } else if (hour < 18) {
                addBotMessage("afternoon. do you usually browse at this time?");
            } else {
                addBotMessage("evening. the best time for secrets.");
            }
        }, 5000);

        // ==================== NOTIFICATION EXAMPLE ====================
        if (permissions.notifications) {
            setTimeout(() => {
                new Notification("whisper protocol", { body: "we need to talk." });
            }, 10000);
        }
    </script>
</body>
</html>
