<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>FreestyleFriendzy</title>
    <style>
        /* Reset and iPhone optimization */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Arial', sans-serif;
        }

        body {
            background: #1a1a1a;
            color: #fff;
            width: 100%;
            max-width: 375px; /* iPhone screen width */
            margin: 0 auto;
            overflow-x: hidden;
            line-height: 1.5;
            -webkit-font-smoothing: antialiased; /* Smoother text on iOS */
        }

        /* Neon text */
        .neon-text {
            color: #0ff;
            text-shadow: 0 0 5px #0ff, 0 0 10px #0ff, 0 0 20px #0ff;
            animation: glow 1.5s infinite alternate;
        }

        @keyframes glow {
            from { text-shadow: 0 0 5px #0ff, 0 0 10px #0ff; }
            to { text-shadow: 0 0 10px #0ff, 0 0 20px #0ff, 0 0 30px #0ff; }
        }

        /* Homepage */
        #homepage {
            height: 100vh;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            text-align: center;
            padding: 20px;
            background: linear-gradient(135deg, #1a1a1a, #2a2a2a); /* Subtle gradient */
        }

        h1 {
            font-size: 2.5em;
            margin-bottom: 15px;
        }

        p {
            font-size: 1.2em;
            color: #ccc;
            margin-bottom: 25px;
        }

        button {
            background: #ff00ff;
            color: #fff;
            border: none;
            padding: 15px 35px;
            font-size: 1.2em;
            border-radius: 30px;
            cursor: pointer;
            transition: transform 0.2s ease, box-shadow 0.2s ease;
        }

        button:hover {
            transform: scale(1.05);
            box-shadow: 0 0 15px #ff00ff;
        }

        /* Cipher Room */
        #cipher-room {
            display: none;
            padding: 20px;
            min-height: 100vh;
            background: linear-gradient(135deg, #1a1a1a, #2a2a2a);
        }

        textarea {
            width: 100%;
            height: 180px;
            background: #333;
            color: #fff;
            border: 2px solid #0ff;
            border-radius: 10px;
            padding: 15px;
            font-size: 1.1em;
            resize: none;
            box-shadow: 0 0 10px rgba(0, 255, 255, 0.3);
            transition: border-color 0.3s ease;
        }

        textarea:focus {
            border-color: #ff00ff;
            outline: none;
        }

        #freestyle-output {
            margin-top: 20px;
            padding: 15px;
            background: #222;
            border-radius: 10px;
            color: #0ff;
            font-size: 1.1em;
            line-height: 1.6;
        }

        /* Chat simulation */
        #chat-status {
            margin-top: 15px;
            font-size: 0.9em;
            color: #ccc;
            text-align: center;
        }

        /* Rapping animation */
        .mic-animation {
            display: none;
            margin: 15px auto;
            width: 50px;
            height: 50px;
            background: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="50" height="50"><circle cx="25" cy="25" r="20" fill="none" stroke="lime" stroke-width="3"/><line x1="25" y1="5" x2="25" y2="20" stroke="lime" stroke-width="3"/><path d="M15 35 A10 10 0 0 1 35 35" fill="none" stroke="lime" stroke-width="3"/></svg>');
            animation: vibe 1.2s infinite ease-in-out;
        }

        @keyframes vibe {
            0% { transform: scale(1) rotate(0deg); opacity: 1; }
            50% { transform: scale(1.1) rotate(5deg); opacity: 0.85; }
            100% { transform: scale(1) rotate(0deg); opacity: 1; }
        }

        /* Custom cursor */
        * {
            cursor: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" width="32" height="32"><path d="M10 10 L22 22" stroke="lime" stroke-width="3"/></svg>'), auto;
        }
    </style>
</head>
<body>
    <!-- Homepage -->
    <div id="homepage">
        <h1 class="neon-text">FreestyleFriendzy</h1>
        <p>Spit bars. Connect raw. No rules.</p>
        <button onclick="enterCipher()">Join the Cipher</button>
    </div>

    <!-- Cipher Room -->
    <div id="cipher-room">
        <h2 class="neon-text">Cipher Room</h2>
        <textarea id="freestyle-input" placeholder="Drop your bars here..."></textarea>
        <button onclick="findFriendzy()">Find a Friendzy</button>
        <div id="chat-status"></div>
        <div class="mic-animation" id="mic-animation"></div>
        <div id="freestyle-output"></div>
    </div>

    <script>
        // Upgraded pool of 100 sharper freestyles
        const freestylePool = [
            "Yo, I’m slicin’ beats precise, lyrical heist, flow so nice it’s a paradise!",
            "Mic’s my blade, I slay, bars cascade, leave the stage in a blaze!",
            "I’m the rap assassin, no slackin’, verses smashin’ like a titan clashin’!",
            "Flow so pristine, I intervene, spittin’ scenes that reign supreme!",
            "Bars cut deep, I reap, lyrical sweep, got the cipher in a heap!",
            "Yo, I’m the rhyme architect, perfect, dissect your intellect with no defect!",
            "Ink’s my fuel, I rule, droppin’ jewels that school the duel!",
            "I’m the rap phantom, anthem, spittin’ tandem, leave ‘em stranded!",
            "Flow like venom, I send ‘em, bars so clever they bend ‘em!",
            "Mic’s my throne, I’ve grown, verses honed, I’m the cyclone!",
            "Yo, I’m the lyrical beast, unleashed, feast on beats from east to west!",
            "Bars so tight, ignite, I strike, freestyle knight in flight!",
            "I’m the rap alchemist, twist this, turnin’ beats to a gold abyss!",
            "Flow so cold, I mold, stories told in bars of bold!",
            "Mic’s my spear, no fear, I steer, droppin’ bars that sear!",
            "Yo, I’m the rhyme renegade, never fade, cuttin’ through shade with a blade!",
            "Bars like lightning, I’m striking, flow so frightening, I’m igniting!",
            "I’m the rap poet, you know it, verses flowin’ like I own it!",
            "Flow so smooth, I groove, makin’ moves that improve!",
            "Mic’s my crown, I drown, spittin’ sound that shakes the ground!",
            "Yo, I’m the freestyle sage, engage, turn the page, I’m the rap cage!",
            "Bars so raw, I draw, breakin’ every law with no flaw!",
            "I’m the rhyme titan, I tighten, verses lightin’ up the horizon!",
            "Flow like a river, I deliver, make ‘em quiver with my vigor!",
            "Mic’s my torch, I scorch, spittin’ from the porch with force!",
            "Yo, I’m the rap ninja, beginner’s ender, bars so tender yet a contender!",
            "Bars like flames, I claim, reframe the game with no shame!",
            "I’m the freestyle hawk, I stalk, spittin’ bars that talk and rock!",
            "Flow so sharp, I harp, carve my art on every chart!",
            "Mic’s my grip, I rip, flip the script with every trip!",
            "Yo, I’m the rap cyclone, I hone, takin’ the throne, I’m known!",
            "Bars so sick, I pick, kickin’ tricks that stick quick!",
            "I’m the rhyme sniper, hyper, wipin’ out cyphers like a viper!",
            "Flow like a storm, I form, transform, I’m the rap swarm!",
            "Mic’s my soul, I roll, takin’ control with bars of gold!",
            "Yo, I’m the freestyle specter, collector, perfectin’ bars that reflect ya!",
            "Bars like a blade, I raid, never fade, I’m the rap crusade!",
            "I’m the rap pulsar, I star, droppin’ bars that scar from afar!",
            "Flow so tight, I ignite, rewrite the night with every bite!",
            "Mic’s my vibe, I scribe, bars that thrive, I’m alive!",
            "Yo, I’m the rhyme bandit, I land it, bars so grand they demand it!",
            "Bars like a flood, in my blood, I’m the rap stud, no dud!",
            "I’m the freestyle phoenix, remix, spittin’ licks that fix!",
            "Flow so deep, I sweep, keepin’ beats in a lyrical leap!",
            "Mic’s my spark, in the dark, I embark, leavin’ my mark!",
            "Yo, I’m the rap inferno, eternal, burnin’ journals with my verbal!",
            "Bars so fresh, I mesh, bless the flesh with no stress!",
            "I’m the rhyme dragon, I’m braggin’, bars so tight they’re snaggin’!",
            "Flow like a jet, I set, bars you won’t forget, no regret!",
            "Mic’s my reign, I sustain, droppin’ pain with every strain!",
            "Yo, I’m the freestyle monarch, I spark, leave the dark with my mark!",
            "Bars like a wave, I rave, save the stage, I’m the brave!",
            "I’m the rap cheetah, I lead ya, bars so lethal they bleed ya!",
            "Flow so clean, I gleam, supreme, livin’ the rap dream!",
            "Mic’s my sword, I’m adored, spittin’ chords that can’t be ignored!",
            "Yo, I’m the rhyme tsunami, no baloney, bars so holy they own me!",
            "Bars so bold, I hold, unfold gold with every roll!",
            "I’m the freestyle cobra, supernova, takin’ over with bars that smolder!",
            "Flow like a breeze, I seize, pleas that tease with ease!",
            "Mic’s my flame, I claim, reframe the game with no tame!",
            "Yo, I’m the rap dynamo, I flow, bars that glow, you know!",
            "Bars like a blast, I cast, fast, surpassin’ the past!",
            "I’m the rhyme wizard, blizzard, spittin’ bars like a lyrical lizard!",
            "Flow so fierce, I pierce, steer clear, I’m the rap pioneer!",
            "Mic’s my wand, I bond, respond with bars beyond!",
            "Yo, I’m the freestyle lion, I’m tryin’, bars so fly they’re defyin’!",
            "Bars like a bomb, I’m calm, droppin’ psalms with rap aplomb!",
            "I’m the rap vortex, I flex, complex bars that perplex!",
            "Flow so raw, I draw, breakin’ every law that you saw!",
            "Mic’s my grip, I slip, flip the script with every dip!",
            "Yo, I’m the rhyme rocket, I lock it, bars from my pocket, I rock it!",
            "Bars so ill, they thrill, fill the skill with no chill!",
            "I’m the freestyle hawk, I talk, spittin’ bars that stalk and rock!",
            "Flow like a tide, I ride, pride inside, I provide!",
            "Mic’s my crown, I drown, spittin’ sound that shakes the town!",
            "Yo, I’m the rap avalanche, I branch, bars that dance and enhance!",
            "Bars like a flare, I swear, rare air, I’m everywhere!",
            "I’m the rhyme titan, I lighten, writin’ bars that tighten!",
            "Flow so sick, I pick, kickin’ quick with every lick!",
            "Mic’s my soul, I roll, takin’ control with bars that toll!",
            "Yo, I’m the freestyle phantom, I slam, bars like a lyrical jam!",
            "Bars so tight, ignite, I strike, rewrite the night!",
            "I’m the rap pulsar, I star, bars that scar from afar!",
            "Flow like a stream, supreme, I gleam, livin’ the dream!",
            "Mic’s my vibe, I scribe, bars that thrive, I’m alive!",
            "Yo, I’m the rhyme bandit, I land it, bars so grand they demand it!",
            "Bars like a flood, in my blood, I’m the rap stud, no dud!",
            "I’m the freestyle phoenix, remix, spittin’ licks that fix!",
            "Flow so deep, I sweep, keepin’ beats in a lyrical leap!",
            "Mic’s my spark, in the dark, I embark, leavin’ my mark!",
            "Yo, I’m the rap inferno, eternal, burnin’ journals with my verbal!",
            "Bars so fresh, I mesh, bless the flesh with no stress!",
            "I’m the rhyme dragon, I’m braggin’, bars so tight they’re snaggin’!",
            "Flow like a jet, I set, bars you won’t forget, no regret!",
            "Mic’s my reign, I sustain, droppin’ pain with every strain!",
            "Yo, I’m the freestyle monarch, I spark, leave the dark with my mark!",
            "Bars like a wave, I rave, save the stage, I’m the brave!",
            "I’m the rap cheetah, I lead ya, bars so lethal they bleed ya!",
            "Flow so clean, I gleam, supreme, livin’ the rap dream!",
            "Mic’s my sword, I’m adored, spittin’ chords that can’t be ignored!"
        ];

        // Page navigation
        function enterCipher() {
            document.getElementById('homepage').style.display = 'none';
            document.getElementById('cipher-room').style.display = 'block';
        }

        // Find a Friendzy logic with smoother chat simulation
        function findFriendzy() {
            const input = document.getElementById('freestyle-input').value;
            const output = document.getElementById('freestyle-output');
            const status = document.getElementById('chat-status');
            const micAnimation = document.getElementById('mic-animation');

            if (input.trim() === '') {
                output.innerHTML = '<p>Drop some bars first, fam!</p>';
                return;
            }

            // Disable button during "chat"
            const button = document.querySelector('#cipher-room button');
            button.disabled = true;

            // Smooth chat simulation
            output.innerHTML = `<p>You: "${input}"</p>`;
            status.innerText = 'Sending to Friendzy...';
            micAnimation.style.display = 'block';

            setTimeout(() => {
                status.innerText = 'Friendzy’s vibin’ on it...';
            }, 1000);

            setTimeout(() => {
                status.innerText = 'Friendzy’s spittin’ back...';
            }, 2500);

            setTimeout(() => {
                const randomFreestyle = freestylePool[Math.floor(Math.random() * freestylePool.length)];
                output.innerHTML = `<p>You: "${input}"</p><p>Friendzy: "${randomFreestyle}"</p>`;
                status.innerText = '';
                micAnimation.style.display = 'none';
                button.disabled = false;
            }, 4500); // 4.5 seconds total—smooth, not too long
        }
    </script>
</body>
</html>
