<script>
    export let metricValue;
    export let message;
</script>

<div class="rounded-lg bg-base-100 p-4 m-2 border border-primary">
    <p class="text-lg font-bold text-primary">
        {metricValue.toLocaleString()}
    </p>
    <p>{message}</p>
</div>
