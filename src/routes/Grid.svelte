<script lang="ts">
    export let cols: number;
    export let rows: number;

    export let centered = false;
</script>

<div class="grid gap-2" class:items-center={centered} style="grid-template-columns: repeat({cols}, minmax(0, 1fr)); grid-template-rows: repeat({rows}, minmax(0, 1fr));">
    <slot/>
</div>