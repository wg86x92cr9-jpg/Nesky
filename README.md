# Nesky
Nesky fx
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Nesky Forex Profit Predictor</title>

<style>

body{
  background:#0f172a;
  color:white;
  font-family:Arial;
  padding:20px;
  text-align:center;
}

.container{
  max-width:500px;
  margin:auto;
  background:#1e293b;
  padding:30px;
  border-radius:20px;
}

h1{
  color:#22c55e;
}

input, select{
  width:90%;
  padding:12px;
  margin:10px 0;
  border:none;
  border-radius:10px;
}

button{
  background:#22c55e;
  color:black;
  padding:15px 30px;
  border:none;
  border-radius:10px;
  font-weight:bold;
  cursor:pointer;
}

.results{
  margin-top:30px;
  text-align:left;
  background:#0f172a;
  padding:20px;
  border-radius:15px;
}

.result-item{
  margin:10px 0;
  font-size:18px;
}

</style>
</head>

<body>

<div class="container">

<h1>Smart Forex Predictor</h1>

<select id="pair">
  <option>EUR/USD</option>
  <option>GBP/USD</option>
  <option>XAU/USD</option>
  <option>USD/JPY</option>
</select>

<select id="type">
  <option>BUY</option>
  <option>SELL</option>
</select>

<input type="number" id="balance" placeholder="Account Balance ($)">

<input type="number" id="risk" placeholder="Risk % per Trade">

<input type="number" id="lot" placeholder="Lot Size">

<input type="number" id="tp" placeholder="Take Profit (Pips)">

<input type="number" id="sl" placeholder="Stop Loss (Pips)">

<button onclick="analyzeTrade()">
Analyze Trade
</button>

<div class="results" id="results">

</div>

</div>

<script>

function analyzeTrade(){

  let balance =
    parseFloat(document.getElementById("balance").value);

  let risk =
    parseFloat(document.getElementById("risk").value);

  let lot =
    parseFloat(document.getElementById("lot").value);

  let tp =
    parseFloat(document.getElementById("tp").value);

  let sl =
    parseFloat(document.getElementById("sl").value);

  let pair =
    document.getElementById("pair").value;

  let type =
    document.getElementById("type").value;

  let pipValue = 10;

  let estimatedProfit =
    tp * lot * pipValue;

  let estimatedLoss =
    sl * lot * pipValue;

  let riskAmount =
    (risk / 100) * balance;

  let rr =
    (estimatedProfit / estimatedLoss).toFixed(2);

  let probability;

  if(rr >= 2){
    probability = "High";
  }
  else if(rr >= 1){
    probability = "Medium";
  }
  else{
    probability = "Low";
  }

  document.getElementById("results").innerHTML = `

    <div class="result-item">
      Pair: ${pair}
    </div>

    <div class="result-item">
      Trade Type: ${type}
    </div>

    <div class="result-item">
      Estimated Profit: $${estimatedProfit}
    </div>

    <div class="result-item">
      Estimated Loss: $${estimatedLoss}
    </div>

    <div class="result-item">
      Risk Amount: $${riskAmount}
    </div>

    <div class="result-item">
      Risk/Reward Ratio: ${rr}
    </div>

    <div class="result-item">
      Winning Probability: ${probability}
    </div>

  `;

}

</script>

</body>
</html>
