<!DOCTYPE html>

<html>
<head>
<meta charset="utf-8"/>
<title>A.I. Musikquiz</title>
<link href="https://fonts.googleapis.com/css2?family=Anonymous+Pro&family=Indie+Flower&family=Playpen+Sans:wght@100;200&family=Roboto:wght@100&family=Silkscreen&display=swap" rel="stylesheet"> 
<style>
        body {
                font-family: Arial, sans-serif;
                background-color: #2a2a2a; /* Dark gray background */
                padding: 10px;
        }

        #game {
            max-width: 600px;
            margin: auto;
            background-color: transparent;
            padding: 20px;
            border-radius: 5px;
            box-shadow: 0px 0px 10px 0px rgba(0,0,0,0.1);
        }

        #songImage {
            max-width: 100%;
            height: auto;
        }

        #introPage {
            text-align: center;
        }

        #songName {
            font-size: 24px;
            font-weight: bold;
            margin-top: 20px;
        }

        button {
            background-color: #00fffb;
            color: #201b1b;
            border: none;
            padding: 10px 20px;
            text-align: center;
            text-decoration: none;
            display: inline-block;
            font-size: 16px;
            margin: 20px 2px;
            cursor: pointer;
            border-radius: 5px;
        }

        button:hover {
            background-color: #028582;
        }
    
#songYear {
    font-size: 18px;
    font-weight: bold;
    margin-top: 10px;
}</style>
</head>
<body>
<canvas id="background-canvas" style="position:fixed;z-index:-1;"></canvas>
<div style="text-align: center;">
<h1 style="font-family: 'Silkscreen', sans-serif; color: #00fffb;">A.I. Musikquiz: 2000's</h1>
</div>
<div id="introPage">
<img src="https://cdn.midjourney.com/0a555ad5-79e5-42db-8153-33f1b6587054/0_0.webp" alt="Image Description" width="500" height="500">
<p style="font-family: Arial, sans-serif; color: #00fffb; padding-top: 70px;">Antal billeder: 11</p>

<button id="startButton">Start quizzen</button>
</div>
<div id="game">
<img id="songImage" src=""/>
<div id="songName" style="display: none;"></div>
<div id="spotifyPlayer"></div>
<button id="revealButton" style="display: none;">Se svaret</button>
<button id="nextButton" style="display: none;">Næste billede</button>
</div>
<div id="introPage">
<p style="font-family: 'Lumanosimo', cursive; color: #717171; font-size: 10px;">Github @TeisLebeck</p>
</div>
<script>
        const canvas = document.getElementById('background-canvas');
        const ctx = canvas.getContext('2d');
        let particlesArray;
    
        // get size of window
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
    
        class Particle {
        constructor(x, y, size, speed) {
            this.x = x;
            this.y = y;
            this.size = size;
            this.speed = speed;
        }

        // method to draw individual particle
        draw() {
            ctx.fillStyle = 'rgba(173, 216, 230, 0.8)';
            ctx.beginPath();
            ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
            ctx.closePath();
            ctx.fill();
        }

        // update particle movement
        update() {
            this.x += this.speed;
            if (this.x > canvas.width) {
                this.x = 0 - this.size;
                this.y = Math.random() * canvas.height;
            }
            this.draw();
        }
    }

    // create particle array
    function init() {
        particlesArray = [];
        let numberOfParticles = (canvas.height * canvas.width) / 30000;
        for (let i = 0; i < numberOfParticles; i++) {
            let size = Math.random() * 5 + 1;
            let x = Math.random() * canvas.width;
            let y = Math.random() * canvas.height;
            let speed = Math.random() * 3 + 1;
            particlesArray.push(new Particle(x, y, size, speed));
        }
    }

    // animate particles
    function animateParticles() {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
        for (let i = 0; i < particlesArray.length; i++) {
            particlesArray[i].update();
        }
        requestAnimationFrame(animateParticles);
    }

    // reinitialize canvas on window resize
    window.addEventListener('resize', function () {
        canvas.width = window.innerWidth;
        canvas.height = window.innerHeight;
        init();
    });

    // call init() and animateParticles() to start the animation
    init();
    animateParticles();
    </script>
<script>
        function shuffleArray(array) {
    for (let i = array.length - 1; i > 0; i--) {
        let j = Math.floor(Math.random() * (i + 1));
        [array[i], array[j]] = [array[j], array[i]];
    }
}
        var songs = [
            {name: 'Placeholder', image: '', spotifyId: ''},
            //{name: 'Himmelhunden', image: 'https://cdn.discordapp.com/attachments/1059412006073016340/1094558129934569482/johnny_can_you_take_dogs_to_heaven_6d3e486c-aa87-45c8-874f-88acb802618f.png', spotifyId: '4o9FXLyDxILghCSs0b75uG'},
            //{name: 'STOR MAND', image: 'https://media.discordapp.net/attachments/1059412006073016340/1141422679468032171/roll_the_allardyce_a_single_really_big_and_tall_man_just_one_ma_7b29d3b6-9414-4605-a276-1957020ce5d1.png', spotifyId: '0BGEImCBesJKIm5kZ0fOkH'},
            //{name: 'Starboy', image: 'https://cdn.discordapp.com/attachments/1059412006073016340/1094640527934246942/johnny_a_boy_surrounded_by_stars_9dde436c-d4a0-4f50-aa9d-2da9067a8ec7.png', spotifyId: '7MXVkk9YMctZqd1Srtv4MB'},
            //{name: 'Timber', image: 'https://cdn.discordapp.com/attachments/1059412006073016340/1094636520729747617/johnny_a_man_cutting_down_tall_tree_timber_b2a657eb-8318-4e39-b8ed-6714d58e45da.png', spotifyId: '3cHyrEgdyYRjgJKSOiOtcS'},
            {name: 'Toxic', image: 'https://cdn.midjourney.com/09cbbf4c-0508-48c6-958e-7c250d884822/0_2.webp', spotifyId: '6I9VzXrHxO9rA9A5euc8Ak'},
            {name: 'Push the button', image: 'https://cdn.midjourney.com/0c62a7e3-d5ae-4cdb-8ecf-5a4e8767c08c/0_0.webp', spotifyId: '2nCmCt4B5vkabS0zeOuc1Z'},
            {name: 'Fireflies', image: 'https://cdn.midjourney.com/c9a92182-c994-4e01-a6fc-14d3fe4226a6/0_0.webp', spotifyId: '3DamFFqW32WihKkTVlwTYQ'},
            //{name: '99 luftballons', image: 'https://cdn.discordapp.com/attachments/1059412006073016340/1094557732591382588/johnny_99_air_balloons_18ed626b-2185-4afd-a5b9-bb00a80c06e3.png', spotifyId: '4ZhPLoMzZwewHLLjV1J15c'},
            {name: 'Murder on the dancefloor', image: 'https://cdn.discordapp.com/attachments/1059412006073016340/1094597289315680286/johnny_crime_scene_at_a_dance_floot_police_tape_disco_ball_42b5c8e2-4733-4f8a-9903-6a6b1736f23f.png', spotifyId: '2Za2mUwmQoSxWPscaY2vxl'},
            //{name: 'Radioactive', image: 'https://cdn.discordapp.com/attachments/1059412006073016340/1094628332697550919/johnny_radioactivity_nuclear_fa71a0a6-d4ba-48e5-9530-0c645191acc6.png', spotifyId: '62yJjFtgkhUrXktIoSjgP2'},
            //{name: "God's plan", image: 'https://cdn.discordapp.com/attachments/1059412006073016340/1094629713462435870/johnny_god_drawing_on_a_whiteboard_long_white_beard_making_a_pl_01ef087f-c470-40d9-8372-73185b4b39fe.png', spotifyId: '6DCZcSspjsKoFjzjrWoCdn'},
            {name: 'She wolf', image: 'https://cdn.discordapp.com/attachments/1059412006073016340/1094634805171343440/johnny_a_wolf_in_a_red_dress_female_5b1db91c-ce5a-454a-b280-a4599d63b7ef.png', spotifyId: '4cS2HQ6jK80vqdY9ofpztx'},
            //{name: 'Cake by the ocean', image: 'https://cdn.discordapp.com/attachments/1059412006073016340/1094638999638921216/johnny_a_birthday_cake_on_the_beach_51045487-bdee-4ba6-99a4-0af75bdd85bb.png', spotifyId: '76hfruVvmfQbw0eYn1nmeC'},
            //{name: 'Panda', image: 'https://cdn.discordapp.com/attachments/1059412006073016340/1094638702594097303/johnny_a_hip_hop_panda_1e3b9a4f-46f9-4729-a91a-298581843926.png', spotifyId: '275a9yzwGB6ncAW4SxY7q3'},
            {name: 'Single ladies', image: 'https://cdn.discordapp.com/attachments/1059412006073016340/1094641837253349396/johnny_putting_a_ring_on_a_finger_786f3285-8f56-4ac5-99ec-309b4f28e4c0.png', spotifyId: '5R9a4t5t5O0IsznsrKPVro'},
            {name: 'Temperature', image: 'https://cdn.discordapp.com/attachments/1059412006073016340/1094643132940959865/johnny_thermometer_ff8dd3c3-23bd-40e1-afff-53eb49df8318.png', spotifyId: '0k2GOhqsrxDTAbFFSdNJjT'},
            {name: 'Right round', image: 'https://cdn.discordapp.com/attachments/1059412006073016340/1094643503801319595/johnny_head_spinning_round_e7fd5fdd-c213-4cda-91ca-d42c9810520b.png', spotifyId: '3GpbwCm3YxiWDvy29Uo3vP'},
            //{name: 'Girl on fire', image: 'https://cdn.discordapp.com/attachments/1059412006073016340/1094634246808797234/johnny_a_women_standing_among_flames_51607835-0516-49d9-af44-2e3d2d936dd2.png', spotifyId: '4esOae7i4rqTbAu9o5Pxco'},
            //{name: 'International love', image: 'https://cdn.discordapp.com/attachments/1059412006073016340/1094644581557092383/johnny_planet_earth_surrounded_by_hearts_8dfe2fd7-3e31-4ae1-9138-248aafb5ba02.png', spotifyId: '62zFEHfAYl5kdHYOivj4BC'},
            {name: 'Elskovspony', image: 'https://cdn.discordapp.com/attachments/1059412006073016340/1095814030939148409/johnny_a_pony_or_small_horse_surrounded_by_hearts_5da1a487-ce5d-4b3c-ab3b-c7faa212b375.png', spotifyId: '0gloEpnKRspgRbp5jI7Bbd'},
            //{name: 'Bumpy ride', image: 'https://cdn.discordapp.com/attachments/1059412006073016340/1095817647330955274/johnny_a_car_riding_over_bumpy_hills_bouncing_bd3f44a1-a243-4a48-932b-4296992ecc5b.png', spotifyId: '71R6zJsrF3ffc3TBFHfivX'},
            //{name: 'Take me home, country roads', image: 'https://cdn.midjourney.com/cb57da70-9421-4cef-978a-82500a62771a/0_3.png', spotifyId: '1QbOvACeYanja5pbnJbAmk'},
            {name: 'Sk8er boi', image: 'https://cdn.midjourney.com/4caaf808-0b8a-4b02-9ecf-4c8be45423a4/0_0.png', spotifyId: '00Mb3DuaIH1kjrwOku9CGU'},
            //{name: 'Galway girl', image: 'https://cdn.midjourney.com/52ca5e96-a430-4c03-8aa2-cd2cf678e596/0_1.png', spotifyId: '0afhq8XCExXpqazXczTSve'},
            //{name: 'Enter sandman', image: 'https://cdn.midjourney.com/ee41cfad-3fa6-4eee-aae2-de5c1d2269be/0_0.png', spotifyId: '5sICkBXVmaCQk5aISGR3x1'},
            //{name: 'Champagne supernova', image: 'https://cdn.midjourney.com/3be2d870-4296-4fb2-bd36-b1938a2f2d52/0_2.png', spotifyId: '6EMynpZ10GVcwVqiLZj6Ye'},
            {name: 'Cry me river', image: 'https://cdn.midjourney.com/9ad6f26f-864e-4f52-bcbe-68edbb2d1597/0_0.png', spotifyId: '7Lf7oSEVdzZqTA0kEDSlS5'},
            //{name: 'Rocket man', image: 'https://cdn.midjourney.com/75e83f94-350b-4309-8077-8c42256f3166/0_1.png', spotifyId: '3gdewACMIVMEWVbyb8O9sY'},
            //{name: 'American pie', image: 'https://cdn.midjourney.com/9036c34d-2ac3-4149-b723-4186f832eb63/0_1.png', spotifyId: '1fDsrQ23eTAVFElUMaf38X'},
            //{name: 'Ice ice baby', image: 'https://cdn.midjourney.com/17b0381f-4392-4c9f-8bcd-f6098e5ba8fd/0_0.png', spotifyId: '11d9oUiwHuYt216EFA2tiz'}

            
        ];

                var currentSong = 0;

        function revealAnswer() {
            document.getElementById('songName').innerTextz = songs[currentSong].name;
            document.getElementById('songName').style.display = 'block';
            document.getElementById('revealButton').style.display = 'none';
            document.getElementById('nextButton').style.display = 'block';
            
            var spotifyEmbed = '<iframe src="https://open.spotify.com/embed/track/' + songs[currentSong].spotifyId + '" width="300" height="80" frameborder="0" allowtransparency="true" allow="encrypted-media"></iframe>';
            document.getElementById('spotifyPlayer').innerHTML = spotifyEmbed;
        }

        function nextSong() {
            currentSong++;
            if (currentSong < songs.length) {
                document.getElementById('songImage').src = songs[currentSong].image;
                document.getElementById('songName').style.display = 'none';
                document.getElementById('spotifyPlayer').innerHTML = '';
                document.getElementById('revealButton').style.display = 'block';
                document.getElementById('nextButton').style.display = 'none';
            } else {
                document.getElementById('game').innerHTML = 'Så er der sgu ikke flere billeder. Genindlæs siden for at starte forfra.';
            }
        }

        document.getElementById('revealButton').onclick = revealAnswer;
        document.getElementById('nextButton').onclick = nextSong;
    </script>
<script>
        document.getElementById('startButton').onclick = function() {
        document.getElementById('introPage').style.display = 'none';
        document.getElementById('game').style.display = 'block';
        document.getElementById('songImage').src = songs[currentSong].image;
        document.getElementById('revealButton').style.display = 'block';
        nextSong();
        };
    </script>
</body>
</html>
