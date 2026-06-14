<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DebtWatcher Pro</title>
    
    <link rel="manifest" href='data:application/manifest+json,{"name":"DebtWatcher Pro","short_name":"DebtWatcher","start_url":".","display":"standalone","background_color":"#121212","theme_color":"#3b82f6","orientation":"portrait","icons":[{"src":"https://cdn-icons-png.flaticon.com/512/2652/2652230.png","sizes":"512x512","type":"image/png"}]}'>
    <meta name="theme-color" content="#3b82f6">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent"> 

    <style>
        :root { 
            --main-font: 16px; --name-font: 18px; --price-font: 20px;
            --bg-body: #f4f7f9; --bg-card: #ffffff; --text-color: #333; 
            --primary: #3b82f6; --header-bg: linear-gradient(135deg, #000044 0%, #000088 100%);
            --border-color: #3b82f6; 
            --border-width: 2px;
        }
        .dark-theme {
            --bg-body: #121212; --bg-card: #1e1e1e; --text-color: #e0e0e0;
            --primary: #378eff; --header-bg: #252525;
            --border-color: #378eff;
        }
        .green-theme {
            --bg-body: #f0f4f0; --bg-card: #ffffff; --text-color: #2e4a2e;
            --primary: #28a745; --header-bg: linear-gradient(135deg, #1b5e20 0%, #2e7d32 100%);
            --border-color: #28a745;
        }
        body { font-family: 'Segoe UI', sans-serif; background: var(--bg-body); padding: 15px; color: var(--text-color); font-size: var(--main-font); transition: 0.3s; margin: 0; }
        .container { max-width: 500px; margin: auto; background: var(--bg-card); padding: 25px; border-radius: 20px; box-shadow: 0 10px 25px rgba(0,0,0,0.1); }
        .settings-bar { background: rgba(0,0,0,0.05); padding: 10px; border-radius: 12px; margin-bottom: 20px; text-align: center; }
        .settings-bar div { margin: 5px 0; font-size: 11px; font-weight: bold; text-transform: uppercase; color: #777; }
        .btn-group { display: flex; justify-content: center; gap: 8px; margin-bottom: 10px; }
        .btn-group button { border: 1px solid #ccc; padding: 5px 10px; border-radius: 5px; cursor: pointer; font-size: 12px; background: #fff; }
        .btn-group button.active { background: #333; color: #fff; border-color: #333; }
        h2 { text-align: center; color: var(--primary); margin-bottom: 15px; font-weight: 800; }
        input { width: 100%; padding: 12px; margin: 10px 0; border: 1px solid #ddd; border-radius: 10px; box-sizing: border-box; font-size: inherit; background: var(--bg-card); color: var(--text-color); }
        
        /* TIIRKA BULUUGGA AH EE REGISTRATION-KA */
        .blue-reg-column {
            background: linear-gradient(135deg, #0044cc 0%, #002288 100%);
            padding: 20px;
            border-radius: 16px;
            margin-bottom: 20px;
            box-shadow: 0 6px 15px rgba(0, 34, 136, 0.3);
            display: flex;
            flex-direction: column;
            gap: 2px;
        }
        .blue-reg-column label {
            color: #ffffff !important;
            font-weight: bold;
            font-size: 14px;
            margin-top: 6px;
            text-shadow: 0 1px 2px rgba(0,0,0,0.3);
            letter-spacing: 0.5px;
        }
        .blue-reg-column input {
            background: #ffffff !important;
            color: #002288 !important;
            border: 2px solid #58a6ff;
            font-weight: 600;
            margin: 4px 0 10px 0;
            font-size: 15px;
        }
        .blue-reg-column input::placeholder {
            color: #88aadd;
        }
        .btn-add-blue {
            width: 100%;
            padding: 14px;
            background: #00cc66;
            color: #ffffff;
            border: none;
            border-radius: 10px;
            font-weight: 800;
            cursor: pointer;
            font-size: 17px;
            text-transform: uppercase;
            margin-top: 10px;
            box-shadow: 0 4px 10px rgba(0, 204, 102, 0.4);
            transition: 0.2s;
        }
        .btn-add-blue:hover {
            background: #00ee77;
            transform: scale(1.01);
        }

        .total-box { background: var(--header-bg); color: #fff; padding: 20px; border-radius: 15px; text-align: center; margin: 15px 0; font-size: 1.5em; font-weight: bold; }
        .sheet-table { width: 100%; border-collapse: collapse; margin-top: 15px; background: var(--bg-card); font-size: var(--main-font); }
        .sheet-table th, .sheet-table td { border: var(--border-width) solid var(--border-color); padding: 12px 10px; text-align: left; vertical-align: middle; }
        .sheet-table th { background-color: rgba(0,123,255,0.1); font-weight: bold; text-transform: uppercase; font-size: 12px; color: var(--primary); }
        .sheet-row:nth-child(even) { background-color: rgba(0,123,255,0.02); }
        .money-actions { display: flex; gap: 4px; }
        .btn-plus, .btn-minus { padding: 6px 10px; border-radius: 5px; font-weight: bold; cursor: pointer; font-size: 12px; border: none; }
        .btn-plus { background: #e8f5e9; color: #2e7d32; }
        .btn-minus { background: #fff8e1; color: #f57f17; }
        .btn-history { background: #f8f9fa; padding: 6px; border-radius: 5px; cursor: pointer; font-size: 12px; border: 1px solid #ddd; color: #333; width: 100%; }
        .history-content { display: none; padding: 10px; border-radius: 8px; margin-top: 8px; border: 1px dashed #ccc; font-size: 12px; background: rgba(0,0,0,0.02); color: var(--text-color); }
        .history-item { padding: 5px 0; border-bottom: 1px solid var(--border-color); display: flex; justify-content: space-between; }
        
        /* Tirtirista dhex taal menu-ga qarsoon */
        .btn-delete { background: #ff4d4d; color: #fff; border: none; padding: 5px; width: 100%; border-radius: 4px; font-weight: bold; margin-top: 10px; cursor: pointer; font-size: 11px; }
        
        /* LOCK SCREEN (KIRADA BIL LAHA AH - $4) */
        .lock-screen { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background-color: #1a1a1a; z-index: 999999; display: none; flex-direction: column; align-items: center; justify-content: center; padding: 20px; text-align: center; }
        .lock-box { background-color: white; padding: 35px; border-radius: 20px; text-align: center; box-shadow: 0px 10px 30px rgba(0, 0, 0, 0.5); max-width: 400px; width: 90%; color: #333; }
        .lock-box h2 { color: #d9534f; margin-bottom: 15px; font-weight: 800; }
        
        /* ALBAABKA MACMIILKA (CUSTOMER PORTAL) */
        .customer-portal-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: #111; z-index: 99998; display: none; flex-direction: column; align-items: center; justify-content: center; padding: 20px; color: #fff; }
        .customer-portal-card { background: #222; padding: 30px; border-radius: 15px; width: 100%; max-width: 400px; text-align: center; box-shadow: 0 10px 25px rgba(0,0,0,0.5); }

        /* SHAASHADDA LOGIN-KA EE GANACSADAHA */
        .merchant-login-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background-color: #0d1117; display: flex; flex-direction: column; justify-content: center; align-items: center; z-index: 99995; padding: 20px; box-sizing: border-box; }
        .merchant-login-card { width: 100%; max-width: 360px; padding: 35px 25px; background: #161b22; border-radius: 16px; text-align: center; box-shadow: 0 20px 40px rgba(0,0,0,0.7); border: 1px solid #30363d; font-family: 'Segoe UI', sans-serif; }
        .merchant-login-card h2 { color: #58a6ff !important; margin-bottom: 5px; font-size: 28px; font-weight: bold; text-transform: uppercase; letter-spacing: 1px; }
        .merchant-login-card p { color: #8b949e; font-size: 13px; margin-bottom: 25px; margin-top: 0; }
        .merchant-input { width: 100%; padding: 14px; margin-bottom: 18px; border: 1px solid #30363d; background: #0d1117 !important; color: #ffffff !important; border-radius: 10px; box-sizing: border-box; font-size: 16px; text-align: center; outline: none; transition: 0.2s; }
        .merchant-input:focus { border-color: #58a6ff; box-shadow: 0 0 0 2px rgba(88,166,255,0.15); }
        .btn-merchant-login { width: 100%; padding: 14px; background: #238636; color: white; border: none; border-radius: 10px; font-size: 16px; font-weight: bold; cursor: pointer; transition: 0.2s; text-transform: uppercase; }
        .btn-merchant-login:hover { background: #2ea043; }
        .merchant-error-msg { color: #f85149; display: none; margin-top: 12px; font-size: 13px; font-weight: bold; }
    </style>
</head>
<body class="light-theme"> 

<div id="paymentModal" style="display:none; position:fixed; top:0; left:0; width:100%; height:100%; background:rgba(0,0,0,0.85); z-index:999999; font-family:'Segoe UI', sans-serif;">
  <div style="background:#ffffff; margin:12% auto; padding:30px; width:90%; max-width:400px; border-radius:16px; text-align:center; box-shadow:0 15px 35px rgba(0,0,0,0.3); color:#333;">
    <h2 style="color:#2563eb; margin-top:0; font-size:22px; font-weight:800;">Ogeysiis Rukunka App-ka</h2>
    <p style="font-size:14px; color:#555; line-height:1.5; margin-bottom:20px;">
        Fadlan bixi rukunka software-ka si aad u sii isticmaasho adegyada <b>DebtWatcher Pro</b>.
    </p>
    
    <div style="margin-bottom:15px; text-align:left;">
      <label style="font-size:12px; font-weight:bold; color:#666;">Lambarka Taleefanka:</label>
      <input type="tel" id="clientPhone" placeholder="Geli lambarkaaga (Tusaale: 061...)" style="width:100%; padding:12px; margin-top:5px; border:1px solid #ccc; border-radius:8px; box-sizing:border-box; color:#000; background:#fff;">
    </div>
    
    <div style="margin-bottom:25px; text-align:left;">
      <label style="font-size:12px; font-weight:bold; color:#666;">Furaha Rukunka (Secret Code):</label>
      <input type="password" id="paymentAmount" placeholder="Geli furaha laguu soo diray" style="width:100%; padding:12px; margin-top:5px; border:1px solid #ccc; border-radius:8px; box-sizing:border-box; color:#000; background:#fff;">
    </div>
    
    <button id="submitPaymentBtn" style="background:#2563eb; color:#fff; padding:14px; border:none; border-radius:8px; font-weight:bold; font-size:16px; cursor:pointer; width:100%; box-shadow:0 4px 10px rgba(37,99,235,0.3);">BIXI HADA 🔑</button>
    
    <button id="closeModalBtn" style="margin-top:12px; background:none; border:none; color:#666; font-size:14px; cursor:pointer; text-decoration:underline;" onclick="document.getElementById('paymentModal').style.display='none'">Xir (Goor Kale)</button>
  </div>
</div>

<div id="dynamicLoginOverlay" class="merchant-login-overlay">
    <div class="merchant-login-card">
        <h2>DebtWatcher</h2>
        <p>Xisaabiyaha Otomaatiga ah ee Dukaanka</p>
        <input type="password" id="dynamicPasswordInput" placeholder="Geli Password-ka Dukaanka..." class="merchant-input">
        <button class="btn-merchant-login" onclick="checkDynamicPassword()">LOGIN NOW 🔓</button>
        <div id="dynamicLoginError" class="merchant-error-msg">Password-ka dukaanka waa khalad!</div>
    </div>
</div>

<div id="lockBox" class="lock-screen">
    <div class="lock-box">
        <h2>⚠️ APP-KA WAA LA XIRAY</h2>
        <p>Fadlan bixi lacagta kirada billaha ah ($4) si aad u sii isticmaasho software-ka.</p>
        <p>La xiriir Maamulka: <b>WhatsApp +252682501951</b></p>
        <hr style="width:80%; margin:15px auto; border:0.5px solid #eee">
        <p style="font-size: 13px; color: #555;">Geli PIN-ka ama Transaction ID-ga rasiidka:</p>
        <input type="password" id="subscription-key" placeholder="••••••••••••" style="text-align: center; font-size: 18px; letter-spacing: 4px;">
        <button onclick="handleLockSubmit()" style="width:100%; padding:14px; background:#007bff; color:white; border:none; border-radius:10px; font-size:16px; font-weight:bold; cursor:pointer;">LOGIN NOW 🔓</button>
        <div id="error-msg" style="color: red; margin-top: 10px; display: none; font-weight: bold;">PIN-ka waa khalad!</div>
    </div>
</div> 

<div id="customerPortal" class="customer-portal-overlay">
    <div class="customer-portal-card">
        <h2 style="color: #3b82f6; margin-top: 0;">ALBAABKA MACMIILKA</h2>
        <p style="font-size: 14px; color: #aaa;">Geli PIN-kaaga si aad u aragto deynta rasmiga ah ee lagugu leeyahay dukaanka.</p>
        <input type="password" id="custPinInput" placeholder="Geli PIN-kaaga (Tusaale: 1234)" style="text-align: center; font-size: 20px; background: #000; border-color: #444; color: #fff; margin-bottom: 15px;">
        <button onclick="checkCustomerPin()" style="width:100%; padding:14px; background:#28a745; color:white; border:none; border-radius:10px; font-size:16px; font-weight:bold; cursor:pointer; margin-bottom: 10px;">Arag Deyntaada 👁️</button>
        <button onclick="exitCustomerPortal()" style="width:100%; padding:14px; background:#555; color:white; border:none; border-radius:10px; font-size:16px; font-weight:bold; cursor:pointer;">Ku Noqo Dukaanka 🛠️</button>
        <div id="custResultArea" style="margin-top: 20px; padding: 15px; border-radius: 10px; display: none; background: #111;"></div>
    </div>
</div>

<div id="mainApp" class="container" style="display: none; opacity: 0; pointer-events: none;">
    <div class="settings-bar">
        <div>Text Size</div>
        <div class="btn-group">
            <button onclick="changeFont('small', event)" class="font-btn">Small</button>
            <button onclick="changeFont('medium', event)" class="font-btn active">Medium</button>
            <button onclick="changeFont('large', event)" class="font-btn">Large</button>
        </div>
        <div>Screen Color</div>
        <div class="btn-group">
            <button onclick="changeTheme('light', event)" class="theme-btn active">Light</button>
            <button onclick="changeTheme('dark', event)" class="theme-btn">Dark</button>
            <button onclick="changeTheme('green', event)" class="theme-btn">Green</button>
        </div>
        <div style="margin-top: 10px; display: flex; flex-direction: column; gap: 5px;">
            <button onclick="openCustomerPortal()" style="background: #e67e22; color: #fff; border: none; padding: 8px; border-radius: 8px; font-weight: bold; cursor: pointer; width: 100%;">🚪 ALBAABKA MACMIILKA (CUSTOMER MODE)</button>
        </div>
    </div> 

    <h2 id="dukaanTitle">DebtWatcher Pro</h2>
    
    <div id="customer-registration-section" class="blue-reg-column">
        <label>Magaca Macamiilka:</label>
        <input type="text" id="cName" placeholder="Halkan ku qor magaca rasmiga ah">

        <label>Telefanka Macamiilka:</label>
        <input type="tel" id="cPhone" placeholder="Tusaale: 061XXXXXXX">
        
        <label>PIN-ka Macmiilka (Password):</label>
        <input type="password" id="cPin" placeholder="PIN-ka (Tusaale: 1234)">

        <button class="btn-add-blue" onclick="addC()">Save (Riix) 💾</button>
    </div>

    <div style="display:flex; gap:8px">
        <input type="text" id="sBar" placeholder="🔍 Search customer..." oninput="render()" style="flex:2">
        <button onclick="back()" style="background:#6c757d; color:#fff; border:none; border-radius:10px; padding:0 15px; cursor:pointer;">Reset</button>
    </div>
    <div class="total-box" id="tGuud">Total: $0.00</div>
    <div id="badhamada-area"></div>
    <table class="sheet-table">
        <thead>
            <tr>
                <th>Magaca Macmiilka</th>
                <th>Haraaga</th>
                <th>Actions</th>
                <th>History</th>
            </tr>
        </thead>
        <tbody id="area"></tbody>
    </table>
    <button onclick="downloadCSV()" style="width:100%; padding:10px; background:#17a2b8; color:white; border:none; border-radius:10px; font-weight:bold; cursor:pointer; margin-top:20px;">📥 Download CSV (Backup)</button>
</div> 

<script>
    const googleScriptUrl = "https://script.google.com/macros/s/AKfycbxATcxrxtxIqTfEqWTqIf2Zg7nnBVMF_sDgNt159kqAnogm3y4P_14rgKYusYXhkkY/exec"; 
    let dynamicSheetURL = localStorage.getItem("user_sheet_url") || "";
    let clients = []; 

    // 1. LIISKA FURAYAASHA AMNIGA (12-KA BILOOD)
    const furayaashaSanadka = {
        1: "9352", 2: "4810", 3: "7264", 4: "1598", 5: "3641", 6: "8523",
        7: "2047", 8: "6139", 9: "5082", 10: "7415", 11: "3968", 12: "8251"
    };

    // 2. MAAREYNTA RUKUNKA EE TAARIIKHDA BISHA BASIIDKA AH
    function checkSubscriptionStatus() {
        let bishaHadda = new Date().getMonth() + 1;
        let lastPaidMonth = parseInt(localStorage.getItem("last_paid_month")) || 0;

        // Haddii bisha la joogo ay isbedeshay, rukunka jooji si otomaatig ah
        if (bishaHadda !== lastPaidMonth) {
            localStorage.setItem("is_subscription_paid", "false");
        }

        let isPaid = localStorage.getItem("is_subscription_paid") === "true";
        let maalintaHadda = new Date().getDate(); 

        // Haddii uu rukunka bixiyey bishan, wax modal ah ha tusin
        if (isPaid) {
            if(document.getElementById("paymentModal")) document.getElementById("paymentModal").style.display = "none";
            if(document.getElementById("lockBox")) document.getElementById("lockBox").style.display = "none";
            return;
        }

        const ogeysiisModal = document.getElementById("paymentModal"); 
        const xiritaanModal = document.getElementById("lockBox");      
        const closeBtn = document.getElementById("closeModalBtn");    

        // TALLAABOOYINKA TAARIIKHDA:
        if (maalintaHadda < 4) {
            if(ogeysiisModal) ogeysiisModal.style.display = "none";
            if(xiritaanModal) xiritaanModal.style.display = "none";
            console.log("Fadlan waqtigii lacagta rukunka wuu dhowyahay.");
        } 
        else if (maalintaHadda === 4 || maalintaHadda === 5) {
            if(ogeysiisModal) {
                ogeysiisModal.style.display = "block";
                if (closeBtn) closeBtn.style.display = "inline-block"; 
            }
            if(xiritaanModal) xiritaanModal.style.display = "none";
        } 
        else if (maalintaHadda >= 6) {
            if(ogeysiisModal) ogeysiisModal.style.display = "none";
            if(xiritaanModal) xiritaanModal.style.display = "flex"; 
            toggleMainAppVisibility(false);
            document.getElementById("dynamicLoginOverlay").style.display = "none";
        }
    }

    // 3. BADHANKA LOGIN-KA EE DUKAANKA
    function checkDynamicPassword() {
        let userInput = document.getElementById("dynamicPasswordInput").value.trim();
        let errorText = document.getElementById("dynamicLoginError"); 
        if (userInput === "") { alert("Fadlan qor password-ka dukaanka!"); return; }
        errorText.style.color = "orange"; errorText.innerText = "Waa lagu guda jiraa furista dukaanka..."; errorText.style.display = "block";

        fetch(`${googleScriptUrl}?action=getMerchantSheet&password=${userInput}`)
            .then(response => response.json())
            .then(data => {
                if (data.status === "Success") {
                    errorText.style.display = "none";
                    localStorage.setItem("dukaan_password", userInput);
                    localStorage.setItem("user_sheet_url", data.sheetURL);
                    dynamicSheetURL = data.sheetURL;
                    document.getElementById("dukaanTitle").innerText = data.businessName;
                    let storeKey = "DATA_" + userInput;
                    clients = JSON.parse(localStorage.getItem(storeKey)) || [];
                    document.getElementById("dynamicLoginOverlay").style.display = "none";
                    toggleMainAppVisibility(true);
                    render();
                    checkSubscriptionStatus();
                } else { errorText.style.color = "#f85149"; errorText.innerText = "⚠️ " + data.message; }
            }).catch(err => {
                let savedPass = localStorage.getItem("dukaan_password");
                if(userInput === savedPass) {
                    errorText.style.display = "none";
                    let storeKey = "DATA_" + userInput;
                    clients = JSON.parse(localStorage.getItem(storeKey)) || [];
                    document.getElementById("dynamicLoginOverlay").style.display = "none";
                    toggleMainAppVisibility(true);
                    render();
                    checkSubscriptionStatus();
                } else { errorText.style.color = "#f85149"; errorText.innerText = "❌ Xiriirka database-ka waa go'an yahay!"; }
            });
    } 

    // 4. MARKII BIINKA LA GELIYO GUDAHA SHASHAADDA LOCK SCREEN-KA (MADAMMA 6-DA LA GAARAY)
    function handleLockSubmit() {
        let inputKey = document.getElementById("subscription-key").value.trim();
        let errorMsg = document.getElementById("error-msg");
        if (inputKey === "") { alert("Fadlan geli PIN-ka rasmiga ah ee rukunka!"); return; }

        let bishaHadda = new Date().getMonth() + 1;
        let biinkaSaxdaAh = furayaashaSanadka[bishaHadda];

        // 7700 waa master pin-kaaga had iyo jeer shaqaynaya
        if (inputKey === biinkaSaxdaAh || inputKey === "7700") {
            localStorage.setItem("is_subscription_paid", "true");
            localStorage.setItem("last_paid_month", bishaHadda);
            document.getElementById("lockBox").style.display = "none";
            document.getElementById("dynamicLoginOverlay").style.display = "flex";
            alert("Furaha rukunka waa sax! App-kii waa lagaa furay.");
            errorMsg.style.display = "none";
        } else {
            errorMsg.style.color = "red";
            errorMsg.innerText = "PIN-ka ama Furaha aad gelisay waa khaldan yahay!";
            errorMsg.style.display = "block";
        }
    }

    function toggleMainAppVisibility(show) {
        let mainContainer = document.getElementById("mainApp");
        if (mainContainer) {
            mainContainer.style.setProperty("display", show ? "block" : "none", "important");
            mainContainer.style.setProperty("opacity", show ? "1" : "0", "important");
            mainContainer.style.setProperty("pointer-events", show ? "all" : "none", "important");
        }
    }

    function changeTheme(theme, event) { document.body.className = theme + '-theme'; document.querySelectorAll('.theme-btn').forEach(btn => btn.classList.remove('active')); event.target.classList.add('active'); }
    function changeFont(size, event) {
        const root = document.documentElement; document.querySelectorAll('.font-btn').forEach(btn => btn.classList.remove('active')); event.target.classList.add('active');
        if(size === 'small') { root.style.setProperty('--main-font', '12px'); root.style.setProperty('--name-font', '14px'); root.style.setProperty('--price-font', '16px'); }
        else if(size === 'medium') { root.style.setProperty('--main-font', '15px'); root.style.setProperty('--name-font', '18px'); root.style.setProperty('--price-font', '20px'); }
        else if(size === 'large') { root.style.setProperty('--main-font', '18px'); root.style.setProperty('--name-font', '22px'); root.style.setProperty('--price-font', '24px'); }
    }

    function addC() { 
        let n = document.getElementById("cName").value.trim(); 
        let p = document.getElementById("cPhone").value.trim(); 
        let pin = document.getElementById("cPin").value.trim() || "1234"; 
        if(!n || !p) { alert("Fadlan buuxi Magaca iyo Telefanka labadaba!"); return; }
        clients.push({ name: n, phone: p, pin: pin, bal: 0, hist: [] }); 
        document.getElementById("cName").value = ""; document.getElementById("cPhone").value = ""; document.getElementById("cPin").value = ""; 
        alert("Macmiilka " + n + " si guul leh ayaa loo diiwaangeliyey!");
        save(); 
    }

    function openCustomerPortal() { document.getElementById("customerPortal").style.display = "flex"; document.getElementById("custPinInput").value = ""; document.getElementById("custResultArea").style.display = "none"; }
    function exitCustomerPortal() { document.getElementById("customerPortal").style.display = "none"; document.getElementById("dynamicLoginOverlay").style.display = "flex"; document.getElementById("dynamicPasswordInput").value = ""; toggleMainAppVisibility(false); }

    function checkCustomerPin() {
        let enteredPin = document.getElementById("custPinInput").value.trim();
        let resultArea = document.getElementById("custResultArea");
        if (enteredPin === "") { alert("Fadlan geli PIN-kaaga rasmiga ah!"); return; }
        let foundClient = clients.find(c => c.pin === enteredPin);
        resultArea.style.display = "block";
        if (foundClient) {
            resultArea.innerHTML = `
                <h3 style="color: #28a745; margin: 0 0 10px 0;">Soodhawoow, ${foundClient.name}!</h3>
                <div style="font-size: 26px; font-weight: bold; color: #ff4d4d; margin-bottom: 10px;">💰 Deyntaada: $${foundClient.bal.toFixed(2)}</div>
                <div style="text-align: left; font-size: 13px; border-top: 1px solid #444; padding-top: 10px; color: #ccc;">
                    <b>Taariikhda dhowaan:</b><br>
                    ${foundClient.hist.slice(0, 3).join("<br>") || "Wax xog ah oo dhowaan ma diiwaangashna."}
                </div>
            `;
        } else { resultArea.innerHTML = `<p style="color: red; font-weight: bold; margin: 0;">⚠️ PIN-ka waa khalad ama lagama diiwaangelin dukaankan!</p>`; }
    }

    function update(i, t){
        let q = parseFloat(prompt(t === 'p' ? "Geli lacagta deynta ah:" : "Geli lacagta bixinta ah:")); if(isNaN(q) || q <= 0) return;
        let d = new Date(); let fullTime = `${d.toLocaleDateString('en-GB')} | ${d.toLocaleTimeString([], {hour:'2-digit', minute:'2-digit'})}`;
        if(t === 'p'){ clients[i].bal += q; clients[i].hist.unshift(`<span style="color:green">+ $${q.toFixed(2)}</span> <small style="color:#888;">[${fullTime}]</small>`); }
        else { clients[i].bal -= q; clients[i].hist.unshift(`<span style="color:red">- $${q.toFixed(2)}</span> <small style="color:#888;">[${fullTime}]</small>`); }
        save();
    }
    
    function tir(i){ if(confirm("Ma hubtaa inaad tirtirto macmiilkan?")){ clients.splice(i, 1); save(); } }
    
    function save(){ 
        let currentPass = localStorage.getItem("dukaan_password") || "HM_V4";
        let storeKey = "DATA_" + currentPass;
        localStorage.setItem(storeKey, JSON.stringify(clients)); 
        render(); 
        if (dynamicSheetURL !== "") {
            fetch(googleScriptUrl, { method: "POST", body: JSON.stringify({ sheetURL: dynamicSheetURL, clients: clients }) });
        }
    }
    
    function toggle(i){ let x = document.getElementById("h-" + i); x.style.display = (x.style.display === "block") ? "none" : "block"; }
    function back(){ document.getElementById("sBar").value = ""; render(); } 

    function render(){
        let a = document.getElementById("area"), q = document.getElementById("sBar").value.toLowerCase(), total = 0; a.innerHTML = "";
        clients.forEach((c, i) => {
            if(!c.name.toLowerCase().includes(q)) return; total += c.bal;
            a.innerHTML += `<tr class="sheet-row">
                <td style="font-size: var(--name-font); font-weight: bold;">👤 ${c.name}<br><small style="color:gray; font-weight:normal;">📱 ${c.phone || 'No Phone'} | 🔑 PIN: ${c.pin || '1234'}</small></td>
                <td style="font-size: var(--price-font); color: var(--primary); font-weight: bold;">$${c.bal.toFixed(2)}</td>
                <td><div class="money-actions"><button class="btn-plus" onclick="update(${i},'p')">+ Debt</button><button class="btn-minus" onclick="update(${i},'m')">- Pay</button></div></td>
                <td><button class="btn-history" onclick="toggle(${i})">🕒 View</button><div id="h-${i}" class="history-content">${c.hist.map(h => `<div class="history-item">${h}</div>`).join("") || "No history yet."}<button class="btn-delete" onclick="tir(${i})">DELETE</button></div></td>
            </tr>`;
        });
        document.getElementById("tGuud").innerText = "Total: $" + total.toFixed(2);
    }
    
    function downloadCSV() {
        let csv = "Magaca,Telefanka,Deynta,Taariikhda\n"; clients.forEach(c => { csv += `${c.name},${c.phone || ''},${c.bal.toFixed(2)},${new Date().toLocaleDateString()}\n`; });
        let a = document.createElement('a'); a.href = window.URL.createObjectURL(new Blob([csv], { type: 'text/csv' })); a.download = 'DebtWatcher_Data.csv'; a.click();
    } 

    // MARKA UU WINDOW-KU LOAD NOQDO
    window.onload = function() { 
        checkSubscriptionStatus(); // Marka hore rukunka eeg taariikhda bisha
        
        let savedPass = localStorage.getItem("dukaan_password");
        if(savedPass) {
            let storeKey = "DATA_" + savedPass;
            clients = JSON.parse(localStorage.getItem(storeKey)) || [];
        }
        render(); 
    }; 

    // SHUQLA BADHANKA "BIXI HADA" EE MODAL-KA BULUUGGA AH
    document.getElementById("submitPaymentBtn").addEventListener("click", function() {
      const phone = document.getElementById("clientPhone").value.trim();
      const paymentCode = document.getElementById("paymentAmount").value.trim();

      if (phone === "" || paymentCode === "") {
        alert("Fadlan geli lambarkaaga iyo Furaha rukunka!");
        return;
      }

      let bishaHadda = new Date().getMonth() + 1;
      let biinkaSaxdaAh = furayaashaSanadka[bishaHadda];

      if (paymentCode === biinkaSaxdaAh || paymentCode === "7700") {
          localStorage.setItem("is_subscription_paid", "true");
          localStorage.setItem("last_paid_month", bishaHadda);
          alert("Mahadsanid! Rukunkaaga si guul leh ayaa loo furay bishan.");
          document.getElementById("paymentModal").style.display = "none";
          checkSubscriptionStatus();
      } else {
          alert("Furaha rukunka (Secret Code) aad gelisay waa khaldan yahay!");
      }
    });
</script>
</body>
</html>
