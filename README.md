<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Cat</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #e0f7fa;
            text-align: center;
            overflow: hidden;
            box-sizing: border-box;
        }
        .container {
            position: relative;
            background-color: #b9fbc0;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            max-width: 90%;
            margin: 10px;
            overflow: hidden;
            box-sizing: border-box;
        }
        .menu {
            margin-bottom: 20px;
        }
        .menu p {
            font-size: 18px;
            color: #00796b;
            margin: 0;
        }
        .emoji {
            font-size: 48px;
            cursor: pointer;
            margin: 10px;
            transition: transform 0.2s;
        }
        .emoji:active {
            transform: scale(1.2);
        }
        .cat {
            font-size: 100px;
            margin: 20px 0;
            transition: transform 1s;
        }
        .cat.sad {
            animation: sad 1s ease-in-out;
        }
        .cat.happy {
            animation: happy 1s ease-in-out;
        }
        .message {
            display: none;
            font-size: 24px;
            color: #00796b;
            margin: 20px 0;
            opacity: 0;
            transition: opacity 1s ease-in-out, font-size 1s ease-in-out;
        }
        .message.new-message {
            display: block;
            opacity: 1;
            font-size: 48px;
        }
        @keyframes sad {
            0% { transform: scale(1); }
            50% { transform: scale(0.9); }
            100% { transform: scale(1); }
        }
        @keyframes happy {
            0% { transform: scale(1); }
            50% { transform: scale(1.1); }
            100% { transform: scale(1); }
        }
        @keyframes float {
            0% { transform: translateY(0) rotate(0); }
            50% { transform: translateY(-20px) rotate(10deg); }
            100% { transform: translateY(0) rotate(0); }
        }
        .kisses, .hearts {
            display: none;
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            overflow: hidden;
        }
        .kisses span, .hearts span {
            display: inline-block;
            position: absolute;
            font-size: 24px;
            animation: float 3s ease-in-out infinite;
        }
        .hearts span {
            font-size: 30px;
        }
        .kisses span:nth-child(1) { top: 10%; left: 20%; }
        .kisses span:nth-child(2) { top: 30%; left: 40%; }
        .kisses span:nth-child(3) { top: 50%; left: 60%; }
        .kisses span:nth-child(4) { top: 70%; left: 80%; }
        .kisses span:nth-child(5) { top: 90%; left: 20%; }
        .hearts span:nth-child(1) { top: 20%; left: 10%; }
        .hearts span:nth-child(2) { top: 40%; left: 30%; }
        .hearts span:nth-child(3) { top: 60%; left: 50%; }
        .hearts span:nth-child(4) { top: 80%; left: 70%; }
        .hearts span:nth-child(5) { top: 20%; left: 80%; }
        .clickable {
            touch-action: manipulation;
        }
        .count {
            font-size: 24px;
            color: #00796b;
            margin: 20px 0;
        }
        .final-message {
            display: none;
            background-color: #007bb2; /* Blue background color */
            color: white; /* White text color */
            padding: 20px;
            border-radius: 10px;
            font-size: 28px;
            margin: 20px 0;
            font-weight: bold;
            text-align: center;
        }
        .final-message img {
            width: 50px; /* Adjust size as needed */
            vertical-align: middle;
            margin-left: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="menu">
            <p>Tap the heart emoji 10 times to make the cat happy. The cat is initially sad.</p>
        </div>
        <div class="cat sad" id="cat">😿</div>
        <div class="emoji clickable" id="heart">❤️</div>
        <div class="count" id="count">Heart taps: 0</div>
        <div class="message" id="message1">Hi, Pogi!!!</div>
        <div class="message" id="message2">Miss you na po!!!</div>
        <div class="kisses" id="kisses">
            <span>😘</span>
            <span>😘</span>
            <span>😘</span>
            <span>😘</span>
            <span>😘</span>
        </div>
        <div class="hearts" id="hearts">
            <span>❤️</span>
            <span>❤️</span>
            <span>❤️</span>
            <span>❤️</span>
            <span>❤️</span>
        </div>
        <!-- New GUI Section -->
        <div class="final-message" id="finalMessage">
            Sarap mong mahalin!!!! <img src="kiss-emoji.png" alt="Kiss Emoji">
        </div>
    </div>

    <script>
        let heartCount = 0;

        function updateHeartCount() {
            document.getElementById('count').textContent = `Heart taps: ${heartCount}`;
        }

        function showMessage(message, isFirstMessage) {
            const messageBox = document.getElementById(isFirstMessage ? 'message1' : 'message2');
            messageBox.textContent = message;
            messageBox.classList.add('new-message');
            setTimeout(() => {
                messageBox.classList.remove('new-message');
            }, 3000);
        }

        function showFloatingElements() {
            const kisses = document.getElementById('kisses');
            const hearts = document.getElementById('hearts');
            kisses.style.display = 'block';
            hearts.style.display = 'block';
        }

        function showFinalMessage() {
            document.getElementById('finalMessage').style.display = 'block';
        }

        document.getElementById('heart').addEventListener('click', function() {
            heartCount++;
            updateHeartCount();
            if (heartCount === 10) {
                document.getElementById('cat').classList.remove('sad');
                document.getElementById('cat').classList.add('happy');
                document.getElementById('cat').textContent = '😸'; // Change to happy cat emoji
                showMessage('Hi, Pogi!!!', true);
                setTimeout(() => {
                    showMessage('Miss you na po!!!', false);
                    showFloatingElements();
                    setTimeout(() => {
                        showFinalMessage();
                    }, 3000); // Delay showing final message
                }, 3000);
            }
        });
    </script>
</body>
</html>
