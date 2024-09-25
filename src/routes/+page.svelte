<script>
    import TradeInformation from "../components/TradeInformation.svelte";
    import Results from "../components/Results.svelte";
    let step = 1;

    // Shared Variables
    let quantity = 1;
    let entryPrice = 15681.25;
    let profitTarget = 16308.75;
    let stopLoss = 15367.5;
    let accountBalance = 50000;
    let accountSize = 50000;
    let riskPercentage = 0.5;
    let riskAmount = 250;
    let riskRewardRatio = 3.3;

    let contractSize = 2;
    let isLong; // bool

    // Position Size Information
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
        <li class="step step-primary">Trade Details</li>
        <li class="step {step >= 2 && 'step-primary'}">Results</li>
        <!-- <li class="step {step >= 3 && 'step-primary'}">Results</li> -->
    </ul>

    <div class="flex flex-col items-center mb-4">
        {#if step == 1}
            <TradeInformation
                bind:quantity
                bind:entryPrice
                bind:profitTarget
                bind:stopLoss
                bind:accountSize
                bind:riskPercentage
                bind:contractSize
                bind:isLong
            />
        {:else if step == 2}
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

        <div class="flex justify-evenly mx-4">
            {#if step > 1}
                <button
                    type="button"
                    class="btn btn-active btn-danger w-full"
                    on:click={() => --step}>Back</button
                >
            {/if}
            {#if step < 2}
                <button
                    type="button"
                    class="btn btn-active btn-primary w-full"
                    on:click={() => ++step}>Continue</button
                >
            {/if}
        </div>
    </div>
</div>
