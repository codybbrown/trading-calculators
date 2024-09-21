<script>
    import NumberInput from "./NumberInput.svelte";

    export let accountBalance = 0;
    export let riskPercentage = 0;
    // export let entryPrice = 0;
    // export let stopLoss = 0;
    // export let contractSize = 0;
</script>

<NumberInput bind:value={accountBalance} id="account-balance" label="Account Balance" />
<NumberInput bind:value={riskPercentage} id="risk-percentage" label="Risk Percentage" />
