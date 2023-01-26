<script lang="ts">
    import "virtual:windi.css";
    import { onDestroy, onMount } from "svelte";

    import { page } from "$app/stores";
    import DownArrow from "../icons/DownArrow.svelte";

    function onZoneUpdate(ev: HashChangeEvent) {
        console.log(ev);
    }

    let scrollTop = 0;
    function onScroll(ev: Event) {
        scrollTop = document.documentElement.scrollTop;
    }

    onMount(() => {
        if (typeof window !== "undefined") window.onhashchange = onZoneUpdate;
        if (typeof document !== "undefined") document.addEventListener("scroll", onScroll);
        if (typeof document !== "undefined") scrollTop = document.documentElement.scrollTop;
    });

    onDestroy(() => {
        if (typeof window !== "undefined") window.onhashchange = null;
        if (typeof document !== "undefined") document.removeEventListener("scroll", onScroll);
    });

    let windowInnerWidth: number;
    let windowInnerHeight: number;
</script>

<svelte:head>
    <title>Jade</title>
</svelte:head>

<svelte:window bind:innerWidth={windowInnerWidth} bind:innerHeight={windowInnerHeight}></svelte:window>

<div class="bg-zinc-900 h-screen sm:bg-transparent">
    <div class="font-sans bg-zinc-900 text-zinc-300">
        <div class="lg:my-42 pt-38 mx-16 flex flex-col gap-6 flex-1 items-center lg:items-start lg:fixed">
            <div class="flex items-end gap-2">
                <span class="text-7xl">Jade</span><span class="text-zinc-700">(she/her)</span>
            </div>
            <div class="flex flex-col">
                <span class="text-2xl">Artist</span>
                <span class="text-2xl text-zinc-500">Writer</span>
                <span class="text-2xl text-zinc-700">Game Developer</span>
                <span class="text-2xl text-zinc-800">Graphic Designer</span>
            </div>
            <div class="text-zinc-500">
                <a href="mailto:jade@midlight.studio">jade@midlight.studio</a>
            </div>
        </div>
    </div>
    <div class="pb-24 bg-zinc-900 lg:h-screen lg:mt-0"></div>
</div>
<div
    class="z-1 sticky top-0 w-full flex justify-center items-center -mt-48 text-zinc-300 border-zinc-700" 
    class:border-b-1={scrollTop > windowInnerHeight - 128}
    class:bg-zinc-900={windowInnerWidth < 1024 || scrollTop > windowInnerHeight - 128}
>
    <div class="flex flex-col justify-center items-center gap-2 sm:gap-8 p-2 sm:p-8">
        <div class="flex items-center sm:items-start">
            <a href="/" class="text-lg sm:text-2xl sm:border-r-1 sm:border-r-zinc-700 px-4 sm:px-16 py-2" class:text-zinc-500={$page.route.id !== "/"}>Personal</a>
            <a href="/college" class="text-lg sm:text-2xl  sm:border-l-1 sm:border-transparent px-4 sm:px-16 py-2" class:text-zinc-500={$page.route.id !== "/college"}>College</a>
        </div>
        <span class="ml-1 text-zinc-500" style="opacity: {1 - (scrollTop / 200)}"  class:hidden={scrollTop > 200}><DownArrow size={32}/></span>
    </div>
</div>
<div class="bg-zinc-900 text-zinc-300">
    <div class="h-9 sm:h-16" class:hidden={scrollTop <= 200}></div>
    <slot/>
</div>