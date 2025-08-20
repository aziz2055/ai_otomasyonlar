<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>n8n Chat Widget</title>
    
    <link href="https://cdn.jsdelivr.net/npm/@n8n/chat/dist/style.css" rel="stylesheet" />
</head>
<body>

    <div id="n8n-chat"></div>

    <script type="module">
        // n8n chat widget kütüphanesini CDN üzerinden içe aktarıyoruz
        import { createChat } from 'https://cdn.jsdelivr.net/npm/@n8n/chat/dist/chat.bundle.es.js';

        // createChat fonksiyonunu, yapılandırma objesi ile birlikte çağırıyoruz
        createChat({
            // ÖNEMLİ: Bu URL'ye kendi n8n webhook URL'nizi girmeniz gerekmektedir.
            webhookUrl: 'https://n8n.n8naziz.com/webhook/ec6ff37a-76be-415e-880b-da4df99fc075/chat',
            
            webhookConfig: {
                method: 'POST',
                headers: {},
            },
            
            // 'window' modunda olduğu için chatbot sayfanın sağ alt köşesinde açılır.
            target: '#n8n-chat',
            mode: 'window', 
            
            chatInputKey: 'chatInput',
            chatSessionKey: 'sessionId',
            loadPreviousSession: true,
            metadata: {},
            showWelcomeScreen: false,
            defaultLanguage: 'tr',
            initialMessages: [
                'Merhaba! 👋',
                ' Bugün size nasıl yardımcı olabilirim?',
            ],
            
            i18n: {
                // 'en' dil ayarları içinde bulunan tüm metinleri kaldırdım
                en: {
                    title: 'MERHABA',
                    subtitle: 'MRTHABA',
                    footer: 'MERHABA',
                    getStarted: 'MERHABA',
                    inputPlaceholder: 'MERHABA',
                },
            },
            
            enableStreaming: false,
        });
    </script>
</body>
</html>
