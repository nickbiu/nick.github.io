<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <title>专业AI对话助手</title>
    <style>
        /* 专业级UI设计 */
        body {
            font-family: 'Segoe UI', Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background: #f5f5f5;
        }
        .chat-container {
            background: white;
            border-radius: 12px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            height: 70vh;
            overflow-y: auto;
            padding: 20px;
        }
        .message {
            margin: 15px 0;
            max-width: 80%;
        }
        .user-message {
            margin-left: auto;
            background: #007bff;
            color: white;
            border-radius: 15px 15px 0 15px;
        }
        .ai-message {
            background: #f8f9fa;
            border-radius: 15px 15px 15px 0;
        }
        .message-content {
            padding: 12px 18px;
            line-height: 1.6;
        }
        .input-container {
            margin-top: 20px;
            display: flex;
            gap: 10px;
        }
        input {
            flex: 1;
            padding: 12px;
            border: 2px solid #ddd;
            border-radius: 25px;
            font-size: 16px;
        }
        button {
            padding: 12px 25px;
            background: #007bff;
            color: white;
            border: none;
            border-radius: 25px;
            cursor: pointer;
            transition: background 0.3s;
        }
        button:hover {
            background: #0056b3;
        }
    </style>
</head>
<body>
    <div class="chat-container" id="chatBox"></div>
    <div class="input-container">
        <input type="text" id="userInput" placeholder="请输入您的问题..." />
        <button onclick="sendMessage()">发送</button>
    </div>

    <script>
        // 替换为您自己的OpenAI API密钥
        const API_KEY = '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';
        
        async function sendMessage() {
            const userInput = document.getElementById('userInput');
            const message = userInput.value.trim();
            if (!message) return;

            // 添加用户消息
            addMessage(message, 'user');
            userInput.value = '';

            try {
                // 调用GPT-4 API
                const response = await fetch('https://api.openai.com/v1/chat/completions', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                        'Authorization': `Bearer ${API_KEY}`
                    },
                    body: JSON.stringify({
                        model: "gpt-4",
                        messages: [{
                            role: "user",
                            content: `${message} 请用专业严谨的学术语言回答，保持逻辑清晰并提供可靠依据。`
                        }],
                        temperature: 0.7,
                        max_tokens: 1000
                    })
                });

                const data = await response.json();
                const aiResponse = data.choices[0].message.content;
                addMessage(aiResponse, 'ai');
            } catch (error) {
                console.error('API请求失败:', error);
                addMessage("当前请求出现异常，请稍后再试。", 'ai');
            }
        }

        function addMessage(content, sender) {
            const chatBox = document.getElementById('chatBox');
            const messageDiv = document.createElement('div');
            messageDiv.className = `message ${sender}-message`;
            messageDiv.innerHTML = `
                <div class="message-content">${content}</div>
            `;
            chatBox.appendChild(messageDiv);
            chatBox.scrollTop = chatBox.scrollHeight;
        }

        // 回车发送
        document.getElementById('userInput').addEventListener('keypress', (e) => {
            if (e.key === 'Enter') sendMessage();
        });
    </script>
</body>
</html>
