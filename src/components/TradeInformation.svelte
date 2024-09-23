<script>
    import NumberInput from "./NumberInput.svelte";
    import DollarInput from "./DollarInput.svelte";
    import SelectInput from "./SelectInput.svelte"; // Exports multiplier prop

    export let entryPrice = 0;
    export let profitTarget = 0;
    export let stopLoss = 0;
    export let contractSize = 0;
    export let quantity = 0;
    export let isLong = 1; // bool
</script>

<div>
    <SelectInput bind:multiplier={contractSize} id="contract-size" label="Instrument" />
    <NumberInput bind:value={entryPrice} id="entry-price" label="Entry Price" />
    <NumberInput bind:value={profitTarget} id="profit-target" label="Profit Target" />
    <NumberInput bind:value={stopLoss} id="stop-loss" label="Stop Loss" />
    <NumberInput bind:value={contractSize} id="contract-size" label="Contract Size" />
    <NumberInput bind:value={quantity} id="quantity" label="Quantity" />
    <NumberInput bind:value={isLong} id="is-long" label="Long Position? (bool - 1 or 0)" />
</div>
