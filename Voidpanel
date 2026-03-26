<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Void Hub Control Panel</title>
<style>
    body {
        background: linear-gradient(135deg, #0a0a15 0%, #05050a 50%, #0a0a15 100%);
        color: #fff;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        margin: 0;
        overflow: hidden;
    }
    
    body::before {
        content: '';
        position: absolute;
        width: 200%;
        height: 200%;
        background: repeating-linear-gradient(
            0deg,
            transparent,
            transparent 2px,
            rgba(0, 170, 255, 0.03) 2px,
            rgba(0, 170, 255, 0.03) 4px
        );
        animation: scan 8s linear infinite;
        pointer-events: none;
    }
    
    @keyframes scan {
        0% { transform: translateY(0); }
        100% { transform: translateY(50px); }
    }
    
    #panel {
        background: rgba(16, 16, 32, 0.9);
        padding: 40px;
        border-radius: 20px;
        border: 1px solid rgba(0, 170, 255, 0.3);
        box-shadow: 
            0 0 30px rgba(0, 170, 255, 0.3),
            inset 0 0 20px rgba(0, 170, 255, 0.05);
        width: 380px;
        text-align: center;
        position: relative;
        backdrop-filter: blur(10px);
        animation: pulse 4s ease-in-out infinite;
    }
    
    @keyframes pulse {
        0%, 100% { box-shadow: 0 0 30px rgba(0, 170, 255, 0.3), inset 0 0 20px rgba(0, 170, 255, 0.05); }
        50% { box-shadow: 0 0 50px rgba(0, 170, 255, 0.5), inset 0 0 30px rgba(0, 170, 255, 0.1); }
    }
    
    h1 {
        font-size: 26px;
        margin-bottom: 25px;
        color: #00aaff;
        text-transform: uppercase;
        letter-spacing: 3px;
        text-shadow: 0 0 10px rgba(0, 170, 255, 0.5);
    }
    
    input[type="password"] {
        width: 85%;
        padding: 12px;
        margin-bottom: 25px;
        border-radius: 10px;
        border: 2px solid rgba(0, 170, 255, 0.3);
        background: rgba(5, 5, 10, 0.8);
        color: #00aaff;
        font-size: 16px;
        text-align: center;
        outline: none;
        transition: all 0.3s;
    }
    
    input[type="password"]:focus {
        border-color: #00aaff;
        box-shadow: 0 0 15px rgba(0, 170, 255, 0.4);
    }
    
    .button-group {
        display: flex;
        gap: 15px;
        justify-content: center;
    }
    
    button {
        padding: 12px 30px;
        font-size: 16px;
        border: none;
        border-radius: 10px;
        cursor: pointer;
        transition: all 0.3s;
        font-weight: bold;
        text-transform: uppercase;
        letter-spacing: 1px;
        position: relative;
        overflow: hidden;
    }
    
    button::before {
        content: '';
        position: absolute;
        top: 50%;
        left: 50%;
        width: 0;
        height: 0;
        border-radius: 50%;
        background: rgba(255, 255, 255, 0.3);
        transform: translate(-50%, -50%);
        transition: width 0.6s, height 0.6s;
    }
    
    button:active::before {
        width: 300px;
        height: 300px;
    }
    
    #onBtn {
        background: linear-gradient(135deg, #00aa00, #00ff33);
        color: #000;
        box-shadow: 0 4px 15px rgba(0, 255, 51, 0.3);
    }
    
    #onBtn:hover {
        transform: translateY(-2px);
        box-shadow: 0 6px 20px rgba(0, 255, 51, 0.5);
    }

    #offBtn {
        background: linear-gradient(135deg, #aa0000, #ff3333);
        color: #fff;
        box-shadow: 0 4px 15px rgba(255, 51, 51, 0.3);
    }
    
    #offBtn:hover {
        transform: translateY(-2px);
        box-shadow: 0 6px 20px rgba(255, 51, 51, 0.5);
    }

    #status {
        margin-top: 25px;
        font-weight: bold;
        font-size: 18px;
        padding: 15px;
        border-radius: 10px;
        background: rgba(0, 0, 0, 0.3);
        min-height: 20px;
        display: flex;
        align-items: center;
        justify-content: center;
        gap: 10px;
        transition: all 0.3s;
    }
    
    .status-enabled {
        color: #00ff00;
        text-shadow: 0 0 10px rgba(0, 255, 0, 0.5);
        border: 1px solid rgba(0, 255, 0, 0.3);
    }
    
    .status-disabled {
        color: #ff0000;
        text-shadow: 0 0 10px rgba(255, 0, 0, 0.5);
        border: 1px solid rgba(255, 0, 0, 0.3);
    }
    
    .status-waiting {
        color: #00aaff;
        border: 1px solid rgba(0, 170, 255, 0.3);
    }
</style>
</head>
<body>

<div id="panel">
    <h1>⚡ Void Hub Control Panel ⚡</h1>
    <input type="password" id="password" placeholder="Enter Password">
    <br>
    <div class="button-group">
        <button id="onBtn">Turn ON</button>
        <button id="offBtn">Turn OFF</button>
    </div>
    <div id="status" class="status-waiting">Awaiting Authentication...</div>
</div>

<script>
    const correctPassword = "102711";
    let scriptEnabled = false;

    const status = document.getElementById("status");
    const passwordInput = document.getElementById("password");

    document.getElementById("onBtn").addEventListener("click", () => {
        if(passwordInput.value === correctPassword){
            scriptEnabled = true;
            status.innerHTML = "Script is ENABLED <span style='font-size:20px'>✅</span>";
            status.className = "status-enabled";
            passwordInput.value = '';
        } else {
            shakePanel();
            alert("🚫 Access Denied: Incorrect password!");
        }
    });

    document.getElementById("offBtn").addEventListener("click", () => {
        if(passwordInput.value === correctPassword){
            scriptEnabled = false;
            status.innerHTML = "Script is DISABLED <span style='font-size:20px'>❌</span>";
            status.className = "status-disabled";
            passwordInput.value = '';
        } else {
            shakePanel();
            alert("🚫 Access Denied: Incorrect password!");
        }
    });

    function shakePanel() {
        const panel = document.getElementById('panel');
        panel.style.animation = 'none';
        setTimeout(() => {
            panel.style.animation = 'shake 0.5s';
        }, 10);
    }

    if(localStorage.getItem("voidHubEnabled") === "true") {
        scriptEnabled = true;
        status.innerHTML = "Script is ENABLED <span style='font-size:20px'>✅</span>";
        status.className = "status-enabled";
    }

    window.addEventListener("beforeunload", () => {
        localStorage.setItem("voidHubEnabled", scriptEnabled);
    });
</script>

<style>
@keyframes shake {
    0%, 100% { transform: translateX(0); }
    25% { transform: translateX(-10px); }
    75% { transform: translateX(10px); }
}
</style>

</body>
</html>
