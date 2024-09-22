<script>
    import MetricCard from "./MetricCard.svelte";

    // ---------- BOUND VARIABLES
    export let entryPrice;
    export let profitTarget;
    export let stopLoss;
    export let contractSize;
    export let quantity;
    export let accountBalance;
    export let riskPercentage;
    export let riskAmount;
    export let riskRewardRatio;
    export let isLong;

    // const riskReward = 3.3;
    // const positionSize = 2;
    // const positionSize = 1.69;

    // ---------- CALCULATE TRADE P/L & R RATIO
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

    // ---------- CALCULATE POSITION SIZE
    function calculatePositionSizeRiskReward(
        accountBalance,
        riskAmount,
        riskPercentage,
        riskRewardRatio,
        entryPrice,
        stopLoss,
        contractSize,
    ) {
        // determine risk amount
        let actualRiskAmount;
        if (riskAmount) {
            actualRiskAmount = riskAmount;
        } else if (riskPercentage) {
            actualRiskAmount = accountBalance * (riskPercentage / 100);
        } else {
            throw new Error("Either riskAmount or riskPercentage must be provided");
        }

        // calculate the risk per contract
        const riskPerContract = Math.abs(entryPrice - stopLoss) * contractSize;
        // calculate the basic position size based on risk
        const basicPositionSize = actualRiskAmount / riskPerContract;
        // calculate the reward amount
        const rewardAmount = actualRiskAmount * riskRewardRatio;
        const profitTarget =
            entryPrice > stopLoss
                ? entryPrice + rewardAmount / (basicPositionSize * contractSize)
                : entryPrice - rewardAmount / (basicPositionSize * contractSize);

        // round down to nearest whole contract
        // const finalPositionSize = Math.floor(basicPositionSize);
        // const finalPositionSize = Math.ceil(basicPositionSize);
        const finalPositionSize = basicPositionSize;

        return {
            positionSize: finalPositionSize,
            riskAmount: actualRiskAmount,
            rewardAmount: rewardAmount,
            profitTarget: profitTarget,
        };
    }

    // ---------- FUNCTION CALLS / USAGE
    const tradeResult = calculateTrade(
        entryPrice,
        profitTarget,
        stopLoss,
        contractSize,
        quantity,
        isLong,
    );

    const positionSizeRiskReward = calculatePositionSizeRiskReward(
        accountBalance,
        riskAmount,
        riskPercentage,
        riskRewardRatio,
        entryPrice,
        stopLoss,
        contractSize,
    );

    // console.log(`Profit: ${tradeResult.potentialProfit}`);
    // console.log(`Loss: ${tradeResult.potentialLoss}`);
    // console.log(`R: ${tradeResult.rRatio}`);
    // console.log(`Position Size: ${positionSize} contract`);

    console.log(positionSizeRiskReward.contractSize);
</script>

<div class="flex flex-col w-full max-w-[90%] md:max-w-[80%] xl:max-w-[75%]">
    <div class="mb-5 mx-2">
        <h1 class="prose-2xl dark:prose-invert">P/L & R</h1>
    </div>

    <div class="grid grid-cols-1 sm:grid-cols-2 xl:grid-cols-4">
        <!-- Calculation Results -->
        <MetricCard metricValue={tradeResult.potentialProfit} message="Potential Profit" />
        <MetricCard metricValue={tradeResult.potentialLoss} message="Potential Loss" />
        <MetricCard metricValue={tradeResult.rRatio} message="R Ratio" />
    </div>
    <div class="mt-5 mb-3 mx-2">
        <h1 class="prose-2xl dark:prose-invert">Position Size</h1>
    </div>

    <div class="grid grid-cols-1 sm:grid-cols-2">
        <MetricCard
            metricValue={positionSizeRiskReward.positionSize}
            message="Final Position Size"
        />
        <MetricCard
            metricValue={positionSizeRiskReward.riskAmount}
            message="Position Size Risk Amount"
        />
        <MetricCard
            metricValue={positionSizeRiskReward.rewardAmount}
            message="Position Size Reward Amount"
        />
    </div>
</div>
