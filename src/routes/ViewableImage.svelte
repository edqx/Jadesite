<script lang="ts">
  import { onDestroy } from "svelte";

    export let src: string;
    export let alt: string;

    let isOpen = false;
    let smallImageElem: HTMLImageElement|undefined = undefined;
    let popupImageElem: HTMLImageElement|undefined = undefined;
    let windowWidth = 0;
    let windowHeight = 0;

    $: if (smallImageElem && popupImageElem && windowWidth > 0 && windowHeight > 0) {
        const aspectRatio = smallImageElem.width / smallImageElem.height;

        const defaultWidth = windowWidth * 0.8;
        const defaultHeight = defaultWidth / aspectRatio;

        const maxHeight = windowHeight * 0.8;
        const adjustedWidth = maxHeight * aspectRatio;
        if (defaultHeight > maxHeight) {
            popupImageElem.style.width = adjustedWidth + "px";
            popupImageElem.style.height = maxHeight + "px";
        } else {
            popupImageElem.style.width = defaultWidth + "px";
            popupImageElem.style.height = defaultHeight + "px";
        }
    }

    function openPopup() {
        isOpen = true;
        document.body.style.overflow = "hidden";
    }

    function closePopup() {
        isOpen = false;
        document.body.style.overflow = "auto";
    }

    onDestroy(() => {
        if (isOpen)
            closePopup();
    });
</script>

<svelte:window bind:innerWidth={windowWidth} bind:innerHeight={windowHeight}/>

<div class="flex flex-col gap-4 cursor-pointer" on:click={openPopup} on:keypress={ev => ev.keyCode === 13 && openPopup()}>
    <img class="w-[38rem]" bind:this={smallImageElem} {src} {alt}/>
</div>

<div class="fixed flex left-0 top-0 w-screen h-screen z-50 bg-dark-900/95 flex-col items-center justify-center gap-2 cursor-pointer" class:hidden={!isOpen} on:click={closePopup} on:keypress={closePopup}>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <img class="cursor-default" bind:this={popupImageElem} {src} {alt} on:click={ev => ev.stopPropagation()}/>
    <div class="text-xl italic">
        <slot/>
    </div>
</div>