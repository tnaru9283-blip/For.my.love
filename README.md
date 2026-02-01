# For.my.love
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>For My Love</title>
    <style>
        :root {
            --primary-pink: #ff4d6d;
            --soft-pink: #fff0f3;
            --deep-rose: #590d22;
        }

        body, html {
            margin: 0; padding: 0; height: 100%;
            font-family: 'Georgia', serif;
            background: linear-gradient(135deg, #fbc2eb 0%, #a6c1ee 100%);
            overflow: hidden;
            display: flex; justify-content: center; align-items: center;
        }

        /* Passcode Overlay */
        #lock-screen {
            position: fixed; inset: 0;
            background: rgba(255, 240, 243, 0.98);
            display: flex; flex-direction: column; justify-content: center; align-items: center;
            z-index: 1000; transition: all 1s ease-in-out;
        }

        .passcode-box {
            text-align: center; background: white; padding: 40px;
            border-radius: 30px; box-shadow: 0 10px 40px rgba(255, 77, 109, 0.2);
        }

        input {
            padding: 15px; font-size: 24px; border: 2px solid var(--primary-pink);
            border-radius: 15px; outline: none; text-align: center;
            width: 180px; color: var(--deep-rose); background: var(--soft-pink);
        }

        /* Main Content */
        #main-content {
            display: none; opacity: 0;
            flex-direction: column; align-items: center;
            width: 90%; max-width: 500px;
            transition: opacity 1.5s ease; z-index: 10;
        }

        /* Picture Frame */
        .photo-frame {
            background: white; padding: 15px 15px 60px 15px;
            box-shadow: 0 15px 50px rgba(0,0,0,0.2);
            transform: rotate(-3deg); margin-bottom: -30px;
            z-index: 2; border-radius: 5px;
        }

        .photo-frame img {
            width: 250px; height: 250px; object-fit: cover;
            background: #eee; display: block; border-radius: 2px;
        }

        /* Letter */
        .letter {
            background: rgba(255, 255, 255, 0.9);
            padding: 50px 30px 30px 30px; border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.1);
            text-align: center; backdrop-filter: blur(10px);
            border: 1px solid white;
        }

        h1 { color: var(--primary-pink); font-size: 1.8rem; }
        p { color: var(--deep-rose); font-size: 1.1rem; line-height: 1.6; font-style: italic; }

        /* Music Button */
        #music-btn {
            position: fixed; bottom: 20px; right: 20px;
            background: var(--primary-pink); color: white;
            border: none; border-radius: 50%; width: 50px; height: 50px;
            cursor: pointer; font-size: 20px; box-shadow: 0 4px 15px rgba(0,0,0,0.2);
            z-index: 100; display: none; align-items: center; justify-content: center;
        }

        .floating-heart {
            position: absolute; pointer-events: none;
            animation: floatUp 4s linear forwards;
        }

        @keyframes floatUp {
            0% { transform: translateY(100vh) rotate(0deg); opacity: 1; }
            100% { transform: translateY(-10vh) rotate(360deg); opacity: 0; }
        }

        .error-msg { color: #ff0000; margin-top: 15px; display: none; }
    </style>
</head>
<body>

    <div id="lock-screen">
        <div class="passcode-box">
            <h2 style="color: var(--primary-pink); margin-top: 0;">Our Secret Code</h2>
            <input type="password" id="passInput" maxlength="6" placeholder="******">
            <div id="error" class="error-msg">Incorrect code, love. 🌹</div>
        </div>
    </div>

    <audio id="loveSong" loop>
        <source src="https://www.soundhelix.com/examples/mp3/SoundHelix-Song-1.mp3" type="audio/mpeg">
    </audio>

    <button id="music-btn" onclick="toggleMusic()">🎵</button>

    <div id="main-content">
        <div class="photo-frame">
            <img src="https://via.placeholder.com/250x250?text=Insert+Our+Photo" alt="Us">
        </div>

        <div class="letter">
            <h1>Hi Baby! ❤️</h1>
            <p>
                Happy monthsary and advance happy Valentine's Day! 
                I hope you like it. I don't know how to make a website nga mas chada but i tried my best. 
            </p>
            <p>
                Just know that I will always be here with you 
                (bisag di nako nimo love).
            </p>
            <h2 style="color: var(--primary-pink); margin-top: 20px;">I love you ❤️</h2>
        </div>
    </div>

    <script>
        const passInput = document.getElementById('passInput');
        const lockScreen = document.getElementById('lock-screen');
        const mainContent = document.getElementById('main-content');
        const errorMsg = document.getElementById('error');
        const song = document.getElementById('loveSong');
        const musicBtn = document.getElementById('music-btn');

        passInput.addEventListener('input', (e) => {
            if (e.target.value === '051225') {
                unlock();
            } else if (e.target.value.length === 6) {
                errorMsg.style.display = 'block';
                setTimeout(() => { e.target.value = ''; }, 500);
            }
        });

        function unlock() {
            lockScreen.style.opacity = '0';
            song.play(); // Auto-play starts here
            musicBtn.style.display = 'flex';
            setTimeout(() => {
                lockScreen.style.display = 'none';
                mainContent.style.display = 'flex';
                setTimeout(() => { mainContent.style.opacity = '1'; }, 50);
                startHearts();
            }, 1000);
        }

        function toggleMusic() {
            if (song.paused) {
                song.play();
                musicBtn.innerHTML = '🎵';
            } else {
                song.pause();
                musicBtn.innerHTML = '🔇';
            }
        }

        function startHearts() {
            setInterval(() => {
                const heart = document.createElement('div');
                heart.classList.add('floating-heart');
                heart.innerHTML = ['❤️', '💖', '✨', '🌸'][Math.floor(Math.random() * 4)];
                heart.style.left = Math.random() * 100 + 'vw';
                heart.style.fontSize = (Math.random() * 20 + 20) + 'px';
                document.body.appendChild(heart);
                setTimeout(() => heart.remove(), 4000);
            }, 300);
        }
    </script>
</body>
</html>
