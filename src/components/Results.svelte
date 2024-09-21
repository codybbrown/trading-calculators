<script>
    import MetricCard from "./MetricCard.svelte";

    export let entryPrice = 0;
    export let profitTarget = 0;
    export let stopLoss = 0;
    export let contractSize = 0;
    export let quantity = 0;
    export let isLon = 1; // bool
    export let accountBalance = 0;
    export let riskPercentage = 0;

    function calculateTrade(entryPrice, profitTarget, stopLoss, contractSize, quantity, isLong) {
        const profitLoss = isLong
            ? (profitTarget - entryPrice) * contractSize * quantity
            : (entryPrice - profitTarget) * contractSize * quantity;

        const riskAmount = isLong
            ? (entryPrice - stopLoss) * contractSize * quantity
            : (stopLoss - entryPrice) * contractSize * quantity;

        const riskReward = profitLoss / riskAmount;

        return {
            potentialProfit: profitLoss,
            potentialLoss: riskAmount,
            rRatio: Math.round(riskReward * 100) / 100,
        };
    }

    const tradeResult = calculateTrade(
        entryPrice,
        profitTarget,
        stopLoss,
        contractSize,
        quantity,
        isLong,
    );

    const potentialProfit = tradeResult.potentialProfit;
</script>

<div class="flex flex-col w-full max-w-[90%] md:max-w-[80%] xl:max-w-[75%]">
    <div class="mb-5 mx-2">
        <h1 class="prose-2xl dark:prose-invert">P/L & R</h1>
    </div>

    <div class="grid grid-cols-1 sm:grid-cols-2 xl:grid-cols-4">
        <!-- Calculation Results -->
        <p>IS THIS REAL</p>
        <MetricCard metricValue={potentialProfit} message="Potential Profit" />
    </div>
    <div class="mt-5 mb-3 mx-2">
        <h1 class="prose-2xl dark:prose-invert">Position Size</h1>
    </div>

    <div class="grid grid-cols-1 sm:grid-cols-2">
        <!-- <MetricCard metricValue={salaryExpectations} message="Salary expectations (remote)" /> -->
    </div>
</div>
