<script>
    import NumberInput from "./NumberInput.svelte";
    import SelectInput from "./SelectInput.svelte"; // Exports multiplier prop

    export let quantity = 0;
    export let entryPrice = 0;
    export let profitTarget = 0;
    export let stopLoss = 0;
    export let accountSize = 0;
    export let riskPercentage = 0;
    export let contractSize = 0;
</script>

<div>
    <SelectInput bind:multiplier={contractSize} id="contract-size" label="Instrument" />
    <NumberInput bind:value={accountSize} id="account-size" label="Account Size" />
    <NumberInput bind:value={riskPercentage} id="risk-percentage" label="Percentage To Risk" />
    <NumberInput bind:value={quantity} id="quantity" label="Quantity" />
    <NumberInput bind:value={entryPrice} id="entry-price" label="Entry Price" />
    <NumberInput bind:value={profitTarget} id="profit-target" label="Take Profit" />
    <NumberInput bind:value={stopLoss} id="stop-loss" label="Stop Loss" />
</div>
