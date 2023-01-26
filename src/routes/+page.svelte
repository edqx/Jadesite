<script lang="ts">
    import { onDestroy, onMount } from "svelte";
    import { goto } from "$app/navigation";
    import { browser } from "$app/environment";
    import ViewableImage from "./ViewableImage.svelte";
    import Grid from "./Grid.svelte";
    import Cell from "./Cell.svelte";

    let projectSectionElements: HTMLDivElement[] = [];
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
</script>

<svelte:head>
    <title>Personal | Jade</title>
</svelte:head>

<svelte:window bind:innerHeight={windowInnerHeight}></svelte:window>

<div class="w-full flex flex-col items-center pt-32">
    <div class="ml-38 relative flex flex-col">
        <div class="absolute -top-32" id="edith" bind:this={projectSectionElements[0]}></div>
        <div class="flex gap-16">
            <div class="w-[30rem]">
                <span class="text-4xl">Edith</span>
                <p>
                    Edith Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla nec laoreet dui. Sed posuere ex vel augue ornare, non euismod ipsum imperdiet. Maecenas quis felis tempor, fringilla elit sed, eleifend mi. Vivamus quis efficitur nulla. Donec ac molestie lorem, imperdiet interdum ipsum. Nulla vestibulum arcu ut accumsan mattis. Phasellus tristique risus quis augue convallis porttitor. Fusce consectetur non libero et semper. Sed sagittis consectetur orci sed finibus. Suspendisse a interdum risus. Sed aliquam tellus vitae interdum rutrum. Aenean sodales arcu metus, vitae dictum ipsum bibendum vitae. Nulla vel velit laoreet, ultrices justo at, suscipit est. Aliquam volutpat semper lacinia.

                    Etiam mattis leo lacus. Aliquam eget felis ac felis dapibus pharetra. Suspendisse potenti. Cras ultrices diam ut ante convallis placerat sit amet ut tortor. Nulla hendrerit leo eu lectus aliquet venenatis. Phasellus nulla tellus, sagittis vel lobortis eu, egestas et elit. Curabitur pulvinar nisl dui, a interdum lorem placerat sed. Vestibulum sed tincidunt sem. Sed sem arcu, pretium at rutrum sit amet, finibus sit amet lorem. Etiam blandit lobortis nisl. Phasellus purus odio, rhoncus quis nisi a, vulputate egestas est. Proin ornare purus ac accumsan ultricies. Phasellus et cursus risus, sed posuere turpis. 
                </p>
            </div>
            <div class="w-[42rem]">
                <Grid cols={5} rows={12}>
                    <Cell col={1} row={1} colSpan={4} rowSpan={3}>
                        <ViewableImage alt="OC character Cluo leaning" src="cluolean.png">
                            Cluo is my baby, as you can see from this image
                        </ViewableImage>
                    </Cell>
                    <Cell col={5} row={1} colSpan={1} rowSpan={3}>
                        <div class="mt-auto">
                            <ViewableImage alt="OC character Macula in both male and female versions" src="macula.png">
                                Macula is a little itty bitty spider who climbed up the water spout
                            </ViewableImage>
                        </div>
                    </Cell>
                    <Cell col={3} row={4} colSpan={3} rowSpan={5}>
                        <ViewableImage alt="Draft art showing various emotions for OC character Cluo" src="cluoemotions.png">
                            Bipolar Cluo designs
                        </ViewableImage>
                    </Cell>
                    <Cell col={1} row={4} colSpan={2} rowSpan={6}>
                        <div class="flex flex-col gap-2">
                            <ViewableImage alt="OC character Cluo in various poses and stages" src="cluopipleine.png">
                                I wanna know, have you ever seen the rain
                            </ViewableImage>
                            <ViewableImage alt="Draft art for video game end scene" src="gameover.png">
                                A dreaded sunny day
                            </ViewableImage>
                            <ViewableImage alt="OC character Iris in various styles" src="iris.png">
                                Some description
                            </ViewableImage>
                        </div>
                    </Cell>
                    <Cell col={3} row={7} colSpan={3} rowSpan={3}>
                        <ViewableImage alt="OC character camina" src="camina.png">
                            Camina progressing through the human evolutionary process
                        </ViewableImage>
                    </Cell>
                </Grid>
            </div>
        </div>
    </div>
    <div class="ml-38 relative flex flex-col">
        <div class="absolute -top-32" id="animation" bind:this={projectSectionElements[1]}></div>
        <div class="flex gap-16">
            <div class="w-[30rem]">
                <span class="text-4xl">Animation</span>
                <p>
                    Edith Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla nec laoreet dui. Sed posuere ex vel augue ornare, non euismod ipsum imperdiet. Maecenas quis felis tempor, fringilla elit sed, eleifend mi. Vivamus quis efficitur nulla. Donec ac molestie lorem, imperdiet interdum ipsum. Nulla vestibulum arcu ut accumsan mattis. Phasellus tristique risus quis augue convallis porttitor. Fusce consectetur non libero et semper. Sed sagittis consectetur orci sed finibus. Suspendisse a interdum risus. Sed aliquam tellus vitae interdum rutrum. Aenean sodales arcu metus, vitae dictum ipsum bibendum vitae. Nulla vel velit laoreet, ultrices justo at, suscipit est. Aliquam volutpat semper lacinia.

                    Etiam mattis leo lacus. Aliquam eget felis ac felis dapibus pharetra. Suspendisse potenti. Cras ultrices diam ut ante convallis placerat sit amet ut tortor. Nulla hendrerit leo eu lectus aliquet venenatis. Phasellus nulla tellus, sagittis vel lobortis eu, egestas et elit. Curabitur pulvinar nisl dui, a interdum lorem placerat sed. Vestibulum sed tincidunt sem. Sed sem arcu, pretium at rutrum sit amet, finibus sit amet lorem. Etiam blandit lobortis nisl. Phasellus purus odio, rhoncus quis nisi a, vulputate egestas est. Proin ornare purus ac accumsan ultricies. Phasellus et cursus risus, sed posuere turpis. 
                </p>
            </div>
            <div class="w-[42rem]">
                <Grid cols={5} rows={2}>
                    <img width={128} alt="pixel art animation showing OC character Cluo attacking" class="image-render-pixel" src="/characters/cluo/cluo_attack_sheet.png.gif">
                    <img width={128} alt="pixel art animation showing OC character Cluo breathing" class="image-render-pixel" src="/characters/cluo/cluo_breathe_sheet.png.gif">
                    <img width={128} alt="pixel art animation showing OC character Cluo crouching" class="image-render-pixel" src="/characters/cluo/cluo_crouch_sheet.png.gif">
                    <img width={128} alt="pixel art animation showing OC character Cluo falling" class="image-render-pixel" src="/characters/cluo/cluo_fall_sheet.png.gif">
                    <img width={128} alt="pixel art animation showing OC character Cluo using her frenzy attack" class="image-render-pixel" src="/characters/cluo/cluo_frenzy_sheet.png.gif">
                    <img width={128} alt="pixel art animation showing OC character Cluo getting hurt" class="image-render-pixel" src="/characters/cluo/cluo_hurt_sheet.png.gif">
                    <img width={128} alt="pixel art animation showing OC character Cluo spinning her knife idly" class="image-render-pixel" src="/characters/cluo/cluo_idle_spin_sheet.png.gif">
                    <img width={128} alt="pixel art animation showing OC character Cluo jumping" class="image-render-pixel" src="/characters/cluo/cluo_jump_sheet.png.gif">
                </Grid>
                <Grid cols={5} rows={1}>
                    <img width={128} alt="pixel art animation showing OC character Jen attacking" class="image-render-pixel" src="/characters/jen/jen_attack_sheet.png.gif">
                    <img width={128} alt="pixel art animation showing OC character Jen breathing" class="image-render-pixel" src="/characters/jen/jen_breathe_sheet.png.gif">
                    <img width={128} alt="pixel art animation showing OC character Jen crouching" class="image-render-pixel" src="/characters/jen/jen_crouch_sheet.png.gif">
                    <img width={128} alt="pixel art animation showing OC character Jen healing" class="image-render-pixel" src="/characters/jen/jen_heal_sheet.png.gif">
                    <img width={128} alt="pixel art animation showing OC character Jen getting hurt" class="image-render-pixel" src="/characters/jen/jen_hurt_sheet.png.gif">
                    <img width={128} alt="pixel art animation showing OC character Jen jumping" class="image-render-pixel" src="/characters/jen/jen_jump_sheet.png.gif">
                </Grid>
                <Grid cols={5} rows={1}>
                    <img width={128} alt="pixel art animation showing OC character Hevel's dust cloud" class="image-render-pixel" src="/characters/hevel/hevel_dust_sheet.png.gif">
                    <img width={128} alt="pixel art animation showing OC character Hevel melting" class="image-render-pixel" src="/characters/hevel/hevel_melt_sheet.png.gif">
                    <img width={128} alt="pixel art animation showing OC character Hevel's spike attack" class="image-render-pixel" src="/characters/hevel/hevel_spike_sheet.png.gif">
                </Grid>
            </div>
        </div>
    </div>
    <div class="relative flex flex-col w-[58rem] mt-14">
        <div class="absolute -top-32" id="chicago" bind:this={projectSectionElements[2]}></div>
        <span class="text-4xl">Chicago</span>
        <p>
            To be, or not to be: that is the question:<br>
            Whether 'tis nobler in the mind to suffer<br>
            The slings and arrows of outrageous fortune,<br>
            Or to take arms against a sea of troubles,<br>
            And by opposing end them? To die: to sleep;<br>
            No more; and by a sleep to say we end<br>
            The heart-ache and the thousand natural shocks<br>
            That flesh is heir to, 'tis a consummation<br>
            Devoutly to be wish'd. To die, to sleep;<br>
            To sleep: perchance to dream: ay, there's the rub;<br>
            For in that sleep of death what dreams may come<br>
            When we have shuffled off this mortal coil,<br>
            Must give us pause: there's the respect<br>
            That makes calamity of so long life;<br>
            For who would bear the whips and scorns of time,<br>
            The oppressor's wrong, the proud man's contumely,<br>
            The pangs of despised love, the law's delay,<br>
            The insolence of office and the spurns<br>
            That patient merit of the unworthy takes,<br>
            When he himself might his quietus make<br>
            With a bare bodkin? who would fardels bear,<br>
            To grunt and sweat under a weary life,<br>
            But that the dread of something after death,<br>
            The undiscover'd country from whose bourn<br>
            No traveller returns, puzzles the will<br>
            And makes us rather bear those ills we have<br>
            Than fly to others that we know not of?<br>
            Thus conscience does make cowards of us all;<br>
            And thus the native hue of resolution<br>
            Is sicklied o'er with the pale cast of thought,<br>
            And enterprises of great pith and moment<br>
            With this regard their currents turn awry,<br>
            And lose the name of action.-Soft you now!<br>
            The fair Ophelia! Nymph, in thy orisons<br>
            Be all my sins remember'd.'
        </p>
    </div>
</div>