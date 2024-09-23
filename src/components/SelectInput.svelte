<script>
    export let id;
    export let label;
    export let multiplier;

    const contractOptions = [
        { name: "Select", multiplier: 1 },
        { name: "Micro Nasdaq", multiplier: 2 },
        { name: "Micro Gold", multiplier: 10 },
        { name: "Micro Crude", multiplier: 100 },
    ];
    // Initialize the selected value and multiplier
    let selectedContract = contractOptions[0].name;
    multiplier = contractOptions[0].multiplier;

    // Function to update the multiplier when selection changes
    function handleSelection() {
        const selected = contractOptions.find((option) => option.name === selectedContract);
        multiplier = selected.multiplier;
    }
</script>

<div class="mb-3 flex flex-col w-full max-w-sm">
    <label for={id} class="prose mb-1">
        {label}
    </label>
    <select
        {id}
        bind:value={selectedContract}
        on:change={handleSelection}
        class="select select-bordered w-full max-w-xs"
    >
        {#each contractOptions as option}
            <option value={option.name}>{option.name}</option>
        {/each}
    </select>
</div>
