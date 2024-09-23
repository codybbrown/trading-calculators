<script>
    import PositionSizeInformation from "../components/PositionSizeInformation.svelte";
    import TradeInformation from "../components/TradeInformation.svelte";
    import Results from "../components/Results.svelte";
    let step = 1;

    // Shared Variables
    let entryPrice = 100;

    let stopLoss = 90;
    let contractSize = 2;

    // Trade Information
    let profitTarget = 150;
    let quantity = 1;
    let isLong = 1; // bool

    // Position Size Information
    let accountBalance = 50000;
    let riskPercentage = 0.5;
    let riskAmount = 250;
    let riskRewardRatio = 3.3;
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
                bind:isLong
            />
        {:else if step == 2}
            <PositionSizeInformation
                bind:accountBalance
                bind:riskPercentage
                bind:riskAmount
                bind:riskRewardRatio
            />
        {:else if step == 3}
            <Results
                {entryPrice}
                {stopLoss}
                {contractSize}
                {profitTarget}
                {quantity}
                {accountBalance}
                {riskPercentage}
                {riskAmount}
                {riskRewardRatio}
                {isLong}
            />
        {/if}
        <!-- ===== DEBUG VALUES -->
        <!-- <div class="flex flex-col items-center mb-4">
            {entryPrice}
            {profitTarget}
            {stopLoss}
            {contractSize}
            {quantity}
            {accountBalance}
            {isLong}
        </div> -->
        <div class="flex justify-evenly mx-4">
            {#if step > 1}
                <button
                    type="button"
                    class="btn btn-active btn-danger w-full"
                    on:click={() => --step}>Back</button
                >
            {/if}
            {#if step < 3}
                <button
                    type="button"
                    class="btn btn-active btn-primary w-full"
                    on:click={() => ++step}>Continue</button
                >
            {/if}
        </div>
    </div>
</div>
