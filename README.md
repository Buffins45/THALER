[index.html](https://github.com/user-attachments/files/22420886/index.html)
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Thaler $THAL Presale</title>
<script src="https://cdn.jsdelivr.net/npm/lucid-cardano@0.10.3/dist/lucid.min.js"></script>
<style>
  body {
    margin: 0;
    padding: 0;
    font-family: 'Arial', sans-serif;
    background: #3e2f22;
    color: #d4af7f;
    text-align: center;
    background-image: url('https://i.imgur.com/your-mining-background.jpg');
    background-size: cover;
    background-position: center;
    overflow-x: hidden;
  }

  .overlay {
    background-color: rgba(62, 47, 34, 0.85);
    position: absolute;
    top:0; left:0;
    width:100%; height:100%;
    z-index:-1;
  }

  .container { position: relative; z-index:1; padding: 80px 20px; }
  h1 { font-size:48px; margin-bottom:10px; text-shadow:0 0 15px #b87333; }
  p { font-size:20px; margin-bottom:20px; }

  .btn {
    background-color:#b87333;
    color:#fff;
    padding:15px 35px;
    font-size:18px;
    border:none;
    border-radius:5px;
    cursor:pointer;
    margin:10px;
    text-decoration:none;
    display:inline-block;
    transition: all 0.3s ease;
    box-shadow:0 0 15px #b87333,0 0 30px #d4af7f;
    position:relative;
  }
  .btn:hover {
    background-color:#d4af7f;
    color:#3e2f22;
    box-shadow:0 0 30px #d4af7f,0 0 40px #b87333;
    transform:translateY(-3px) scale(1.05);
  }
  .btn::after {
    content:'';
    position:absolute;
    top:0; left:0; width:100%; height:100%;
    border-radius:5px;
    pointer-events:none;
    background: radial-gradient(circle, rgba(212,175,127,0.6) 0%, transparent 70%);
    opacity:0;
    transition: opacity 0.3s;
  }
  .btn:hover::after { opacity:1; }

  #countdown { font-size:28px; margin:30px 0; font-weight:bold; text-shadow:0 0 10px #b87333; }

  .mine-container { display:flex; justify-content:center; gap:30px; margin:40px 0; }
  .mine { width:60px; height:120px; background:#3e2f22; border:3px solid #b87333; border-radius:5px; animation: moveUpDown 2s infinite alternate; }

  @keyframes moveUpDown { 0% { transform: translateY(0px); } 100% { transform: translateY(-15px); } }

  input[type="number"] { padding:10px; font-size:16px; border-radius:5px; border:2px solid #d4af7f; margin:10px 0; width:200px; text-align:center; }
  #thalerAmount { font-size:18px; margin-top:10px; display:block; }
  footer { margin-top:50px; font-size:14px; }

  @media (max-width:600px) {
    h1 { font-size:32px; }
    p { font-size:16px; }
    .btn { padding:12px 25px; font-size:16px; }
    #countdown { font-size:22px; }
    .mine-container { gap:15px; }
    .mine { width:40px; height:80px; }
    input[type="number"] { width:150px; }
  }
</style>
</head>
<body>
<div class="overlay"></div>
<div class="container">
  <h1>Thaler $THAL Presale</h1>
  <p>Join the mining revolution and secure your $THAL now!</p>

  <div class="mine-container">
    <div class="mine"></div>
    <div class="mine"></div>
    <div class="mine"></div>
  </div>

  <div id="countdown"></div>

  <input type="number" id="adaAmount" placeholder="Amount in ADA" min="1">
  <span id="thalerAmount">0 $THAL</span>
  <button class="btn" id="buyBtn" title="Click to connect wallet and buy $THAL">Connect Wallet & Buy $THAL</button>

  <a href="https://discord.gg/MnhtbQ3P" class="btn" target="_blank">Join Discord</a>
  <a href="https://x.com/peoplesthaler?s=21" class="btn" target="_blank">Follow on X</a>
  <a href="https://example.com/donate?address=addr1q8ezzalrn0l9q79aqxkxqjmshzwxn9vz29rquylrk4l9aqck0t8n5k4nfe2zvt9fkt9r8dtnkgyje0e599ce4jc3ktmst3g3xq" class="btn" target="_blank">Donate $THAL</a>
</div>

<footer>&copy; 2025 Thaler $THAL | Designed for the Mining Community</footer>

<script>
const presaleEnd = new Date("2025-11-01T00:00:00").getTime();
const countdownEl = document.getElementById("countdown");
setInterval(() => {
  const now = new Date().getTime();
  const dist = presaleEnd - now;
  if(dist < 0){ countdownEl.innerHTML = "Presale Ended!"; return; }
  const d = Math.floor(dist/(1000*60*60*24));
  const h = Math.floor((dist % (1000*60*60*24))/(1000*60*60));
  const m = Math.floor((dist % (1000*60*60))/(1000*60));
  const s = Math.floor((dist % (1000*60))/1000);
  countdownEl.innerHTML = `Presale ends in: ${d}d ${h}h ${m}m ${s}s`;
},1000);

const adaInput = document.getElementById("adaAmount");
const thalerDisplay = document.getElementById("thalerAmount");
const exchangeRate = 100; // 1 ADA = 100 $THAL
adaInput.addEventListener("input", () => {
  const ada = parseFloat(adaInput.value) || 0;
  thalerDisplay.textContent = `${ada*exchangeRate} $THAL`;
});

const buyBtn = document.getElementById('buyBtn');
buyBtn.addEventListener('click', async () => {
  try {
    let wallet;
    if(window.cardano?.tokeo) wallet = window.cardano.tokeo;
    else if(window.cardano?.nami) wallet = window.cardano.nami;
    else if(window.cardano?.flint) wallet = window.cardano.flint;
    else if(window.cardano?.gero) wallet = window.cardano.gero;
    else { alert("Install Tokeo, Nami, Flint or Gero."); return; }

    await wallet.enable();
    const lucid = await Lucid.new(wallet, "Mainnet");
    const adaAmount = parseFloat(adaInput.value);
    if(!adaAmount || adaAmount <= 0){ alert("Enter valid ADA amount."); return; }

    const tx = await lucid.newTx()
      .payToAddress("117cd6befe8442fc9ea0ff7587476d72e5586f5fb92684cd3a9a5bae5448414c4552", { lovelace: BigInt(adaAmount*1000000) })
      .complete();

    const signedTx = await tx.sign().complete();
    const txHash = await signedTx.submit();

    // Button animation feedback
    buyBtn.textContent = "Transaction Sent!";
    buyBtn.style.transform = "scale(1.1)";
    setTimeout(()=>{ buyBtn.textContent="Connect Wallet & Buy $THAL"; buyBtn.style.transform="scale(1)"; },2000);

    alert(`Transaction submitted! Tx Hash: ${txHash}\nYou will receive ${adaAmount*exchangeRate} $THAL.`);
  } catch(e){ console.error(e); alert("Error: "+e); }
});
</script>
</body>
</html>
