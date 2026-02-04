<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Be My Valentine? ❤️</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; }
        
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            background: linear-gradient(180deg, #ffafbd 0%, #ffc3a0 100%);
            font-family: 'Arial Rounded MT Bold', 'Helvetica', sans-serif;
            overflow: hidden; /* Prevents scrolling on mobile */
            padding: 20px;
        }

        #container {
            background: rgba(255, 255, 255, 0.9);
            padding: 30px 20px;
            border-radius: 30px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.1);
            text-align: center;
            width: 100%;
            max-width: 350px;
            z-index: 10;
        }

        h1 { color: #d63384; font-size: 1.8rem; margin-bottom: 20px; }

        .buttons {
            display: flex;
            flex-direction: column; /* Stacked for easier tapping on mobile */
            gap: 15px;
            align-items: center;
            margin-top: 20px;
            position: relative;
            height: 150px; /* Space for moving button */
        }

        button {
            padding: 15px 30px;
            font-size: 1.2rem;
            border: none;
            border-radius: 50px;
            cursor: pointer;
            width: 80%;
            font-weight: bold;
            touch-action: manipulation; /* Optimizes for touch */
        }

        #yesBtn {
            background-color: #ff4d6d;
            color: white;
            transition: transform 0.2s cubic-bezier(0.175, 0.885, 0.32, 1.275);
            z-index: 20;
        }

        #noBtn {
            background-color: #f8f9fa;
            color: #6c757d;
            border: 1px solid #dee2e6;
            position: absolute;
            bottom: 0;
            transition: 0.3s ease;
        }

        .hidden { display: none; }

        #success-ui img { width: 150px; margin-bottom: 15px; }
    </style>
</head>
<body>

    <div id="container">
        <div id="question-ui">
            <h1>Will you be my Valentine? 🌹</h1>
            <div class="buttons">
                <button id="yesBtn">YES</button>
                <button id="noBtn">No</button>
            </div>
        </div>

        <div id="success-ui" class="hidden">
            <h1>YAY! ❤️</h1>
            <p>I'm the luckiest person!</p>
            <p style="font-size: 3rem; margin-top: 10px;">🥰</p>
        </div>
    </div>

    <script>
        const yesBtn = document.getElementById('yesBtn');
        const noBtn = document.getElementById('noBtn');
        const questionUI = document.getElementById('question-ui');
        const successUI = document.getElementById('success-ui');

        let yesScale = 1;

        // Mobile-friendly: Button moves when tapped
        noBtn.addEventListener('touchstart', moveNoButton);
        noBtn.addEventListener('click', moveNoButton);

        function moveNoButton(e) {
            e.preventDefault(); // Prevents accidental double-clicks

            // 1. Make Yes button bigger (Essential for mobile)
            yesScale += 0.4;
            yesBtn.style.transform = `scale(${yesScale})`;

            // 2. Move No button within safe screen bounds
            const padding = 50;
            const maxX = window.innerWidth - noBtn.offsetWidth - padding;
            const maxY = window.innerHeight - noBtn.offsetHeight - padding;
            
            const randomX = Math.max(padding, Math.floor(Math.random() * maxX));
            const randomY = Math.max(padding, Math.floor(Math.random() * maxY));

            noBtn.style.position = 'fixed';
            noBtn.style.left = randomX + 'px';
            noBtn.style.top = randomY + 'px';
        }

        yesBtn.addEventListener('click', () => {
            questionUI.classList.add('hidden');
            successUI.classList.remove('hidden');
        });
    </script>
</body>
</html>
