<script lang="ts">
    import "virtual:windi.css";

    import { page } from "$app/stores";
    import DownArrow from "../icons/DownArrow.svelte";

    $: console.log($page);
</script>

<div class="w-full h-screen flex flex-col font-sans bg-zinc-900 text-zinc-300">
    <div class="my-32 mx-16 flex flex-col gap-6 flex-1">
        <div class="flex items-end gap-2">
            <span class="text-7xl">Jade</span><span class="text-zinc-700">(she/her)</span>
        </div>
        <div class="flex flex-col">
            <span class="text-2xl">Artist</span>
            <span class="text-2xl text-zinc-500">Writer</span>
            <span class="text-2xl text-zinc-700">Game Developer</span>
            <span class="text-2xl text-zinc-800">Graphic Designer</span>
        </div>
    </div>
    <div class="flex justify-center flex-col items-center gap-8 m-8 mb-24">
        <div class="flex flex-col items-center sm:flex-row sm:items-start">
            <a href="/" class="text-2xl sm:border-r-1 sm:border-r-zinc-500 px-16" class:text-zinc-500={$page.route.id !== "/"}>Personal</a>
            <a href="/college" class="text-2xl sm:border-l-1 sm:border-transparent px-16" class:text-zinc-500={$page.route.id !== "/college"}>College</a>
        </div>
        <span class="text-2xl text-zinc-500"><DownArrow size={32}/></span>
    </div>
</div>

<slot/>