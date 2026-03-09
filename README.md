<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8">
<title>Daily Check-in</title>

<style>
body{
    font-family: Arial;
    background:#f2f2f2;
    text-align:center;
    padding:40px;
}

.box{
    background:white;
    width:320px;
    margin:auto;
    padding:30px;
    border-radius:10px;
    box-shadow:0 5px 15px rgba(0,0,0,0.1);
}

button{
    padding:12px 25px;
    font-size:16px;
    background:#1877f2;
    color:white;
    border:none;
    border-radius:6px;
    cursor:pointer;
}

button:disabled{
    background:gray;
}
</style>

</head>

<body>

<div class="box">

<h2>🔥 Daily Check-in</h2>

<p>Streak hiện tại:</p>
<h1 id="streak">0</h1>

<button id="checkinBtn">CHECK-IN</button>

<p id="status"></p>

</div>

<script>

let streak = localStorage.getItem("streak") || 0
let lastCheck = localStorage.getItem("lastCheck")

document.getElementById("streak").innerText = streak

let now = new Date()
let today = now.toDateString()

if(lastCheck === today){
    document.getElementById("checkinBtn").disabled = true
    document.getElementById("status").innerText = "Bạn đã check-in hôm nay"
}

document.getElementById("checkinBtn").onclick = function(){

    let last = new Date(lastCheck)
    let diff = (now - last) / (1000*60*60*24)

    if(diff <= 2){
        streak++
    }else{
        streak = 1
    }

    localStorage.setItem("streak", streak)
    localStorage.setItem("lastCheck", today)

    document.getElementById("streak").innerText = streak
    document.getElementById("status").innerText = "Check-in thành công 🔥"
    this.disabled = true
}

</script>

</body>
</html>
