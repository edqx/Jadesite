<script lang="ts">
    import { onDestroy, onMount } from "svelte";
    import { goto } from "$app/navigation";
    import { browser } from "$app/environment";

    let projectSectionElements: HTMLDivElement[] = [];
    let windowInnerWidth: number;
    let windowInnerHeight: number;

    function reverseArray<T>(array: T[]) {
        let reversedArray: T[] = [];
        for (let i = array.length - 1; i >= 0; i--) {
            reversedArray.push(array[i]);
        }
        return reversedArray;
    }

    let lastSectionInView: HTMLDivElement|undefined;
    function onScroll() {
        let sectionInView = reverseArray(projectSectionElements).find(section => {
            return section.getBoundingClientRect().top < windowInnerHeight / 2;
        });

        if (sectionInView !== lastSectionInView) {
            lastSectionInView = sectionInView;
        }
    }

    onMount(() => {
        if (typeof document !== "undefined") document.addEventListener("scroll", onScroll);
        onScroll();
    });

    onDestroy(() => {
        if (typeof document !== "undefined") document.removeEventListener("scroll", onScroll);
    });

    $: browser && goto(lastSectionInView ? "#" + lastSectionInView.id : "#", { replaceState: true, noScroll: true });

    let postersContainerElem: HTMLDivElement|undefined = undefined;
    let videoWidth = 0;
    let videoHeight = 0;

    $: if (windowInnerWidth && postersContainerElem) {
        videoWidth = postersContainerElem.getBoundingClientRect().width;
        videoHeight = videoWidth / (16 / 9);
    }
</script>

<svelte:head>
    <title>College | Jade</title>
</svelte:head>

<svelte:window bind:innerWidth={windowInnerWidth} bind:innerHeight={windowInnerHeight}></svelte:window>

<div class="w-full flex flex-col items-center pt-32">
    <div class="lg:ml-38 mb-42 relative flex flex-col">
        <div class="absolute -top-32" id="magazine" bind:this={projectSectionElements[0]}></div>
        <div class="flex items-center flex-col xl:items-start xl:flex-row gap-16">
            <div class="mx-8 sm:mx-0 sm:w-[30rem]">
                <span class="text-4xl">Magazine Project</span>
                <p>
                    Edith Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla nec laoreet dui. Sed posuere ex vel augue ornare, non euismod ipsum imperdiet. Maecenas quis felis tempor, fringilla elit sed, eleifend mi. Vivamus quis efficitur nulla. Donec ac molestie lorem, imperdiet interdum ipsum. Nulla vestibulum arcu ut accumsan mattis. Phasellus tristique risus quis augue convallis porttitor. Fusce consectetur non libero et semper. Sed sagittis consectetur orci sed finibus. Suspendisse a interdum risus. Sed aliquam tellus vitae interdum rutrum. Aenean sodales arcu metus, vitae dictum ipsum bibendum vitae. Nulla vel velit laoreet, ultrices justo at, suscipit est. Aliquam volutpat semper lacinia.

                    Etiam mattis leo lacus. Aliquam eget felis ac felis dapibus pharetra. Suspendisse potenti. Cras ultrices diam ut ante convallis placerat sit amet ut tortor. Nulla hendrerit leo eu lectus aliquet venenatis. Phasellus nulla tellus, sagittis vel lobortis eu, egestas et elit. Curabitur pulvinar nisl dui, a interdum lorem placerat sed. Vestibulum sed tincidunt sem. Sed sem arcu, pretium at rutrum sit amet, finibus sit amet lorem. Etiam blandit lobortis nisl. Phasellus purus odio, rhoncus quis nisi a, vulputate egestas est. Proin ornare purus ac accumsan ultricies. Phasellus et cursus risus, sed posuere turpis. 
                    <br><br>
                    <a class="hover:underline" href="https://docs.google.com/presentation/d/1d-APPx1bwGE_9T6ASdWYTzbLSc5M-MJvLn39odNTzKI/edit?usp=sharing">Presentation</a>
                </p>
            </div>
            <div class="flex flex-col gap-2 2xl:w-[42rem] sm:w-[28rem] w-[20rem]">
                <img src="/Cover_1_Jay.3.png"/>
                <img src="/Page_1_Jay.png"/>
            </div>
        </div>
    </div>
    <div class="lg:ml-38 mb-38 relative flex flex-col">
        <div class="absolute -top-32" id="advertisign" bind:this={projectSectionElements[1]}></div>
        <div class="flex items-center flex-col xl:items-start xl:flex-row gap-16">
            <div class="mx-8 sm:mx-0 sm:w-[30rem]">
                <span class="text-4xl">Advertising Project</span>
                <p>
                    Edith Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla nec laoreet dui. Sed posuere ex vel augue ornare, non euismod ipsum imperdiet. Maecenas quis felis tempor, fringilla elit sed, eleifend mi. Vivamus quis efficitur nulla. Donec ac molestie lorem, imperdiet interdum ipsum. Nulla vestibulum arcu ut accumsan mattis. Phasellus tristique risus quis augue convallis porttitor. Fusce consectetur non libero et semper. Sed sagittis consectetur orci sed finibus. Suspendisse a interdum risus. Sed aliquam tellus vitae interdum rutrum. Aenean sodales arcu metus, vitae dictum ipsum bibendum vitae. Nulla vel velit laoreet, ultrices justo at, suscipit est. Aliquam volutpat semper lacinia.

                    Etiam mattis leo lacus. Aliquam eget felis ac felis dapibus pharetra. Suspendisse potenti. Cras ultrices diam ut ante convallis placerat sit amet ut tortor. Nulla hendrerit leo eu lectus aliquet venenatis. Phasellus nulla tellus, sagittis vel lobortis eu, egestas et elit. Curabitur pulvinar nisl dui, a interdum lorem placerat sed. Vestibulum sed tincidunt sem. Sed sem arcu, pretium at rutrum sit amet, finibus sit amet lorem. Etiam blandit lobortis nisl. Phasellus purus odio, rhoncus quis nisi a, vulputate egestas est. Proin ornare purus ac accumsan ultricies. Phasellus et cursus risus, sed posuere turpis. 
                </p>
            </div>
            <div class="flex flex-col gap-2 2xl:w-[42rem] sm:w-[28rem] w-[20rem]">
                <div class="grid gap-1 grid-cols-3" bind:this={postersContainerElem}>
                    <img src="/alien-boy.png"/>
                    <img src="/twcftw.png"/>
                    <img src="/utopia.png"/>    
                </div>
                <div>
                    <iframe width={videoWidth} height={videoHeight} src="https://www.youtube.com/embed/ehBbexwnfn8"></iframe>
                </div>
            </div>
        </div>
    </div>
</div>