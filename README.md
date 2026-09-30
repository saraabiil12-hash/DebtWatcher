<!DOCTYPE html>
<html lang="so">
<head>  
<link rel="manifest" href="manifest.json">
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>HantiMaamul</title>
<style>
:root {
  --bg-color: #f4f6f9;
  --container-bg: #ffffff;
  --text-color: #333333;
  --accent-color: #007bff;
  --border-color: #cccccc;
  --main-font: 15px;
  --name-font: 18px;
  --price-font: 20px;
}

.dark-theme {
  --bg-color: #121212;
  --container-bg: #1e1e1e;
  --text-color: #e0e0e0;
  --accent-color: #00adb5;
  --border-color: #333;
}

.light-theme {
  --bg-color: #f4f6f9;
  --container-bg: #ffffff;
  --text-color: #333333;
  --accent-color: #007bff;
}

* { box-sizing: border-box; margin: 0; padding: 0; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; }
body { background-color: var(--bg-color); color: var(--text-color); font-size: var(--main-font); padding: 10px; transition: background 0.3s, color 0.3s; overflow-x: hidden; }

.container { 
  max-width: 1200px; 
  margin: 0 auto; 
  background: var(--container-bg); 
  padding: 15px; 
  border-radius: 8px; 
  box-shadow: 0 4px 6px rgba(0,0,0,0.05); 
  border: 1px solid var(--border-color); 
  position: relative;
}

/* OVERLAY MODALS */
.overlay-card {
  position: fixed;
  top: 0; left: 0;
  width: 100%; height: 100%;
  background: rgba(0, 0, 0, 0.7);
  z-index: 9999;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 15px;
}

.card-content { 
  background: var(--container-bg); 
  padding: 20px; 
  border-radius: 10px; 
  width: 100%; 
  max-width: 480px; 
  text-align: center; 
  border: 1px solid var(--border-color); 
  max-height: 90vh; 
  overflow-y: auto; 
  color: var(--text-color);
}

/* HEADER */
.app-header { 
  display: flex; 
  justify-content: space-between; 
  align-items: center; 
  background: linear-gradient(135deg, #0056b3, #007bff); 
  padding: 14px 18px; 
  border-radius: 8px; 
  margin-bottom: 15px; 
  box-shadow: 0 4px 10px rgba(0, 123, 255, 0.25);
  position: relative;
  z-index: 100;
}

.merchant-title-style { 
  font-weight: bold; 
  font-size: 20px; 
  color: #ffffff; 
}

.menu-dropdown { position: relative; display: inline-block; }

.menu-btn { 
  background: rgba(255, 255, 255, 0.2); 
  color: #ffffff; 
  padding: 8px 16px; 
  font-size: 14px; 
  border: 1px solid rgba(255, 255, 255, 0.4); 
  border-radius: 6px; 
  cursor: pointer; 
  font-weight: bold; 
}

.dropdown-content { 
  display: none; 
  position: absolute; 
  left: 0; 
  top: 45px; 
  background-color: var(--container-bg); 
  min-width: 220px; 
  box-shadow: 0px 8px 16px rgba(0,0,0,0.2); 
  z-index: 1000; 
  border-radius: 6px; 
  border: 1px solid var(--border-color); 
  overflow: hidden; 
}

.dropdown-content a { 
  color: var(--text-color); 
  padding: 12px 16px; 
  text-decoration: none; 
  display: block; 
  font-weight: bold; 
  font-size: 14px; 
  border-bottom: 1px solid var(--border-color); 
}

.dropdown-content a:hover { background-color: rgba(0,123,255,0.1); }
.show-dropdown { display: block !important; }

.section-badge-header { 
  display: flex; 
  justify-content: space-between; 
  align-items: center; 
  background: linear-gradient(135deg, #0056b3, #007bff); 
  color: #ffffff;
  padding: 12px 16px; 
  border-radius: 6px; 
  margin-bottom: 15px; 
  font-weight: bold; 
}

.section-badge-header .count-pill { 
  background: #ffffff; 
  color: #0056b3; 
  padding: 3px 10px; 
  border-radius: 12px; 
  font-size: 13px; 
  font-weight: bold; 
}

.input-group { display: flex; flex-direction: column; gap: 10px; background: rgba(0,0,0,0.02); padding: 14px; border-radius: 6px; border: 1px solid var(--border-color); margin-bottom: 12px; text-align: left; }

input, select { width: 100%; padding: 10px; border-radius: 5px; border: 1px solid var(--border-color); background: #fff; color: #333; font-size: 14px; }
.dark-theme input, .dark-theme select { background: #2a2a2a; color: #fff; }

button { padding: 10px; border: none; border-radius: 5px; font-weight: bold; cursor: pointer; font-size: 14px; background: var(--accent-color); color: #fff; }
.btn-danger { background: #dc3545; color: #fff; }
.btn-success { background: #28a745; color: #fff; }
.btn-secondary { background: #6c757d; color: #fff; }
.btn-warning { background: #ffc107; color: #000; }

.customer-row { display: flex; flex-direction: column; gap: 8px; padding: 12px; background: rgba(0,0,0,0.01); border: 1px solid var(--border-color); border-radius: 6px; margin-bottom: 8px; }
.customer-row-top { display: flex; justify-content: space-between; align-items: center; }
.amaano-card-btn { display: flex; flex-direction: column; gap: 8px; background: rgba(40,167,69,0.05); border: 1px solid var(--border-color); border-left: 5px solid #28a745; padding: 12px; margin-bottom: 8px; border-radius: 6px; width: 100%; }

.customer-info-left { display: flex; flex-direction: column; text-align: left; }
.customer-name-text { font-size: var(--name-font); font-weight: bold; }
.customer-phone-text { font-size: 12px; color: #666; }
.customer-balance-right { font-size: var(--price-font); font-weight: bold; color: #dc3545; }
.total-box { font-size: 18px; font-weight: bold; text-align: center; margin-top: 10px; padding: 10px; background: #e9ecef; border-radius: 5px; color: var(--accent-color); }
.dark-theme .total-box { background: #2b2b2b; }

.drawer-overlay { position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(0, 0, 0, 0.5); display: none; z-index: 9998; }
.drawer-overlay.active { display: block; }

.side-drawer { position: fixed; top: 0; right: -100%; width: 100%; max-width: 440px; height: 100%; background: var(--container-bg); box-shadow: -5px 0 25px rgba(0,0,0,0.15); transition: right 0.3s ease; z-index: 9999; display: flex; flex-direction: column; padding: 20px; overflow-y: auto; }
.side-drawer.open { right: 0; }

.warning-banner { background: #fff3cd; color: #856404; border: 1px solid #ffeeba; padding: 10px; border-radius: 6px; font-size: 13px; margin-bottom: 12px; text-align: center; font-weight: bold; display: none; }

.theme-font-section { display: flex; justify-content: space-between; margin-top: 20px; padding-top: 10px; border-top: 1px solid var(--border-color); }
.sub-btn-group { display: flex; flex-direction: column; gap: 4px; width: 48%; }
.mini-btn-grid { display: grid; grid-template-columns: repeat(2, 1fr); gap: 4px; }
.mini-btn-grid-three { display: grid; grid-template-columns: repeat(3, 1fr); gap: 4px; }
.theme-btn, .font-btn { padding: 6px; font-size: 11px; background: #e0e0e0; color: #333; border: 1px solid var(--border-color); font-weight: bold; cursor: pointer; }
.theme-btn.active, .font-btn.active { background: var(--accent-color); color: #fff; }

.action-btn-row { display: flex; gap: 6px; flex-wrap: wrap; margin-top: 4px; }
.action-btn-row button { padding: 6px 10px; font-size: 12px; border-radius: 4px; flex: 1; }

.badge-tag { padding: 3px 8px; border-radius: 4px; font-size: 11px; font-weight: bold; }
.badge-deyn { background: rgba(220,53,69,0.15); color: #dc3545; }
.badge-amaano { background: rgba(40,167,69,0.15); color: #28a745; }

.view-section { display: block; }
.hidden-section { display: none !important; }
</style>
</head>
<body class="light-theme">

<!-- LOCKOUT OVERLAY -->
<div id="appLockoutOverlay" class="overlay-card" style="display: none;">
  <div class="card-content">
    <h2 style="color: #dc3545; margin-bottom: 10px;">🔒 App Locked</h2>
    <p style="font-size: 14px; margin-bottom: 15px;">Subscription expired. Please renew your plan.</p>
    <div style="background: rgba(0,123,255,0.1); padding: 12px; border-radius: 6px; margin-bottom: 15px;">
      <p style="font-size: 13px; font-weight: bold;">Contact for activation:</p>
      <p style="font-size: 18px; font-weight: bold; color: #007bff; margin-top: 5px;">📞 +252682501951</p>
    </div>
    <input type="text" id="activationCodeInput" placeholder="Enter activation code..." style="margin-bottom: 10px;">
    <button onclick="unlockAppWithCode()" class="btn-success" style="width: 100%;">UNLOCK</button>
  </div>
</div>

<!-- PORTAL-KA MACMIILKA -->
<div id="customerPortal" class="overlay-card" style="display:flex;">
  <div class="card-content">
    <h2>📱 Customer Portal</h2>
    <p style="font-size: 12px; color: #666; margin-bottom: 12px;">Enter your PIN to access account:</p>

    <div id="custAuthForm">
      <input type="password" id="custPinInput" placeholder="Enter PIN..." autocomplete="off">
      <button onclick="accessCustomerFiles()" class="btn-success" style="width:100%; margin-top:10px;">LOGIN</button>
    </div>

    <div id="custResultArea" style="margin-top:15px; display:none; text-align: left;">
      <div style="background: rgba(0,123,255,0.05); padding: 12px; border-radius: 6px; border: 1px solid var(--accent-color); margin-bottom: 12px; text-align: center;">
        <span id="portalAccountBadge" class="badge-tag badge-deyn">Deyn</span>
        <h3 id="portalClientTitle" style="color: var(--accent-color); margin-top: 6px;">👤 Welcome</h3>
      type: 'kudalacag', amount: totalAmount,
      note: `Invoice: ${desc} (${qty} x $${price.toFixed(2)})`,
      date: new Date().toLocaleString('so-SO', { hour12: true })
    });
  } else {
    customer.bal = (Number(customer.bal) || 0) - totalAmount;
    customer.hist.unshift({
      type: 'bixi', amount: totalAmount,
      note: `Invoice: ${desc} (${qty} x $${price.toFixed(2)})`,
      date: new Date().toLocaleString('so-SO', { hour12: true })
    });
  }

  save();
  document.getElementById("invDesc").value = "";
  document.getElementById("invQty").value = "1";
  document.getElementById("invPrice").value = "0.00";
  alert("✅ Invoice-ka waa loo kaydiyay macmiilka!");
  closeInvoiceModal();
}

function toggleMenu() { document.getElementById("myDropdown").classList.toggle("show-dropdown"); }

function switchView(viewName) {
  document.getElementById("myDropdown").classList.remove("show-dropdown");
  document.getElementById("viewDebtsSection").classList.add("hidden-section");
  document.getElementById("viewAmaanadaSection").classList.add("hidden-section");
  document.getElementById("viewMacaamiishaSection").classList.add("hidden-section");

  if (viewName === 'debts') { document.getElementById("viewDebtsSection").classList.remove("hidden-section"); render(); }
  else if (viewName === 'amaanada') { document.getElementById("viewAmaanadaSection").classList.remove("hidden-section"); renderAmaanada(); }
  else if (viewName === 'macaamiisha') { document.getElementById("viewMacaamiishaSection").classList.remove("hidden-section"); renderMacaamiishaGrid(); }
}

function changeTheme(theme, e) {
  if (e) {
    document.querySelectorAll('.theme-btn').forEach(btn => btn.classList.remove('active'));
    e.target.classList.add('active');
  }
  document.body.className = theme === 'dark' ? 'dark-theme' : 'light-theme';
}

function changeFont(size, e) {
  if (e) {
    document.querySelectorAll('.font-btn').forEach(btn => btn.classList.remove('active'));
    e.target.classList.add('active');
  }
  document.documentElement.style.setProperty('--main-font', size);
}

function addNewStore() {
  let storeName = prompt("Geli magaca dukaanka cusub:");
  if (storeName && storeName.trim() !== "") {
    let select = document.getElementById("storeSelect");
    let option = document.createElement("option");
    option.value = storeName.trim();
    option.text = storeName.trim();
    select.appendChild(option);
    select.value = storeName.trim();
    changeStore(storeName.trim());
  }
}

function changeStore(storeName) {
  loadStoreData(storeName);
  render();
  renderAmaanada();
  renderMacaamiishaGrid();
  populateInvoiceSelect();
  alert("🟢 Waxaa loo badalay: " + storeName);
}
</script>
</body>
</html>
 
