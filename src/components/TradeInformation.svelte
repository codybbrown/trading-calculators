<script>
    import NumberInput from "./NumberInput.svelte";
    export let entryPrice = 0;
    export let profitTarget = 0;
    export let stopLoss = 0;
    export let contractSize = 0;
    export let quantity = 0;
    export let isLong = 1; // bool
</script>

<div>
    <NumberInput bind:value={entryPrice} id="entry-price" label="Entry Price" />
    <NumberInput bind:value={profitTarget} id="profit-target" label="Profit Target" />
    <NumberInput bind:value={stopLoss} id="entry-price" label="Stop Loss" />
    <NumberInput bind:value={contractSize} id="entry-price" label="Contract Size" />
    <NumberInput bind:value={quantity} id="entry-price" label="Quantity" />
    <NumberInput bind:value={isLong} id="entry-price" label="Long Position? (bool - 1 or 0)" />
</div>
