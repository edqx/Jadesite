<script lang="ts">
    import { onMount, onDestroy } from "svelte";
    export let cols: number;
    let collageElem: HTMLDivElement|undefined = undefined;

    interface GridElem {
        gridStartCol: number;
        gridStartRow: number;
        gridEndCol: number;
        gridEndRow: number;
        elem: HTMLDivElement;
    }

    let grid: (GridElem|null)[][] = [];

    function getAspectRatio(elem: Element) {
        const bounds = elem.getBoundingClientRect();
        elem.setAttribute("ar", (bounds.width / bounds.height).toString());
        return bounds.width / bounds.height;
    }

    function createNewRows(newRows: number) {
        for (let i = 0; i < newRows; i++) {
            grid.push(new Array(cols).fill(null));
        }
    }

    function doesFitIn(colsStart: number, rowsStart: number, colsSpan: number, rowsSpan: number) {
        for (let row = 0; row < rowsSpan; row++) {
            if (!grid[rowsStart + row])
                return false;

            for (let col = 0; col < colsSpan; col++) {
                if (grid[rowsStart + row][colsStart + col] !== null)
                    return false;
            }
        }

        return true;
    }

    function fitIn(colsStart: number, rowsStart: number, colsSpan: number, rowsSpan: number, elem: HTMLDivElement) {
        for (let row = 0; row < rowsSpan; row++) {
            for (let col = 0; col < colsSpan; col++) {
                grid[row][col] = {
                    gridStartCol: colsStart,
                    gridStartRow: rowsStart,
                    gridEndRow: rowsStart + rowsSpan,
                    gridEndCol: colsStart + colsSpan,
                    elem
                };
            }
        }
    }

    function attemptToFit(elem: HTMLDivElement) {
        const aspectRatio = getAspectRatio(elem);
        const colsSpanF = Math.min(cols, Math.max(1, (cols / 2) * aspectRatio));
        const rowsSpanF = Math.max(1, colsSpanF / aspectRatio);

        const colsSpan = Math.floor(colsSpanF);
        const rowsSpan = Math.ceil(rowsSpanF);

        for (let row = 0; row < grid.length; row++) {
            for (let col = 0; col < grid[row].length; col++) {
                if (grid[row][col] === null) {
                    if (doesFitIn(col, row, colsSpan, rowsSpan)) {
                        console.log(col, row, colsSpan, rowsSpan);
                        fitIn(col, row, colsSpan, rowsSpan, elem);
                        return;
                    }
                }
            }
        }

        createNewRows(rowsSpan);
        fitIn(0, grid.length - rowsSpan, colsSpan, rowsSpan, elem);
    }

    export function refreshLayout() {
        if (collageElem === undefined)
            return;

        grid = [];
        const allChildren = Array.from(collageElem.querySelectorAll(":scope > div")) as HTMLDivElement[];
        let averageAspectRatio = allChildren.reduce((prev, cur) => prev + getAspectRatio(cur), 0) / allChildren.length;

        for (const child of allChildren) {
            attemptToFit(child);
        }

        rerenderGrid();
    }

    export function rerenderGrid() {
        const rendered: Set<HTMLDivElement> = new Set;
        for (const row of grid) {
            for (const cell of row) {
                if (!cell)
                    continue;

                if (rendered.has(cell.elem))
                    continue;

                cell.elem.style.gridColumnStart = cell.gridStartCol.toString();
                cell.elem.style.gridRowStart = cell.gridStartRow.toString();
                cell.elem.style.gridColumnEnd = cell.gridEndCol.toString();
                cell.elem.style.gridRowEnd = cell.gridEndRow.toString();
                rendered.add(cell.elem);
            }
        }
    }

    onMount(() => {
        if (typeof window !== "undefined")
            window.addEventListener("resize", refreshLayout, false)
    })

    onDestroy(() => {
        if (typeof window !== "undefined")
            window.removeEventListener("resize", refreshLayout, false)
    });
      
    $: if (collageElem) { 
        refreshLayout();
    }
</script>

<div bind:this={collageElem} class="grid" style="grid-template-columns: repeat({cols}, 1fr);">
    <slot/>
</div>