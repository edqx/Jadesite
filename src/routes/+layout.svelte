<script lang="ts">
    import "virtual:windi.css";
    import { onDestroy, onMount } from "svelte";

    import { page } from "$app/stores";
    import DownArrow from "../icons/DownArrow.svelte";

    let scrollTop = 0;
    function onScroll(ev: Event) {
        scrollTop = document.documentElement.scrollTop;
    }

    onMount(() => {
        if (typeof document !== "undefined") document.addEventListener("scroll", onScroll);
        if (typeof document !== "undefined") scrollTop = document.documentElement.scrollTop;
    });

    onDestroy(() => {
        if (typeof document !== "undefined") document.removeEventListener("scroll", onScroll);
    });

    $: dark = $page.route.id === "/";

    let windowInnerWidth: number;
    let windowInnerHeight: number;
</script>

<svelte:head>
    <title>Jade</title>
</svelte:head>

<svelte:window bind:innerWidth={windowInnerWidth} bind:innerHeight={windowInnerHeight}></svelte:window>

<div class="h-screen lg:bg-transparent" class:bg-zinc-900={dark} class:bg-zinc-100={!dark}>
    <div class="font-sans" class:text-zinc-300={dark} class:text-zinc-700={!dark}>
        <div class="lg:my-42 pt-38 mx-16 flex flex-col gap-6 flex-1 items-center lg:items-start lg:fixed">
            <div class="flex items-end gap-2">
                <span class="text-7xl">Jade</span><span>(she/her)</span>
            </div>
            <div class="flex flex-col">
                <span class="text-2xl">Artist</span>
                <span class="text-2xl text-zinc-500">Writer</span>
                <span class="text-2xl" class:text-zinc-700={dark} class:text-zinc-300={!dark}>Game Developer</span>
                <span class="text-2xl" class:text-zinc-800={dark} class:text-zinc-200={!dark}>Graphic Designer</span>
            </div>
            <div class="text-zinc-500">
                <a href="mailto:jade@midlight.studio">jade@midlight.studio</a>
            </div>
        </div>
    </div>
    <div class="pb-24 lg:h-screen lg:mt-0" class:bg-zinc-900={dark} class:bg-zinc-100={!dark}></div>
</div>
<div
    class="z-1 sticky top-0 w-full flex justify-center items-center -mt-48"
    class:text-zinc-300={dark} class:text-zinc-700={!dark}
    class:border-zinc-700={dark} class:border-zinc-300={!dark}
    class:border-b-1={scrollTop > windowInnerHeight - 128}
    class:bg-zinc-900={dark && (windowInnerWidth < 1024 || scrollTop > windowInnerHeight - 128)}
    class:bg-zinc-100={!dark && (windowInnerWidth < 1024 || scrollTop > windowInnerHeight - 128)}
>
    <div class="flex flex-col justify-center items-center gap-2 sm:gap-8 p-2 sm:p-8">
        <div class="flex items-center sm:items-start">
            <a href="/" class="text-lg sm:text-2xl sm:border-r-1 px-4 sm:px-16 py-2"
                class:border-r-zinc-700={dark && windowInnerWidth > 640} class:border-r-zinc-300={!dark && windowInnerWidth > 640}
                class:text-zinc-500={$page.route.id !== "/"}>Personal</a>
            <a href="/college" class="text-lg sm:text-2xl  sm:border-l-1 sm:border-transparent px-4 sm:px-16 py-2"
                class:text-zinc-500={$page.route.id !== "/college"}>College</a>
        </div>
        <span class="ml-1 text-zinc-500" style="opacity: {1 - (scrollTop / 200)}"  class:hidden={scrollTop > 200}><DownArrow size={32}/></span>
    </div>
</div>
<div class:bg-zinc-900={dark} class:text-zinc-300={dark} class:bg-zinc-100={!dark} class:text-zinc-700={!dark}>
    <div class="h-9 sm:h-16" class:hidden={scrollTop <= 200}></div>
    <slot/>
</div>

<style global>
    * {
        transition: background-color 100ms linear, color 100ms linear;
    }
</style>