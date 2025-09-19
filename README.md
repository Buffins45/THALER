[index.html](https://github.com/user-attachments/files/22421098/index.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Thaler $THAL Presale</title>
<script src="https://cdn.jsdelivr.net/npm/lucid-cardano@0.10.3/dist/lucid.min.js"></script>
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&family=Orbitron:wght@700&display=swap" rel="stylesheet">
<style>
body {
  margin: 0;
  padding: 0;
  font-family: 'Roboto', sans-serif;
  background: #3e2f22;
  color: #d4af7f;
  text-align: center;
  background-image: url('https://i.imgur.com/your-mining-background.jpg');
  background-size: cover;
  background-position: center;
  overflow-x: hidden;
}
.overlay { background-color: rgba(62, 47, 34, 0.85); position:absolute; top:0; left:0; width:100%; height:100%; z-index:-1; }
.container { position: relative; z-index:1; padding: 60px 20px; max-width: 1000px; margin: 0 auto; }
h1 { font-family: 'Orbitron', sans-serif; font-size:48px; margin-bottom:10px; text-shadow:0 0 15px #b87333; }
p { font-size:18px; margin-bottom:20px; line-height:1.5; }
.tabs { display:flex; justify-content:center; gap:20px; margin-bottom:30px; flex-wrap:wrap; }
.tab { cursor:pointer; padding:12px 25px; border-radius:5px; background:#b87333; color:#fff; font-weight:bold; transition:0.3s; }
.tab.active, .tab:hover { background:#d4af7f; color:#3e2f22; }
.tab-content { display:none; animation: fadeIn 0.5s; }
.tab-content.active { display:block; }
@keyframes fadeIn { from{opacity:0;} to{opacity:1;} }

.input-group { margin:20px 0; }
input[type="number"] { padding:10px; font-size:16px; border-radius:5px; border:2px solid #d4af7f; width:220px; text-align:center; margin-bottom:10px; }
#thalerAmount { display:block; font-weight:bold; font-size:18px; margin-top:5px; }

.btn { background-color:#b87333; color:#fff; padding:15px 35px; font-size:18px; border:none; border-radius:5px; cursor:pointer; margin:10px; transition:0.3s; box-shadow:0 0 15px #b87333,0 0 30px #d4af7f; position:relative; }
.btn:hover { background-color:#d4af7f; color:#3e2f22; box-shadow:0 0 30px #d4af7f,0 0 40px #b87333; transform:scale(1.05); }
footer { margin-top:50px; font-size:14px; }
.mine-container { display:flex; justify-content:center; gap:30px; margin:40px 0; flex-wrap:wrap; }
.mine { width:60px; height:120px; background:#3e2f22; border:3px solid #b87333; border-radius:5px; animation: moveUpDown 2s infinite alternate; }
@keyframes moveUpDown { 0%{transform:translateY(0);} 100%{transform:translateY(-15px);} }

@media(max-width:700px){ h1{font-size:36px;} .tab{padding:10px 20px;} input[type="number"]{width:160px;} .mine{width:40px;height:80px;} }
</style>
</head>
<body>
<div class="overlay"></div>
<div class="container">
<h1>Thaler $THAL Presale</h1>
<p>Join the mining revolution and secure your $THAL now!</p>

<div class="tabs">
  <div class="tab active" data-tab="presale">Presale</div>
  <div class="tab" data-tab="info">Info</div>
  <div class="tab" data-tab="wallet">Wallet & Donate</div>
  <div class="tab" data-tab="community">Community</div>
</div>

<!-- Presale Tab -->
<div id="presale" class="tab-content active">
  <div class="mine-container">
    <div class="mine"></div>
    <div class="mine"></div>
    <div class="mine"></div>
  </div>
  <div class="input-group">
    <input type="number" id="adaAmount" placeholder="Amount in ADA" min="1">
    <span id="thalerAmount">0 $THAL</span>
    <button class="btn" id="buyBtn" title="Connect wallet to buy $THAL">Connect Wallet & Buy $THAL</button>
  </div>
  <div id="countdown"></div>
</div>

<!-- Info Tab -->
<div id="info" class="tab-content">
  <h2>Whitepaper & Info</h2>
  <p>Thaler ($THAL) is the mining-inspired token built for community engagement. Our theme revolves around mines, coal shafts, and miners. Presale ends November 1, 2025.</p>
  <a href="https://x.com/peoplesthaler?s=21" class="btn" target="_blank">Follow on X</a>
</div>

<!-- Wallet Tab -->
<div id="wallet" class="tab-content">
  <h2>Wallet & Donate</h2>
  <p>Send ADA to buy $THAL:</p>
  <p><strong>117cd6befe8442fc9ea0ff7587476d72e5586f5fb92684cd3a9a5bae5448414c4552</strong></p>
  <p>Donate $THAL:</p>
  <p><strong>addr1q8ezzalrn0l9q79aqxkxqjmshzwxn9vz29rquylrk4l9aqck0t8n5k4nfe2zvt9fkt9r8dtnkgyje0e599ce4jc3ktmst3g3xq</strong></p>
</div>

<!-- Community Tab -->
<div id="community" class="tab-content">
  <h2>Join the Community</h2>
  <a href="https://discord.gg/MnhtbQ3P" class="btn" target="_blank">Join Discord</a>
  <a href="https://x.com/peoplesthaler?s=21" class="btn" target="_blank">Follow on X</a>
</div>

<footer>&copy; 2025 Thaler $THAL | Designed for the Mining Community</footer>

<script>
const tabs = document.querySelectorAll('.tab');
const contents = document.querySelectorAll('.tab-content');
tabs.forEach(tab => {
  tab.addEventListener('click', ()=>{
    tabs.forEach(t=>t.classList.remove('active'));
    contents.forEach(c=>c.classList.remove('active'));
    tab.classList.add('active');
    document.getElementById(tab.dataset.tab).classList.add('active');
  });
});

// Countdown
const presaleEnd = new Date("2025-11-01T00:00:00").getTime();
const countdownEl = document.getElementById("countdown");
setInterval(()=>{
  const now=new Date().getTime();
  const dist=presaleEnd-now;
  if(dist<0){ countdownEl.innerHTML="Presale Ended!"; return; }
  const d=Math.floor(dist/(1000*60*60*24));
  const h=Math.floor((dist%(1000*60*60*24))/(1000*60*60));
  const m=Math.floor((dist%(1000*60*60))/(1000*60));
  const s=Math.floor((dist%(1000*60))/1000);
  countdownEl.innerHTML=`Presale ends in: ${d}d ${h}h ${m}m ${s}s`;
},1000);

// $THAL calculation
const adaInput=document.getElementById("adaAmount");
const thalerDisplay=document.getElementById("thalerAmount");
const exchangeRate=100; // 1 ADA = 100 $THAL
adaInput.addEventListener("input",()=>{ const ada=parseFloat(adaInput.value)||0; thalerDisplay.textContent=`${ada*exchangeRate} $THAL`; });

// Wallet connect
const buyBtn=document.getElementById('buyBtn');
buyBtn.addEventListener('click', async ()=>{
  try{
    let wallet;
    if(window.cardano?.tokeo) wallet=window.cardano.tokeo;
    else if(window.cardano?.nami) wallet=window.cardano.nami;
    else if(window.cardano?.flint) wallet=window.cardano.flint;
    else if(window.cardano?.gero) wallet=window.cardano.gero;
    else { alert("Install Tokeo, Nami, Flint or Gero."); return; }
    await wallet.enable();
    const lucid = await Lucid.new(wallet, "Mainnet");
    const adaAmount=parseFloat(adaInput.value);
    if(!adaAmount||adaAmount<=0){ alert("Enter valid ADA amount."); return; }
    const tx = await lucid.newTx().payToAddress("117cd6befe8442fc9ea0ff7587476d72e5586f5fb92684cd3a9a5bae5448414c4552",{lovelace:BigInt(adaAmount*1000000)}).complete();
    const signedTx = await tx.sign().complete();
    const txHash = await signedTx.submit();
    buyBtn.textContent="Transaction Sent!";
    buyBtn.style.transform="scale(1.1)";
    setTimeout(()=>{buyBtn.textContent="Connect Wallet & Buy $THAL"; buyBtn.style.transform="scale(1)";},2000);
    alert(`Transaction submitted! Tx Hash: ${txHash}\nYou will receive ${adaAmount*exchangeRate} $THAL.`);
  }catch(e){ console.error(e); alert("Error: "+e);}
});
</script>
</body>
</html>
