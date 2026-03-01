<html lang="te">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>A Special Surprise for You!</title>
    <style>
        :root {
            --primary-red: #ff4d6d;
            --gold: #ffd700;
        }
        body, html { margin: 0; padding: 0; height: 100%; font-family: 'Poppins', sans-serif; overflow: hidden; background: #000; color: white; }
        
        /* PAGE SYSTEM */
        .page { display: none; height: 100vh; width: 100vw; flex-direction: column; align-items: center; justify-content: center; position: absolute; text-align: center; }
        .active { display: flex; animation: slideIn 0.8s ease-out forwards; }
        @keyframes slideIn { from { transform: translateY(20px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }

        /* --- PAGE 1: CATCHY GALAXY HEART --- */
        #page1 { background: radial-gradient(circle at center, #2b0014 0%, #000 100%); }
        .stars { position: absolute; width: 2px; height: 2px; background: white; border-radius: 50%; opacity: 0.5; animation: twinkle 2s infinite; }
        @keyframes twinkle { 0%, 100% { opacity: 0.3; } 50% { opacity: 1; } }

        .floating-heart {
            position: relative; width: 120px; height: 120px;
            background: var(--primary-red); transform: rotate(45deg);
            box-shadow: 0 0 60px var(--primary-red);
            animation: pulse 1.5s infinite ease-in-out; cursor: pointer;
            transition: transform 0.3s;
        }
        .floating-heart::before, .floating-heart::after {
            content: ""; position: absolute; width: 120px; height: 120px;
            background: var(--primary-red); border-radius: 50%;
        }
        .floating-heart::before { left: -60px; }
        .floating-heart::after { top: -60px; }
        @keyframes pulse { 0% { transform: rotate(45deg) scale(1); } 50% { transform: rotate(45deg) scale(1.15); box-shadow: 0 0 100px var(--primary-red); } 100% { transform: rotate(45deg) scale(1); } }
        
        .catchy-text { margin-top: 80px; font-size: 24px; letter-spacing: 3px; font-weight: 200; animation: glowText 2s infinite; }
        @keyframes glowText { 0%, 100% { text-shadow: 0 0 5px #fff; } 50% { text-shadow: 0 0 20px var(--primary-red); } }

        /* --- PAGE 2: GREETING CARD --- */
        #page2 { background: #fff5f7; color: #333; }
        .card { background: white; padding: 40px; border-radius: 20px; box-shadow: 0 20px 50px rgba(0,0,0,0.1); border: 2px dashed var(--primary-red); max-width: 350px; }
        .btn-action { background: var(--primary-red); color: white; border: none; padding: 15px 40px; border-radius: 30px; cursor: pointer; font-size: 18px; margin-top: 20px; transition: 0.3s; }
        .btn-action:hover { background: #d00040; transform: translateY(-3px); }

        /* --- PAGE 3: THE BIG GIFT --- */
        .gift-container { font-size: 120px; cursor: pointer; filter: drop-shadow(0 0 20px gold); animation: wobble 2s infinite; }
        @keyframes wobble { 0%, 100% { transform: rotate(0); } 25% { transform: rotate(-5deg); } 75% { transform: rotate(5deg); } }
        .confetti { position: absolute; width: 10px; height: 10px; opacity: 0; }

        /* --- PAGE 4: TELUGU BLESSINGS --- */
        .temple-icon { font-size: 120px; filter: drop-shadow(0 0 10px orange); }
        .bell-div { font-size: 80px; cursor: pointer; transition: 0.2s; margin: 20px; }
        .bell-ring { animation: ring 0.5s ease-in-out infinite alternate; }
        @keyframes ring { from { transform: rotate(-15deg); } to { transform: rotate(15deg); } }
        .telugu-text { font-size: 24px; color: #800000; padding: 20px; background: rgba(255, 215, 0, 0.2); border-radius: 10px; display: none; }
    </style>
</head>
<body onload="createStars()">

    <div id="page1" class="page active" onclick="nextPage(2)">
        <div class="floating-heart"></div>
        <div class="catchy-text">CLICK THE BEAT</div>
        <p style="opacity: 0.6; font-size: 12px; margin-top: 10px;">A special message is waiting...</p>
    </div>

    <div id="page2" class="page">
        <div class="card">
            <h2 style="color: var(--primary-red);">Happy Anniversary! 🥂</h2>
            <p>Dear Brother & Sister-in-law,</p>
            <p>Wishing you a day as beautiful as the love you share!</p>
            <button class="btn-action" onclick="nextPage(3)">Open Your Gift 🎁</button>
        </div>
    </div>

    <div id="page3" class="page">
        <div class="gift-container" onclick="openGift()">🎁</div>
        <h2 id="gift-h2">A Little Celebration!</h2>
        <button id="next-to-temple" class="btn-action" style="display:none;" onclick="nextPage(4)">Seek Blessings 🪔</button>
    </div>

    <div id="page4" class="page" style="background: #fff8e1; color: #5d4037;">
        <div class="temple-icon">🛕</div>
        <div class="bell-div" id="mainBell" onclick="ringBell()">🔔</div>
        <p>Ring the bell for the couple's happiness!</p>
        <div id="teluguMsg" class="telugu-text">
            మీ ఇద్దరికీ వివాహ వార్షికోత్సవ శుభాకాంక్షలు!<br>
            మరిన్ని సుఖసంతోషాలతో నిండు నూరేళ్లు వర్ధిల్లాలి.
        </div>
    </div>

    <script>
        function createStars() {
            for (let i = 0; i < 100; i++) {
                let star = document.createElement('div');
                star.className = 'stars';
                star.style.left = Math.random() * 100 + 'vw';
                star.style.top = Math.random() * 100 + 'vh';
                star.style.animationDelay = Math.random() * 2 + 's';
                document.getElementById('page1').appendChild(star);
            }
        }

        function nextPage(num) {
            document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
            document.getElementById('page' + num).classList.add('active');
        }

        function openGift() {
            document.getElementById('gift-h2').innerText = "Surprise! ✨";
            document.getElementById('next-to-temple').style.display = "block";
            for (let i = 0; i < 60; i++) {
                let c = document.createElement('div');
                c.className = 'confetti';
                c.style.left = '50%'; c.style.top = '50%';
                c.style.background = ['#ff4d6d','#ffd700','#ffffff','#00e5ff'][Math.floor(Math.random()*4)];
                document.body.appendChild(c);
                let x = (Math.random() - 0.5) * 1000;
                let y = (Math.random() - 0.5) * 1000;
                c.animate([
                    { transform: 'translate(0,0)', opacity: 1 },
                    { transform: `translate(${x}px, ${y}px)`, opacity: 0 }
                ], { duration: 2000, easing: 'ease-out' });
            }
        }

        function ringBell() {
            const bell = document.getElementById('mainBell');
            bell.classList.add('bell-ring');
            setTimeout(() => bell.classList.remove('bell-ring'), 2000);
            document.getElementById('teluguMsg').style.display = "block";
        }
    </script>
</body>
</html>
