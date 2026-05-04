<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Link Redirector</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            background: linear-gradient(135deg, #1e1e2f, #3a3a6a);
            color: white;
            text-align: center;
            padding: 50px;
        }

        .box {
            background: rgba(255,255,255,0.1);
            padding: 30px;
            border-radius: 15px;
            display: inline-block;
        }

        input {
            padding: 10px;
            width: 250px;
            border: none;
            border-radius: 5px;
            margin-bottom: 10px;
        }

        button {
            padding: 10px 20px;
            background: #00c3ff;
            border: none;
            border-radius: 5px;
            color: black;
            cursor: pointer;
            font-weight: bold;
        }

        button:hover {
            background: #00a2d6;
        }
    </style>
</head>
<body>

    <div class="box">
        <h1>🔗 Link Redirector</h1>
        <p>Paste a link below:</p>

        <input type="text" id="linkInput" placeholder="https://example.com">
        <br>
        <button onclick="goToLink()">Go</button>
    </div>

    <script>
        function goToLink() {
            let link = document.getElementById("linkInput").value.trim();

            if (!link) {
                alert("Please enter a link!");
                return;
            }

            // Auto add https if missing
            if (!link.startsWith("http://") && !link.startsWith("https://")) {
                link = "https://" + link;
            }

            // Redirect
            window.location.href = link;
        }
    </script>

</body>
</html>            </div>
            <p id="statusMsg" class="text-xs text-white/70 mt-2 italic">Processing...</p>
        </div>

        <div id="previewCard" class="hidden animate-fade-in bg-white/5 p-4 rounded-2xl border border-white/10">
            <img id="thumb" src="" class="w-full rounded-lg mb-4 shadow-lg">
            <h3 id="videoTitle" class="text-white font-semibold mb-4 truncate">Video Title</h3>
            
            <select id="quality" class="w-full p-2 mb-4 rounded bg-slate-800 text-white border-none">
                <option value="1080">1080p (HD)</option>
                <option value="720">720p</option>
                <option value="360">360p</option>
            </select>
            
            <button onclick="startDownload()" class="w-full bg-green-500 hover:bg-green-400 text-white font-bold py-2 rounded-lg transition">
                Download Now
            </button>
        </div>
    </div>

    <script src="app.js"></script>
</body>
</html>
