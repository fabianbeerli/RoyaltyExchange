<script>
    let url = location.protocol + "//" + location.host;
    let predictedPrice = "n.a.";

    async function predict() {
        let last12MonthEarnings = parseInt($$('last12MonthEarnings').value);
        let dollarAge = parseInt($$('dollarAge').value);

        let result = await fetch(
            `${url}/api/predict`,
            {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({ last12MonthEarnings, dollarAge })
            }
        );
        let data = await result.json();
        predictedPrice = data.predictedPrice;

        $$('predictedPrice').innerText = predictedPrice;
    }
</script>

<h1>Price Prediction</h1>

<div class="input-container">
    <label for="last12MonthEarnings">Last 12 Month Earnings:</label>
    <input type="number" id="last12MonthEarnings" min="0" max="1000000" />
</div>

<div class="input-container">
    <label for="dollarAge">Dollar Age:</label>
    <input type="number" id="dollarAge" min="0" max="100" />
</div>

<button on:click={predict}>Predict</button>

<p>Predicted Price: <span id="predictedPrice">{predictedPrice}</span></p>
