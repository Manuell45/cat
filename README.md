<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Animated Letter</title>
    <link href="https://fonts.googleapis.com/css2?family=Great+Vibes&display=swap" rel="stylesheet">
    <style>
        body {
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            background-color: #f0f8ff;
            margin: 0;
        }

        .envelope {
            position: relative;
            width: 300px;
            height: 200px;
            background: #fff;
            border: 2px solid #ccc;
            border-radius: 10px;
            overflow: hidden;
            transition: transform 1s;
            cursor: pointer;
        }

        .envelope::before, .envelope::after {
            content: '';
            position: absolute;
            width: 300px;
            height: 100px;
            background: #fff;
            border: 2px solid #ccc;
            border-top: 0;
            border-bottom-left-radius: 10px;
            border-bottom-right-radius: 10px;
            transition: transform 1s;
        }

        .envelope::before {
            top: 0;
            left: 0;
            transform-origin: bottom;
            transform: rotateX(0deg);
        }

        .envelope::after {
            bottom: 0;
            left: 0;
            transform-origin: top;
            transform: rotateX(0deg);
        }

        .letter {
            display: none;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            text-align: center;
            font-family: 'Great Vibes', cursive;
            font-size: 24px;
            opacity: 0;
        }

        .letter span {
            display: inline-block;
            opacity: 0;
            animation: fadeIn 0.5s forwards;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
            }
            to {
                opacity: 1;
            }
        }
    </style>
</head>
<body>

<div class="envelope" onclick="openEnvelope()">
    <div class="letter" id="letter">
        <span>Y</span><span>O</span><span>U</span> <span>M</span><span>A</span><span>D</span><span>E</span> <span>M</span><span>E</span> <span>T</span><span>H</span><span>E</span> <span>H</span><span>A</span><span>P</span><span>P</span><span>I</span><span>E</span><span>S</span><span>T</span> <span>P</span><span>E</span><span>R</span><span>S</span><span>O</span><span>N</span> <span>I</span><span>'</span><span>V</span><span>E</span> <span>E</span><span>V</span><span>E</span><span>R</span> <span>B</span><span>E</span><span>E</span><span>N</span>.
    </div>
</div>

<script>
    function openEnvelope() {
        const envelope = document.querySelector('.envelope');
        const letter = document.getElementById('letter');
        envelope.style.transform = 'rotateX(180deg)';
        envelope.style.zIndex = '1';
        envelope::before.style.transform = 'rotateX(180deg)';
        envelope::after.style.transform = 'rotateX(180deg)';
        setTimeout(() => {
            letter.style.display = 'block';
            letter.style.opacity = '1';
            const spans = letter.querySelectorAll('span');
            spans.forEach((span, index) => {
                span.style.animationDelay = `${index * 0.1}s`;
            });
        }, 1000);
    }
</script>

</body>
</html>
