<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>aziz efe - Chatbot</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #6e8efb, #a777e3);
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }
        
        .chat-container {
            width: 100%;
            max-width: 400px;
            height: 600px;
            background-color: white;
            border-radius: 16px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            display: flex;
            flex-direction: column;
            overflow: hidden;
        }
        
        .chat-header {
            background: linear-gradient(135deg, #6e8efb, #a777e3);
            color: white;
            padding: 20px;
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .logo {
            width: 45px;
            height: 45px;
            border-radius: 50%;
            background-color: white;
            display: flex;
            justify-content: center;
            align-items: center;
            font-weight: bold;
            color: #6e8efb;
            font-size: 18px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        
        .logo img {
            width: 100%;
            height: 100%;
            border-radius: 50%;
            object-fit: cover;
        }
        
        .chat-header-content {
            flex: 1;
        }
        
        .chat-header h2 {
            font-size: 18px;
            font-weight: 600;
            margin-bottom: 4px;
        }
        
        .status {
            display: flex;
            align-items: center;
            gap: 6px;
            font-size: 12px;
        }
        
        .status-indicator {
            width: 8px;
            height: 8px;
            background-color: #4cd964;
            border-radius: 50%;
        }
        
        .chat-messages {
            flex: 1;
            padding: 20px;
            overflow-y: auto;
            display: flex;
            flex-direction: column;
            gap: 15px;
            background-color: #f5f7fb;
        }
        
        .message {
            max-width: 80%;
            padding: 12px 16px;
            border-radius: 18px;
            line-height: 1.4;
            animation: fadeIn 0.3s ease;
            position: relative;
        }
        
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        
        .bot-message {
            background-color: white;
            border-bottom-left-radius: 4px;
            align-self: flex-start;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
            border: 1px solid #eee;
        }
        
        .user-message {
            background: linear-gradient(135deg, #6e8efb, #a777e3);
            color: white;
            border-bottom-right-radius: 4px;
            align-self: flex-end;
            box-shadow: 0 2px 5px rgba(110, 142, 251, 0.3);
        }
        
        .message-time {
            font-size: 10px;
            margin-top: 5px;
            opacity: 0.7;
            text-align: right;
        }
        
        .chat-input-container {
            padding: 15px 20px;
            border-top: 1px solid #eee;
            display: flex;
            gap: 10px;
            background-color: white;
        }
        
        .chat-input {
            flex: 1;
            padding: 12px 16px;
            border: 1px solid #ddd;
            border-radius: 24px;
            outline: none;
            transition: border-color 0.3s;
            font-size: 14px;
        }
        
        .chat-input:focus {
            border-color: #6e8efb;
        }
        
        .send-button {
            background: linear-gradient(135deg, #6e8efb, #a777e3);
            color: white;
            border: none;
            width: 45px;
            height: 45px;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: transform 0.2s;
            box-shadow: 0 2px 10px rgba(110, 142, 251, 0.3);
        }
        
        .send-button:hover {
            transform: scale(1.05);
        }
        
        .welcome-container {
            text-align: center;
            padding: 20px;
            background-color: white;
            border-radius: 12px;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
            margin: 15px;
        }
        
        .welcome-title {
            color: #6e8efb;
            font-weight: 600;
            margin-bottom: 10px;
        }
        
        .welcome-text {
            color: #666;
            line-height: 1.5;
            margin-bottom: 15px;
        }
        
        .start-chat-button {
            background: linear-gradient(135deg, #6e8efb, #a777e3);
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 24px;
            cursor: pointer;
            font-weight: 600;
            transition: transform 0.2s;
            box-shadow: 0 2px 10px rgba(110, 142, 251, 0.3);
        }
        
        .start-chat-button:hover {
            transform: scale(1.05);
        }
        
        .typing-indicator {
            display: flex;
            align-items: center;
            gap: 5px;
            margin-top: 5px;
        }
        
        .typing-dot {
            width: 6px;
            height: 6px;
            background-color: #a777e3;
            border-radius: 50%;
            animation: typingAnimation 1.4s infinite ease-in-out;
        }
        
        .typing-dot:nth-child(1) { animation-delay: 0s; }
        .typing-dot:nth-child(2) { animation-delay: 0.2s; }
        .typing-dot:nth-child(3) { animation-delay: 0.4s; }
        
        @keyframes typingAnimation {
            0%, 60%, 100% { transform: translateY(0); }
            30% { transform: translateY(-5px); }
        }
        
        .suggestion-chips {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-top: 10px;
        }
        
        .suggestion-chip {
            background-color: #f0f4ff;
            color: #6e8efb;
            padding: 8px 15px;
            border-radius: 16px;
            font-size: 12px;
            cursor: pointer;
            transition: background-color 0.2s;
        }
        
        .suggestion-chip:hover {
            background-color: #e2e9ff;
        }
        
        @media (max-width: 480px) {
            .chat-container {
                height: 100%;
                max-height: 100vh;
                border-radius: 0;
            }
            
            body {
                padding: 0;
            }
        }
    </style>
</head>
<body>
    <div class="chat-container">
        <div class="chat-header">
            <div class="logo">
                <!-- Logo URL'si buraya eklenebilir -->
                <span>AE</span>
            </div>
            <div class="chat-header-content">
                <h2>aziz efe</h2>
                <div class="status">
                    <div class="status-indicator"></div>
                    <span>Çevrimiçi</span>
                </div>
            </div>
        </div>
        
        <div class="chat-messages" id="chatMessages">
            <div class="welcome-container">
                <div class="welcome-title">Merhaba!</div>
                <div class="welcome-text">Sorularınıza anında yanıt alın! Sohbet etmek için aşağıdaki butona tıklayın.</div>
                <button class="start-chat-button" id="startButton">
                    Sohbeti Başlat
                </button>
            </div>
        </div>
        
        <div class="chat-input-container" id="inputContainer" style="display: none;">
            <input type="text" class="chat-input" placeholder="Bir mesaj yazın..." id="messageInput">
            <button class="send-button" id="sendButton">
                <i class="fas fa-paper-plane"></i>
            </button>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const messageInput = document.getElementById('messageInput');
            const sendButton = document.getElementById('sendButton');
            const chatMessages = document.getElementById('chatMessages');
            const startButton = document.getElementById('startButton');
            const inputContainer = document.getElementById('inputContainer');
            
            // Webhook yapılandırması
            const webhookConfig = {
                url: 'https://n8n.n8naziz.com/webhook/ec6ff37a-76be-415e-880b-da4df99fc075/chat',
                route: 'general'
            };
            
            // Marka yapılandırması
            const branding = {
                logo: 'INSERT_LOGO_URL',
                name: 'aziz efe',
                welcomeText: 'Sorularınıza anında yanıt alın!',
                responseTimeText: 'Sohbet etmek için aşağıdaki butona tıklayın'
            };
            
            // Öneri mesajları
            const suggestions = [
                "Nasıl yardımcı olabilirsiniz?",
                "Hizmetleriniz neler?",
                "İletişim bilgileriniz nedir?",
                "Fiyatlar hakkında bilgi alabilir miyim?"
            ];
            
            // Sohbeti başlatma
            startButton.addEventListener('click', function() {
                startButton.parentElement.style.display = 'none';
                inputContainer.style.display = 'flex';
                
                // İlk bot mesajını ekle
                setTimeout(() => {
                    addMessage('Merhaba! Size nasıl yardımcı olabilirim?', 'bot');
                    showSuggestions();
                }, 500);
            });
            
            // Mesaj gönderme fonksiyonu
            function sendMessage() {
                const message = messageInput.value.trim();
                if (message === '') return;
                
                // Kullanıcı mesajını ekrana ekle
                addMessage(message, 'user');
                messageInput.value = '';
                
                // Öneri çiplerini temizle
                document.querySelectorAll('.suggestion-chips').forEach(el => el.remove());
                
                // Botun yazıyor gösterimi
                const typingIndicator = document.createElement('div');
                typingIndicator.className = 'message bot-message typing-indicator';
                typingIndicator.innerHTML = `
                    <div>Yazıyor...</div>
                    <div class="typing-dots">
                        <div class="typing-dot"></div>
                        <div class="typing-dot"></div>
                        <div class="typing-dot"></div>
                    </div>
                `;
                chatMessages.appendChild(typingIndicator);
                chatMessages.scrollTop = chatMessages.scrollHeight;
                
                // Webhook'a istek gönder
                fetch(webhookConfig.url, {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                    },
                    body: JSON.stringify({
                        message: message,
                        route: webhookConfig.route
                    })
                })
                .then(response => {
                    if (!response.ok) {
                        throw new Error('Webhook hatası');
                    }
                    return response.json();
                })
                .then(data => {
                    // Yazıyor gösterimini kaldır
                    chatMessages.removeChild(typingIndicator);
                    
                    // Bot yanıtını ekrana ekle
                    if (data && data.response) {
                        addMessage(data.response, 'bot');
                    } else {
                        addMessage('Mesajınızı aldım, en kısa sürede dönüş yapacağım.', 'bot');
                    }
                    
                    // Önerileri göster
                    showSuggestions();
                })
                .catch(error => {
                    console.error('Error:', error);
                    chatMessages.removeChild(typingIndicator);
                    addMessage('Üzgünüm, şu anda teknik bir sorun yaşıyorum. Lütfen daha sonra tekrar deneyin.', 'bot');
                });
            }
            
            // Mesaj ekleme fonksiyonu
            function addMessage(text, sender) {
                const messageElement = document.createElement('div');
                messageElement.className = `message ${sender}-message`;
                
                const now = new Date();
                const time = now.getHours().toString().padStart(2, '0') + ':' + 
                             now.getMinutes().toString().padStart(2, '0');
                
                messageElement.innerHTML = `
                    <div>${text}</div>
                    <div class="message-time">${time}</div>
                `;
                
                chatMessages.appendChild(messageElement);
                chatMessages.scrollTop = chatMessages.scrollHeight;
            }
            
            // Öneri çiplerini göster
            function showSuggestions() {
                const chipsContainer = document.createElement('div');
                chipsContainer.className = 'suggestion-chips';
                
                suggestions.forEach(suggestion => {
                    const chip = document.createElement('div');
                    chip.className = 'suggestion-chip';
                    chip.textContent = suggestion;
                    chip.addEventListener('click', () => {
                        messageInput.value = suggestion;
                        sendMessage();
                    });
                    chipsContainer.appendChild(chip);
                });
                
                chatMessages.appendChild(chipsContainer);
                chatMessages.scrollTop = chatMessages.scrollHeight;
            }
            
            // Enter tuşu ve buton olayları
            sendButton.addEventListener('click', sendMessage);
            messageInput.addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    sendMessage();
                }
            });
        });
    </script>
</body>
</html>
