<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Surprise Button</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            margin-top: 50px;
            background-color: #f0f8ff;
        }

        #surprise-button {
            padding: 15px 30px;
            font-size: 20px;
            color: white;
            background-color: #ff4500;
            border: none;
            border-radius: 10px;
            cursor: pointer;
            transition: transform 0.2s, background-color 0.3s;
        }

        #surprise-button:hover {
            background-color: #ff6347;
            transform: scale(1.1);
        }

        /* Shake animation */
        @keyframes shake {
            0% { transform: translateX(0); }
            25% { transform: translateX(-10px); }
            50% { transform: translateX(10px); }
            75% { transform: translateX(-10px); }
            100% { transform: translateX(0); }
        }

        .shaking {
            animation: shake 0.5s ease-in-out;
        }

        #photo-gallery {
            position: fixed;
            bottom: 0;
            width: 100%;
            display: none;
            justify-content: space-between;
            align-items: center;
            gap: 20px;
            padding: 20px;
        }

        .photo {
            height: auto;
        }

        .photo:first-child {
            width: 250px;
        }

        .photo:nth-child(2) {
            width: 380px;
        }

        .photo:nth-child(3) {
            width: 450px;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-30px); }
        }

        .surprise-message {
            animation: bounce 1s ease-in-out;
            font-size: 64px;
            font-weight: 900;
            color: #FF69B4;
            text-align: center;
            margin-top: 30px;
            text-shadow: 4px 4px #FFD700;
        }

        .subtext {
            font-size: 20px;
            font-style: italic;
            color: #696969;
            margin-top: 10px;
        }

        /* Typewriter Effect */
        .typewriter {
            font-family: 'Courier New', monospace;
            white-space: nowrap;
            overflow: hidden;
            display: inline-block;
            width: 0;
            animation: typing 3s steps(30) forwards;
            text-align: center;
            margin-top: 20px;
        }

        @keyframes typing {
            from { width: 0; }
            to { width: 100%; }
        }

        /* Graduation year scroll effect */
        #scrolling-year {
            position: fixed;
            right: 10px;
            top: 20%;
            font-size: 50px;
            font-family: 'Courier New', Courier, monospace;
            color: black; /* Bold black color for the numbers */
            font-weight: bold; /* Make the numbers bold */
            z-index: 1000;
            display: none;
        }

        .scrolling {
            animation: scrollYear 10s linear infinite;
        }

        @keyframes scrollYear {
            0% { top: -30%; }
            100% { top: 100%; }
        }
    </style>
</head>
<body>
    <h1>Click the Button for a Surprise!</h1>
    <button id="surprise-button">Surprise</button>

    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <script>
        document.getElementById("surprise-button").addEventListener("click", function() {
            // Apply shake effect
            this.classList.add('shaking');

            // Remove the shake effect after animation is complete
            setTimeout(() => {
                this.classList.remove('shaking');
            }, 500);  // 500ms matches the duration of the shake animation

            // Display the first message "ALL THE BEST!" and photo
            const messageDiv = document.createElement("div");
            messageDiv.innerHTML = "🎉 ALL THE BEST! 💖";
            messageDiv.classList.add('surprise-message');
            document.body.appendChild(messageDiv);

            // Display photo at the same time
            const photoGalleryDiv = document.createElement("div");
            photoGalleryDiv.id = "photo-gallery";
            photoGalleryDiv.innerHTML = '<img src="images/photo1.png" alt="Friend Photo 1" class="photo">';
            document.body.appendChild(photoGalleryDiv);

            // Show the photo gallery immediately
            document.getElementById("photo-gallery").style.display = "flex";

            // Delay the second message and apply typewriter effect
            setTimeout(function() {
                const subtextDiv = document.createElement("div");
                subtextDiv.innerHTML = "for your final exam of the semester";
                subtextDiv.classList.add('subtext', 'typewriter'); // Add typewriter effect
                document.body.appendChild(subtextDiv);
            }, 1500); // 1.5 seconds after the first message

            // Confetti Effect
            confetti({
                particleCount: 100,
                spread: 70,
                origin: { y: 0.6 }
            });

            // Add scrolling graduation year effect
            const scrollingYear = document.createElement("div");
            scrollingYear.innerHTML = `2<br>0<br>2<br>1<br>~<br>2<br>0<br>2<br>5`;
            scrollingYear.id = "scrolling-year";
            scrollingYear.classList.add('scrolling');  // Apply scroll effect
            document.body.appendChild(scrollingYear);

            // Show the scrolling year after clicking the button
            document.getElementById("scrolling-year").style.display = "block";
        });
    </script>
</body>
</html>
