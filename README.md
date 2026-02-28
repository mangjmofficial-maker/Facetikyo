# Facetikyo
Video downloader 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Universal Video Downloader</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css">
    <style>
        body.dark { background: #0f172a; color: white; }
        .glass {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        .gradient-bg {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
        }
    </style>
</head>
<body class="gradient-bg min-h-screen flex items-center justify-center p-4 transition-colors duration-300">
    
    <div class="max-w-2xl w-full glass rounded-3xl p-8 shadow-2xl text-center">
        <div class="flex justify-between items-center mb-8">
            <h1 class="text-3xl font-bold text-white">StreamFetch</h1>
            <button id="themeToggle" class="p-2 bg-white/20 rounded-full hover:bg-white/40 transition">
                <i class="fas fa-moon text-white"></i>
            </button>
        </div>

        <p class="text-white/80 mb-6">Paste your link below to download from YT, TikTok, or IG.</p>

        <div class="relative mb-6">
            <input type="text" id="videoUrl" placeholder="https://www.youtube.com/watch?v=..." 
                   class="w-full p-4 rounded-xl bg-white/10 border border-white/20 text-white placeholder-white/50 focus:outline-none focus:ring-2 focus:ring-purple-400">
            <button onclick="fetchVideoData()" class="mt-4 w-full bg-purple-600 hover:bg-purple-500 text-white font-bold py-3 rounded-xl transition-all transform hover:scale-[1.02] active:scale-95">
                Fetch Video
            </button>
        </div>

        <div id="progressContainer" class="hidden mb-6">
            <div class="w-full bg-white/20 rounded-full h-2.5">
                <div id="progressBar" class="bg-purple-400 h-2.5 rounded-full transition-all duration-500" style="width: 0%"></div>
            </div>
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
