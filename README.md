<!DOCTYPE html><html lang="gu">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Animated Welcome Page</title>
    <style>
        body {
            margin: 0;
            padding: 0;
            background-color: black;
            color: white;
            text-align: center;
            overflow: hidden;
        }
        .welcome {
            font-size: 50px;
            color: red;
            animation: fadeIn 3s ease-in-out;
        }
        .signature {
            position: absolute;
            bottom: 10px;
            right: 10px;
            font-size: 14px;
        }
        .swans {
            position: absolute;
            bottom: 50px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            align-items: center;
        }
        .next-button {
            background: white;
            border: none;
            padding: 10px 20px;
            font-size: 18px;
            cursor: pointer;
            border-radius: 5px;
        }
        .angels {
            display: none;
            font-size: 30px;
            margin-top: 100px;
        }
        .wallpapers {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 10px;
            margin-top: 20px;
        }
        .wallpaper {
            width: 200px;
            height: 100px;
            background: linear-gradient(45deg, #ff0000, #000000);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 20px;
            font-weight: bold;
        }
        .download-button {
            margin-top: 10px;
            padding: 10px;
            background: white;
            color: black;
            border: none;
            cursor: pointer;
            border-radius: 5px;
        }
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
    </style>
</head>
<body>
    <div class="welcome">WELCOME</div>
    <div class="swans">
        <img src="swan.png" width="50">
        <button class="next-button" onclick="enterPage()">Next</button>
        <img src="swan.png" width="50">
    </div>
    <div class="signature">DATT PANDYA</div>
    <div id="secondPage" class="angels">
        👼✨ ENTER YOUR NAME 🤩<br>
        <input type="text" id="username" placeholder="Enter your name" oninput="generateWallpapers()">
        <div id="wallpapers" class="wallpapers"></div>
    </div>
    <script>
        function enterPage() {
            document.body.innerHTML = document.getElementById("secondPage").outerHTML;
            document.getElementById("secondPage").style.display = "block";
        }
        function generateWallpapers() {
            let name = document.getElementById("username").value;
            let container = document.getElementById("wallpapers");
            container.innerHTML = "";
            if (name) {
                for (let i = 0; i < 5; i++) {
                    let wallpaper = document.createElement("div");
                    wallpaper.className = "wallpaper";
                    wallpaper.textContent = name;
                    let downloadBtn = document.createElement("button");
                    downloadBtn.className = "download-button";
                    downloadBtn.textContent = "Download";
                    downloadBtn.onclick = () => downloadWallpaper(name, i);
                    container.appendChild(wallpaper);
                    container.appendChild(downloadBtn);
                }
            }
        }
        function downloadWallpaper(name, index) {
            let canvas = document.createElement("canvas");
            canvas.width = 800;
            canvas.height = 400;
            let ctx = canvas.getContext("2d");
            let gradient = ctx.createLinearGradient(0, 0, canvas.width, canvas.height);
            gradient.addColorStop(0, "#ff0000");
            gradient.addColorStop(1, "#000000");
            ctx.fillStyle = gradient;
            ctx.fillRect(0, 0, canvas.width, canvas.height);
            ctx.fillStyle = "white";
            ctx.font = "50px Arial";
            ctx.textAlign = "center";
            ctx.fillText(name, canvas.width / 2, canvas.height / 2);
            let link = document.createElement("a");
            link.download = `wallpaper_${index}.png`;
            link.href = canvas.toDataURL();
            link.click();
        }
    </script>
</body>
</html>
