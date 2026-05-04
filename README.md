<html>
<head>
<meta charset="UTF-8">
<title>My Aircraft Site</title>

<style>
body {
    margin: 0;
    font-family: Arial;
    background: linear-gradient(to bottom, #4db8ff, #ffffff);
    text-align: center;
    color: #000;
}

header {
    padding: 40px;
    font-size: 40px;
    font-weight: bold;
}

button {
    padding: 15px 25px;
    font-size: 18px;
    margin: 10px;
    border: none;
    border-radius: 10px;
    cursor: pointer;
    background: #007bff;
    color: white;
}

button:hover {
    background: #0056b3;
}

.container {
    margin-top: 50px;
}

.card {
    background: white;
    display: inline-block;
    padding: 20px;
    margin: 10px;
    border-radius: 15px;
    width: 250px;
    box-shadow: 0px 5px 15px rgba(0,0,0,0.2);
    transition: 0.3s;
}

.card:hover {
    transform: scale(1.05);
}
</style>
</head>

<body>

<header>✈️ Aircraft Game Website</header>

<div class="container">

<div class="card">
<h2>Play Game</h2>
<p>Tap to fly and dodge obstacles!</p>
<button onclick="alert('Put your game link here')">Play</button>
</div>

<div class="card">
<h2>Shop</h2>
<p>Buy aircraft with special abilities</p>
<button onclick="alert('Shop coming soon')">Open</button>
</div>

<div class="card">
<h2>Download</h2>
<p>Get the full version</p>
<button onclick="alert('Download link here')">Download</button>
</div>

</div>

</body>
</html>
