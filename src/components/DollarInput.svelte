<script>
    export let id;
    export let label;
    export let value = 0;
</script>

<div class="mb-3 flex flex-col w-full max-w-sm">
    <label for={id} class="prose mb-1">
        {label}
    </label>
    <input
        type="number"
        {id}
        min={0}
        bind:value
        class="input input-bordered input-primary"
        placeholder="$0"
    />
</div>
