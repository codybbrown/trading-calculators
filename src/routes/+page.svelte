<script>
    import PositionSizeInformation from "../components/PositionSizeInformation.svelte";
    import TradeInformation from "../components/TradeInformation.svelte";
    import Results from "../components/Results.svelte";
    let step = 1;

    // Shared Variables
    let entryPrice = 0;
    let stopLoss = 0;
    let contractSize = 0;

    // Trade Information
    let profitTarget = 0;
    let quantity = 0;
    let isLon = 1; // bool

    // Position Size Information
    let accountBalance = 0;
    let riskPercentage = 0;
    // let contractSize = 0;
</script>

<div class="p-4 flex flex-col items-center font-sans">
    <div class="mb-5 max-w-[90%] md:max-w-[70%] xl:max-w-[50%]">
        <h1 class="prose-2xl dark:prose-invert leading-snug">Trading Calculators</h1>
    </div>
    <p class="mb-4 max-w-[90%] md:max-w-[70%] xl:max-w-[50%]">
        A set of risk management utilities for futures and forex trading.
    </p>
    <p class="divider prose-xl dark:prose-invert">Start Calculation</p>

    <ul class="steps mb-6">
        <li class="step step-primary">Profit/Loss Details</li>
        <li class="step {step >= 2 && 'step-primary'}">Position Size Details</li>
        <li class="step {step >= 3 && 'step-primary'}">Results</li>
    </ul>

    <div class="flex flex-col items-center mb-4">
        {#if step == 1}
            <TradeInformation
                bind:entryPrice
                bind:profitTarget
                bind:stopLoss
                bind:contractSize
                bind:quantity
                bind:isLon
            />
        {:else if step == 2}
            <PositionSizeInformation bind:accountBalance bind:riskPercentage />
        {:else if step == 3}
            <Results
                {entryPrice}
                {profitTarget}
                {stopLoss}
                {contractSize}
                {quantity}
                {isLon}
                {accountBalance}
            />
        {/if}
    </div>
    <!-- <div class="flex flex-col items-center mb-4">
        {entryPrice}
        {profitTarget}
        {stopLoss}
        {contractSize}
        {quantity}
        {isLon}
        {accountBalance}
    </div> -->
    <div class="flex justify-evenly mx-4">
        {#if step > 1}
            <button type="button" class="btn btn-active btn-danger w-full" on:click={() => --step}
                >Back</button
            >
        {/if}
        {#if step < 3}
            <button type="button" class="btn btn-active btn-primary w-full" on:click={() => ++step}
                >Continue</button
            >
        {/if}
    </div>
</div>
