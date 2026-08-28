<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport"
      content="width=device-width, initial-scale=1.0,
      maximum-scale=1.0, user-scalable=no">

<title>Tap Tap Game</title>

<script src="https://telegram.org/js/telegram-web-app.js"></script>

<style>
*{
  box-sizing:border-box;
  -webkit-tap-highlight-color:transparent;
}

html,body{
  margin:0;
  padding:0;
  width:100%;
  min-height:100%;
  font-family:Arial,sans-serif;
  background:
    radial-gradient(circle at top,#263d67 0%,#101827 45%,#080d16 100%);
  color:#fff;
}

body{
  min-height:100vh;
}

.app{
  width:100%;
  max-width:520px;
  margin:auto;
  padding:18px 16px 95px;
}

/* HEADER */

.header{
  display:flex;
  align-items:center;
  justify-content:space-between;
  margin-bottom:18px;
}

.brand{
  display:flex;
  align-items:center;
  gap:10px;
}

.logo{
  width:48px;
  height:48px;
  border-radius:15px;
  display:flex;
  align-items:center;
  justify-content:center;
  font-size:25px;
  background:linear-gradient(145deg,#7c3aed,#2563eb);
  box-shadow:0 8px 25px rgba(60,80,255,.35);
}

.brand h1{
  margin:0;
  font-size:21px;
}

.brand p{
  margin:3px 0 0;
  color:#aebbd0;
  font-size:12px;
}

.user{
  text-align:right;
}

.user small{
  color:#91a0b8;
}

#userName{
  display:block;
  font-weight:bold;
  margin-top:3px;
}

/* BALANCE */

.balance{
  background:linear-gradient(145deg,
    rgba(124,58,237,.32),
    rgba(37,99,235,.20));
  border:1px solid rgba(255,255,255,.12);
  border-radius:24px;
  padding:20px;
  text-align:center;
  box-shadow:0 12px 35px rgba(0,0,0,.25);
}

.balance-label{
  color:#b9c4d6;
  font-size:13px;
}

.coins{
  margin-top:6px;
  font-size:39px;
  font-weight:900;
}

.coin-icon{
  font-size:31px;
}

/* TAP AREA */

.tap-section{
  text-align:center;
  margin-top:25px;
}

.tap-section h2{
  margin:0;
  font-size:17px;
}

.tap-section p{
  margin:7px 0 15px;
  color:#9facbf;
  font-size:13px;
}

.tap-button{
  width:210px;
  height:210px;
  border:0;
  border-radius:50%;
  background:
    radial-gradient(circle at 35% 25%,#a78bfa,#7c3aed 45%,#4c1d95);
  color:#fff;
  font-size:27px;
  font-weight:900;
  box-shadow:
    0 0 0 8px rgba(124,58,237,.12),
    0 18px 50px rgba(88,28,135,.55);
  cursor:pointer;
  user-select:none;
  transition:.08s;
}

.tap-button:active{
  transform:scale(.92);
  box-shadow:
    0 0 0 5px rgba(124,58,237,.12),
    0 10px 25px rgba(88,28,135,.45);
}

.tap-button span{
  display:block;
  font-size:42px;
  margin-bottom:5px;
}

/* FLOATING +1 */

.plus{
  position:fixed;
  pointer-events:none;
  font-size:25px;
  font-weight:900;
  color:#facc15;
  animation:floatUp .8s ease-out forwards;
  z-index:99;
}

@keyframes floatUp{
  0%{
    opacity:1;
    transform:translateY(0) scale(1);
  }
  100%{
    opacity:0;
    transform:translateY(-100px) scale(1.3);
  }
}

/* CARDS */

.grid{
  display:grid;
  grid-template-columns:repeat(2,1fr);
  gap:12px;
  margin-top:25px;
}

.card{
  background:rgba(255,255,255,.07);
  border:1px solid rgba(255,255,255,.09);
  border-radius:18px;
  padding:16px;
  min-height:105px;
}

.card .icon{
  font-size:25px;
}

.card h3{
  margin:8px 0 4px;
  font-size:14px;
}

.card p{
  margin:0;
  color:#9facbf;
  font-size:11px;
}

.card button{
  margin-top:9px;
  border:0;
  border-radius:10px;
  padding:8px 11px;
  background:#2563eb;
  color:#fff;
  font-weight:bold;
}

/* REFERRAL */

.referral{
  margin-top:14px;
  background:rgba(255,255,255,.07);
  border:1px solid rgba(255,255,255,.09);
  border-radius:18px;
  padding:16px;
}

.referral h3{
  margin:0 0 5px;
}

.referral p{
  color:#9facbf;
  font-size:12px;
  margin:0 0 12px;
}

.ref-row{
  display:flex;
  gap:8px;
}

.ref-row input{
  min-width:0;
  flex:1;
  border:1px solid rgba(255,255,255,.1);
  border-radius:10px;
  padding:11px;
  color:#fff;
  background:rgba(0,0,0,.25);
}

.ref-row button{
  border:0;
  border-radius:10px;
  padding:0 15px;
  background:#7c3aed;
  color:#fff;
  font-weight:bold;
}

/* MODAL */

.modal{
  position:fixed;
  inset:0;
  background:rgba(0,0,0,.68);
  display:none;
  align-items:center;
  justify-content:center;
  padding:20px;
  z-index:100;
}

.modal.show{
  display:flex;
}

.modal-box{
  width:100%;
  max-width:390px;
  background:#172235;
  border:1px solid rgba(255,255,255,.12);
  border-radius:24px;
  padding:22px;
}

.modal-box h2{
  margin-top:0;
}

.modal-box input,
.modal-box select{
  width:100%;
  padding:13px;
  margin:7px 0;
  border:1px solid rgba(255,255,255,.12);
  border-radius:12px;
  background:#0e1726;
  color:#fff;
}

.modal-actions{
  display:flex;
  gap:10px;
  margin-top:12px;
}

.modal-actions button{
  flex:1;
  padding:13px;
  border:0;
  border-radius:12px;
  font-weight:bold;
}

.cancel{
  background:#334155;
  color:#fff;
}

.confirm{
  background:#7c3aed;
  color:#fff;
}

/* TOAST */

.toast{
  position:fixed;
  left:50%;
  bottom:82px;
  transform:translateX(-50%) translateY(20px);
  background:#111827;
  border:1px solid rgba(255,255,255,.12);
  padding:12px 17px;
  border-radius:13px;
  opacity:0;
  pointer-events:none;
  transition:.25s;
  z-index:200;
  font-size:13px;
  white-space:nowrap;
}

.toast.show{
  opacity:1;
  transform:translateX(-50%) translateY(0);
}

/* NAV */

.nav{
  position:fixed;
  left:50%;
  bottom:0;
  transform:translateX(-50%);
  width:100%;
  max-width:520px;
  display:grid;
  grid-template-columns:repeat(4,1fr);
  padding:10px 8px calc(10px + env(safe-area-inset-bottom));
  background:rgba(10,16,27,.95);
  backdrop-filter:blur(15px);
  border-top:1px solid rgba(255,255,255,.08);
  z-index:50;
}

.nav button{
  border:0;
  background:none;
  color:#8290a7;
  font-size:11px;
}

.nav button span{
  display:block;
  font-size:21px;
  margin-bottom:3px;
}

.nav button.active{
  color:#a78bfa;
}

/* LEADERBOARD */

.rank-list{
  margin-top:15px;
}

.rank{
  display:flex;
  align-items:center;
  justify-content:space-between;
  background:rgba(255,255,255,.06);
  padding:13px;
  border-radius:13px;
  margin-bottom:8px;
}

.rank-left{
  display:flex;
  gap:10px;
  align-items:center;
}

.rank-num{
  width:30px;
  height:30px;
  display:flex;
  justify-content:center;
  align-items:center;
  border-radius:50%;
  background:rgba(255,255,255,.08);
}

/* RESPONSIVE */

@media(max-width:360px){
  .tap-button{
    width:180px;
    height:180px;
  }

  .coins{
    font-size:33px;
  }
}
</style>
</head>

<body>

<div class="app">

  <!-- HEADER -->
  <header class="header">

    <div class="brand">
      <div class="logo">👆</div>

      <div>
        <h1>Tap Tap</h1>
        <p>Play • Tap • Earn</p>
      </div>
    </div>

    <div class="user">
      <small>Player</small>
      <span id="userName">Guest</span>
    </div>

  </header>


  <!-- BALANCE -->
  <section class="balance">

    <div class="balance-label">
      YOUR COINS
    </div>

    <div class="coins">
      <span class="coin-icon">🪙</span>
      <span id="coins">0</span>
    </div>

  </section>


  <!-- TAP -->
  <section class="tap-section">

    <h2>Tap to earn coins</h2>

    <p>
      Every tap gives you <b>+1 coin</b>
    </p>

    <button
      class="tap-button"
      id="tapButton">

      <span>👆</span>
      TAP

    </button>

  </section>


  <!-- FEATURE CARDS -->
  <section class="grid">

    <div class="card">

      <div class="icon">💰</div>

      <h3>Balance</h3>

      <p>
        Your current coin balance
      </p>

    </div>


    <div class="card">

      <div class="icon">🎁</div>

      <h3>Referral</h3>

      <p>
        Invite friends and earn
      </p>

      <button id="inviteBtn">
        Invite
      </button>

    </div>


    <div class="card">

      <div class="icon">💵</div>

      <h3>Withdraw</h3>

      <p>
        Withdraw your earnings
      </p>

      <button id="withdrawBtn">
        Withdraw
      </button>

    </div>


    <div class="card">

      <div class="icon">🏆</div>

      <h3>Leaderboard</h3>

      <p>
        See top players
      </p>

    </div>

  </section>


  <!-- REFERRAL -->
  <section class="referral">

    <h3>🎁 Invite Friends</h3>

    <p>
      Share your referral link and invite friends.
    </p>

    <div class="ref-row">

      <input
        id="refLink"
        readonly
        value="">

      <button id="copyBtn">
        Copy
      </button>

    </div>

  </section>


  <!-- LEADERBOARD -->
  <section style="margin-top:25px">

    <h2 style="font-size:18px">
      🏆 Top Players
    </h2>

    <div class="rank-list">

      <div class="rank">

        <div class="rank-left">
          <div class="rank-num">1</div>
          <b>🥇 Player One</b>
        </div>

        <b>12,450 🪙</b>

      </div>


      <div class="rank">

        <div class="rank-left">
          <div class="rank-num">2</div>
          <b>🥈 Player Two</b>
        </div>

        <b>9,820 🪙</b>

      </div>


      <div class="rank">

        <div class="rank-left">
          <div class="rank-num">3</div>
          <b>🥉 Player Three</b>
        </div>

        <b>7,650 🪙</b>

      </div>

    </div>

  </section>

</div>


<!-- WITHDRAW MODAL -->

<div class="modal" id="withdrawModal">

  <div class="modal-box">

    <h2>💵 Withdraw</h2>

    <p style="color:#9facbf;font-size:13px">
      Enter your withdrawal details.
    </p>

    <input
      id="withdrawAmount"
      type="number"
      placeholder="Amount">

    <select id="withdrawMethod">

      <option value="telebirr">
        Telebirr
      </option>

      <option value="bank">
        Bank
      </option>

    </select>

    <input
      id="withdrawAccount"
      placeholder="Phone / Account number">

    <div class="modal-actions">

      <button
        class="cancel"
        id="closeWithdraw">
        Cancel
      </button>

      <button
        class="confirm"
        id="confirmWithdraw">
        Submit
      </button>

    </div>

  </div>

</div>


<!-- TOAST -->

<div
  class="toast"
  id="toast">
</div>


<!-- BOTTOM NAV -->

<nav class="nav">

  <button class="active">
    <span>🏠</span>
    Home
  </button>

  <button id="navFriends">
    <span>👥</span>
    Friends
  </button>

  <button id="navRank">
    <span>🏆</span>
    Rank
  </button>

  <button id="navProfile">
    <span>👤</span>
    Profile
  </button>

</nav>


<script>

/* =====================================
   TELEGRAM MINI APP
===================================== */

const tg = window.Telegram &&
           window.Telegram.WebApp
           ? window.Telegram.WebApp
           : null;

if(tg){
  tg.ready();
  tg.expand();
}


/* =====================================
   STORAGE
===================================== */

const STORAGE_KEY = "tap_tap_coins";

let coins =
  Number(localStorage.getItem(STORAGE_KEY) || 0);


/* =====================================
   USER
===================================== */

let userName = "Guest";

if(tg && tg.initDataUnsafe && tg.initDataUnsafe.user){

  const user = tg.initDataUnsafe.user;

  userName =
    user.first_name ||
    user.username ||
    "Player";

}

document.getElementById("userName")
  .textContent = userName;


/* =====================================
   COINS
===================================== */

const coinsElement =
  document.getElementById("coins");

function updateCoins(){

  coinsElement.textContent =
    coins.toLocaleString();

  localStorage.setItem(
    STORAGE_KEY,
    coins
  );
}

updateCoins();


/* =====================================
   TAP BUTTON
===================================== */

const tapButton =
  document.getElementById("tapButton");

tapButton.addEventListener(
  "click",
  function(event){

    coins++;

    updateCoins();

    createPlusOne(
      event.clientX,
      event.clientY
    );

    if(navigator.vibrate){
      navigator.vibrate(20);
    }

  }
);


/* =====================================
   +1 ANIMATION
===================================== */

function createPlusOne(x,y){

  const el =
    document.createElement("div");

  el.className = "plus";

  el.textContent = "+1 🪙";

  el.style.left =
    (x - 25) + "px";

  el.style.top =
    (y - 30) + "px";

  document.body.appendChild(el);

  setTimeout(
    () => el.remove(),
    800
  );
}


/* =====================================
   TOAST
===================================== */

const toast =
  document.getElementById("toast");

let toastTimer;

function showToast(message){

  toast.textContent = message;

  toast.classList.add("show");

  clearTimeout(toastTimer);

  toastTimer =
    setTimeout(
      () => toast.classList.remove("show"),
      2200
    );
}


/* =====================================
   REFERRAL LINK
===================================== */

const BOT_USERNAME =
  "TapTapGame_24Bot";

const referralLink =
  "https://t.me/" +
  BOT_USERNAME +
  "?start=ref_" +
  (
    tg &&
    tg.initDataUnsafe &&
    tg.initDataUnsafe.user
      ? tg.initDataUnsafe.user.id
      : "guest"
  );

document.getElementById("refLink")
  .value = referralLink;


/* =====================================
   COPY REFERRAL
===================================== */

document.getElementById("copyBtn")
.addEventListener(
  "click",
  async function(){

    try{

      await navigator.clipboard.writeText(
        referralLink
      );

      showToast(
        "Referral link copied! 🎁"
      );

    }catch(e){

      showToast(
        "Copy failed. Please copy manually."
      );

    }

  }
);


/* =====================================
   TELEGRAM SHARE
===================================== */

document.getElementById("inviteBtn")
.addEventListener(
  "click",
  function(){

    const shareUrl =
      "https://t.me/share/url?url=" +
      encodeURIComponent(referralLink) +
      "&text=" +
      encodeURIComponent(
        "🎮 Join Tap Tap Game and start earning coins!"
      );

    if(tg){

      tg.openTelegramLink(shareUrl);

    }else{

      window.open(
        shareUrl,
        "_blank"
      );

    }

  }
);


/* =====================================
   WITHDRAW
===================================== */

const withdrawModal =
  document.getElementById(
    "withdrawModal"
  );

document.getElementById(
  "withdrawBtn"
).addEventListener(
  "click",
  function(){

    if(coins <= 0){

      showToast(
        "You don't have enough coins."
      );

      return;
    }

    withdrawModal.classList.add(
      "show"
    );

  }
);


document.getElementById(
  "closeWithdraw"
).addEventListener(
  "click",
  function(){

    withdrawModal.classList.remove(
      "show"
    );

  }
);


document.getElementById(
  "confirmWithdraw"
).addEventListener(
  "click",
  function(){

    const amount =
      Number(
        document.getElementById(
          "withdrawAmount"
        ).value
      );

    const method =
      document.getElementById(
        "withdrawMethod"
      ).value;

    const account =
      document.getElementById(
        "withdrawAccount"
      ).value.trim();


    if(!amount || amount <= 0){

      showToast(
        "Enter a valid amount."
      );

      return;
    }


    if(amount > coins){

      showToast(
        "Insufficient coins."
      );

      return;
    }


    if(!account){

      showToast(
        "Enter your account number."
      );

      return;
    }


    /*
      IMPORTANT:
      This is only the FRONTEND request UI.

      A real withdrawal must be processed
      by your secure backend/bot server.
    */


    showToast(
      "Withdrawal request submitted! ✅"
    );

    withdrawModal.classList.remove(
      "show"
    );

    document.getElementById(
      "withdrawAmount"
    ).value = "";

    document.getElementById(
      "withdrawAccount"
    ).value = "";

  }
);


/* =====================================
   NAVIGATION
===================================== */

document.getElementById(
  "navFriends"
).addEventListener(
  "click",
  function(){

    document.querySelector(
      ".referral"
    ).scrollIntoView({
      behavior:"smooth"
    });

  }
);


document.getElementById(
  "navRank"
).addEventListener(
  "click",
  function(){

    document.querySelector(
      ".rank-list"
    ).scrollIntoView({
      behavior:"smooth"
    });

  }
);


document.getElementById(
  "navProfile"
).addEventListener(
  "click",
  function(){

    showToast(
      "Profile: " + userName
    );

  }
);


/* =====================================
   PREVENT DOUBLE TAP ZOOM
===================================== */

let lastTouchEnd = 0;

document.addEventListener(
  "touchend",
  function(event){

    const now =
      Date.now();

    if(
      now - lastTouchEnd <= 300
    ){

      event.preventDefault();

    }

    lastTouchEnd = now;

  },
  false
);

</script>

</body>
</html>
