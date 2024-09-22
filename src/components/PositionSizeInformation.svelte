<script>
    import NumberInput from "./NumberInput.svelte";

    export let accountBalance;
    export let riskPercentage;
    export let riskAmount;
    export let riskRewardRatio;
    // export let entryPrice = 0;
    // export let stopLoss = 0;
    // export let contractSize = 0;
</script>

<NumberInput bind:value={accountBalance} id="account-balance" label="Account Balance" />
<NumberInput bind:value={riskPercentage} id="risk-percentage" label="Risk Percentage" />
<NumberInput bind:value={riskAmount} id="risk-amount" label="Risk Amount" />
<NumberInput bind:value={riskRewardRatio} id="risk-reward-ratio" label="R:R as R" />
