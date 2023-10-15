# GPT
<!DOCTYPE html>
<html>
<head>
    <title>ChatGPT Web App</title>
</head>
<body>
    <h1>Chat with GPT-3</h1>
    <div id="chat-container">
        <div id="chat-output"></div>
        <input type="text" id="user-input" placeholder="Type a message...">
        <button id="send-button">Send</button>
    </div>

    <script>
        // Đặt API Key của bạn ở đây
        const apiKey = 'YOUR_API_KEY';

        const chatOutput = document.getElementById('chat-output');
        const userInput = document.getElementById('user-input');
        const sendButton = document.getElementById('send-button');

        sendButton.addEventListener('click', () => {
            const userMessage = userInput.value;
            
            // Gửi yêu cầu đến API ChatGPT
            fetch('https://api.openai.com/v1/engines/davinci-codex/completions', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    'Authorization': `Bearer ${apiKey}`
                },
                body: JSON.stringify({
                    prompt: userMessage,
                    max_tokens: 50
                })
            })
            .then(response => response.json())
            .then(data => {
                const chatResponse = data.choices[0].text;
                displayResponse(chatResponse);
            })
            .catch(error => console.error(error));
        });

        function displayResponse(response) {
            // Hiển thị câu trả lời trên giao diện
            const responseElement = document.createElement('p');
            responseElement.textContent = response;
            chatOutput.appendChild(responseElement);

            // Xóa nội dung đầu vào người dùng
            userInput.value = '';
        }
    </script>
</body>
</html>
