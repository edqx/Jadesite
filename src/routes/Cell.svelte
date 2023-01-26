<script lang="ts">
    export let col: number;
    export let row: number;

    export let colSpan = 0;
    export let rowSpan = 0;
</script>

<div class="grid" style="grid-column-start: {col}; grid-column-end: {col + colSpan}; grid-row-start: {row}; grid-row-end: {row + rowSpan}">
    <slot/>
</div>