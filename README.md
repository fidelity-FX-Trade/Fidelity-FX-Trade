<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Deposit | Fidelity FX (Demo)</title>
  <style>
    :root{
      --bg: #0f1220;
      --card: #141a2a;
      --card-edge: #1e2540;
      --text: #e9eaf6;
      --muted: #a6a6b3;
      --accent: #4cc9f0;
      --accent-2: #ffd166;
    }
    *{box-sizing:border-box}
    html,body{margin:0;padding:0;height:100%}
    body{
      font-family: system-ui, -apple-system, "Segoe UI", Roboto, Arial;
      background: radial-gradient(circle at 20% -10%, rgba(76,201,240,.15), transparent 40%),
                  radial-gradient(circle at 100% 0%, rgba(255,209,102,.12), transparent 40%),
                  var(--bg);
      color: var(--text);
      min-height:100vh;
    }

    .deposit-wrap{
      max-width: 900px;
      margin: 40px auto;
      padding: 20px;
    }

    .deposit-header h1{
      font-size: 2rem;
      margin: 0 0 8px;
    }
    .deposit-header .subtitle{
      color: var(--muted);
      margin: 0 0 20px;
      font-weight: 500;
    }

    .currency-grid{
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(140px, 1fr));
      gap: 12px;
      margin-bottom: 18px;
    }

    .currency-card{
      display:flex; align-items:center; gap:8px;
      padding:12px;
      background: linear-gradient(#1b2140, #141a2a);
      border:1px solid var(--card-edge);
      border-radius: 12px;
      cursor: pointer;
      text-align:left;
      color: var(--text);
      transition: transform .15s ease, box-shadow .15s ease;
    }
    .currency-card:hover{ transform: translateY(-1px); box-shadow: 0 6px 18px rgba(0,0,0,.25); }
    .currency-card[aria-pressed="true"]{
      outline: 2px solid var(--accent);
      background: linear-gradient(#1a254a, #1b2140);
    }

    .currency-card .icon{
      font-size: 1.4rem;
      width: 28px;
      height: 28px;
      display: inline-flex;
      align-items: center;
      justify-content: center;
    }
    .currency-card .name{
      font-weight: 600;
    }

    .deposit-amount{
      margin: 10px 0 20px;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 12px;
    }
    .deposit-amount label{
      grid-column: 1 / -1;
      color: var(--muted);
      font-size: .9rem;
      margin-bottom: 6px;
    }
    .deposit-amount input{
      padding: 10px 12px;
      border-radius: 8px;
      border:1px solid #334;
      background: #0b1020;
      color: var(--text);
    }

    .deposit-actions{
      text-align: right;
    }
    .btn{
      padding: 12px 18px;
      border-radius: 8px;
      border: none;
      background: linear-gradient(135deg, #4cc9f0, #0ea5e9);
      color: white;
      cursor: pointer;
      font-weight: 700;
    }
    .btn[disabled]{
      opacity:.5; cursor:not-allowed;
    }

    @media (max-width: 600px){
      .deposit-amount{ grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>
  <main class="deposit-wrap">
    <section class="deposit-header">
      <h1>Deposit</h1>
      <p class="subtitle">STEP 1: SELECT CRYPTOCURRENCY</p>
    </section>

    <section class="currency-grid" aria-label="Choose cryptocurrency">
      <button class="currency-card" data-currency="btc" aria-pressed="false" title="Bitcoin">
        <span class="icon" aria-hidden="true">₿</span>
        <span class="name">Bitcoin</span>
      </button>
      <button class="currency-card" data-currency="eth" aria-pressed="false" title="Ethereum">
        <span class="icon" aria-hidden="true">Ξ</span>
        <span class="name">Ethereum</span>
      </button>
      <button class="currency-card" data-currency="ltc" aria-pressed="false" title="Litecoin">
        <span class="icon" aria-hidden="true">Ł</span>
        <span class="name">Litecoin</span>
      </button>
      <button class="currency-card" data-currency="xrp" aria-pressed="false" title="Ripple">
        <span class="icon" aria-hidden="true">✕</span>
        <span class="name">Ripple</span>
      </button>
      <button class="currency-card" data-currency="sol" aria-pressed="false" title="Solana">
        <span class="icon" aria-hidden="true">◎</span>
        <span class="name">Solana</span>
      </button>
    </section>

    <section class="deposit-amount" aria-label="Deposit amount">
      <label for="amount">Deposit Amount (USD)</label>
      <input type="number" id="amount" min="0" step="0.01" placeholder="0.00" />
    </section>

    <section class="deposit-actions">
      <button id="continueBtn" class="btn" disabled>Continue</button>
    </section>
  </main>

  <script>
    document.addEventListener('DOMContentLoaded', () => {
      const cards = document.querySelectorAll('.currency-card');
      const amountInput = document.getElementById('amount');
      const continueBtn = document.getElementById('continueBtn');

      let selectedCurrency = null;

      cards.forEach(card => {
        card.addEventListener('click', () => {
          // clear previous
          cards.forEach(c => c.setAttribute('aria-pressed', 'false'));
          card.setAttribute('aria-pressed', 'true');
          selectedCurrency = card.dataset.currency;
          updateContinueState();
        });
      });

      amountInput.addEventListener('input', updateContinueState);

      function updateContinueState() {
        const hasAmount = parseFloat(amountInput.value) > 0;
        if (selectedCurrency && hasAmount) {
          continueBtn.disabled = false;
        } else {
          continueBtn.disabled = true;
        }
      }

      continueBtn.addEventListener('click', () => {
        // Example: proceed to next step
        if (continueBtn.disabled) return;
        // You can navigate to a next step route or reveal a modal.
        alert(`Proceeding with ${selectedCurrency.toUpperCase()} deposit of $${parseFloat(amountInput.value).toFixed(2)}`);
      });
    });
  </script>
</body>
</html>
