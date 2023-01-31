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
    <div class="lg:ml-38 relative flex flex-col">
        <div class="absolute -top-32" id="edith" bind:this={projectSectionElements[0]}></div>
        <div class="flex items-center flex-col xl:items-start xl:flex-row gap-16">
            <div class="mx-8 sm:mx-0 sm:w-[30rem]">
                <span class="text-4xl">Edith - Concept Art Examples</span>
                <p>
                    To the right are just a few samples of concept art drawn for characters in a project going by the name "Edith". Edith is a passion project started by myself and a very close friend of mine and is currently one year into development, with it's demo a very early work in progress. Inspired by OMOCAT's "OMORI", Edith is a top-down RPG loveletter to the aformentioned title, with my primary role in its creation being art direction for both final pieces along with concept artwork and designs (with a secondary but still large focus on story and character development). The images to the right are clickable, and should display a small and relevant caption. The date at which each piece of concept art was made is written in red pen to give an idea as to which are early works and which are more recent.
                </p>
            </div>
            <div class="2xl:w-[42rem] sm:w-[28rem] w-[20rem]">
                <Grid cols={5} rows={12}>
                    <Cell col={1} row={1} colSpan={4} rowSpan={3}>
                        <ViewableImage alt="OC character Cluo leaning" src="cluolean.png">
                            One of the more dynamic poses I referenced for Edith's deuteragonist, 'Cluo', including two slighly different designs, concepted to show small differences in her appearence that might be made depending on what difficulty the game is set at.
                        </ViewableImage>
                    </Cell>
                    <Cell col={5} row={1} colSpan={1} rowSpan={3}>
                        <div class="mt-auto">
                            <ViewableImage alt="OC character Macula in both male and female versions" src="macula.png">
                                Some "finalised" artwork of Edith's protagonist, 'Macula', when considering letting the player pick their gender. It was eventually decided, however, that the left design would be used.
                            </ViewableImage>
                        </div>
                    </Cell>
                    <Cell col={3} row={4} colSpan={3} rowSpan={5}>
                        <ViewableImage alt="Draft art showing various emotions for OC character Cluo" src="cluoemotions.png">
                            The first ever concept drawings done for Edith, an emotion sheet showing a gameplay mechanic dubbed "patience". This was the first of many emotion charts I ended up drawing for Edith.
                        </ViewableImage>
                    </Cell>
                    <Cell col={1} row={4} colSpan={2} rowSpan={6}>
                        <div class="flex flex-col gap-2">
                            <ViewableImage alt="OC character Cluo in various poses and stages" src="cluopipleine.png">
                                A page showing some progression of how I choose to draw Edith's concept art, along with some processes of how I take an older design and modernise them with my updated drawing style.
                            </ViewableImage>
                            <ViewableImage alt="Draft art for video game end scene" src="gameover.png">
                                Unfinished concept art for the pose taken by Cluo during a proposed "Game Over" screen. The intention would be that her hand be hovering over an analogue clock, though I'm still yet to finish this.
                            </ViewableImage>
                            <ViewableImage alt="OC character Iris in various styles" src="iris.png">
                                The difference in only a few months work in designing one of Edith's bosses, "Iris". After a new idea for her design along with some new skills, this is probably one of my best modernisations of older artwork.
                            </ViewableImage>
                        </div>
                    </Cell>
                    <Cell col={3} row={7} colSpan={3} rowSpan={3}>
                        <ViewableImage alt="OC character camina" src="camina.png">
                            Despite the artwork being quite dated at this point in time, I'd still like to show this one as it's evidence of how I used to (and largely still do) refine my artwork, by drawing over it a lot until I'm happy with it. It's an ineffecient process that I'm trying to stop, but for now it helps me get my ideas across.
                        </ViewableImage>
                    </Cell>
                </Grid>
            </div>
        </div>
    </div>
    <div class="lg:ml-38 mb-38 relative flex flex-col">
        <div class="absolute -top-32" id="animation" bind:this={projectSectionElements[1]}></div>
        <div class="flex items-center flex-col xl:items-start xl:flex-row gap-16">
            <div class="mx-8 sm:mx-0 sm:w-[30rem]">
                <span class="text-4xl">Edith - Spritework Examples</span>
                <p>
                     To the right are some examples of the in-game spritework test animations done for the previously mentioned early unpolished demo currently being worked on for Edith, along with a screen recording containing some of them actually being used. These animations include: breathing, idling, attacking, jumping and crouching motions, as well as taking damage. While they don't look particuarly animated on their own, however once given context with each other, they flow well into one another for the type of gameplay we hope Edith is going to have. Some older attempts at these animations should be seen below the screen recording.
                </p>
            </div>
            <div class="2xl:w-[42rem] sm:w-[28rem] w-[20rem]">
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
                <div class="mt-4">
                    <ViewableImage src="/edithdemoexaxmple.gif" alt="Demo of game showing animations in action">
                    </ViewableImage>
                </div>
            </div>
        </div>
    </div>
    <div class="lg:ml-38 mb-38 relative flex flex-col">
        <div class="absolute -top-32" id="animation" bind:this={projectSectionElements[1]}></div>
        <div class="flex items-center flex-col xl:items-start xl:flex-row gap-16">
            <div class="mx-8 sm:mx-0 sm:w-[30rem]">
                <span class="text-4xl">(OLD) Edith - Spritework Examples</span>
                <p>
                     To the right are some examples of the in-game spritework test animations done for the previously mentioned early unpolished demo currently being worked on for Edith, along with a screen recording containing some of them actually being used. These animations include: breathing, idling, attacking, jumping and crouching motions, as well as taking damage. While they don't look particuarly animated on their own, however once given context with each other, they flow well into one another for the type of gameplay we hope Edith is going to have. Some older attempts at these animations should be seen below the screen recording.
                </p>
            </div>
            <div class="2xl:w-[42rem] sm:w-[28rem] w-[20rem]">
                <Grid cols={5} rows={2}>
                    <img width={128} alt="a higher-resolution pixel art animation showing OC character Cluo attacking" class="image-render-pixel" src="/old_animations/cluo_attack_old.gif">
                    <img width={128} alt="a higher-resolution pixel art animation showing OC character Cluo crouching" class="image-render-pixel" src="/old_animations/cluo_crouch_old.gif">
                    <img width={128} alt="a higher-resolution pixel art animation showing OC character Cluo using her frenzy attack" class="image-render-pixel" src="/old_animations/cluo_frenzy_full_old.gif">
                    <img width={128} alt="a higher-resolution pixel art animation showing OC character Cluo getting hurt" class="image-render-pixel" src="/old_animations/cluo_hurt_old.gif">
                    <img width={128} alt="a higher-resolutionpixel art animation showing OC character Cluo spinning her knife idly" class="image-render-pixel" src="/old_animations/cluo_idle_old.gif">
                    <img width={128} alt="a higher-resolutionpixel art animation showing OC character Cluo jumping" class="image-render-pixel" src="/old_animations/cluo_jump_old.gif">
                </Grid>
                <Grid cols={5} rows={1} centered={true}>
                    <img width={128} alt="a higher-resolution pixel art animation showing OC character Jen attacking" class="image-render-pixel" src="/old_animations/jen_attack_old.gif">
                    <img width={128} alt="a higher-resolution pixel art animation showing OC character Jen crouching" class="image-render-pixel" src="/old_animations/jen_crouch_old.gif">
                    <img width={128} alt="a higher-resolution pixel art animation showing OC character Jen healing" class="image-render-pixel" src="/old_animations/jen_heal_old.gif">
                    <img width={128} alt="a higher-resolution pixel art animation showing OC character Jen getting hurt" class="image-render-pixel" src="/old_animations/jen_hurt_old.gif">
                    <img width={128} alt="a higher-resolution pixel art animation showing OC character Jen dripping paint from her paint brush idly" class="image-render-pixel" src="/old_animations/jen_idle_old.gif">
                    <img width={128} alt="a higher-resolutionpixel art animation showing OC character Jen jumping" class="image-render-pixel" src="/old_animations/jen_jump_old.gif">
                </Grid>
                <div class="mt-4">
                    <ViewableImage src="/old_animations/edithdemoexampleold.gif" alt="Demo of game showing animations in action">
                    </ViewableImage>
                </div>
            </div>
        </div>
    </div>
    <div class="lg:ml-38 relative flex flex-col">
        <div class="absolute -top-32" id="misc" bind:this={projectSectionElements[2]}></div>
        <div class="flex items-center flex-col xl:items-start xl:flex-row gap-16">
            <div class="mx-8 sm:mx-0 sm:w-[30rem]">
                <span class="text-4xl">Misc</span>
                <p>
                    Edithy Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla nec laoreet dui. Sed posuere ex vel augue ornare, non euismod ipsum imperdiet. Maecenas quis felis tempor, fringilla elit sed, eleifend mi. Vivamus quis efficitur nulla. Donec ac molestie lorem, imperdiet interdum ipsum. Nulla vestibulum arcu ut accumsan mattis. Phasellus tristique risus quis augue convallis porttitor. Fusce consectetur non libero et semper. Sed sagittis consectetur orci sed finibus. Suspendisse a interdum risus. Sed aliquam tellus vitae interdum rutrum. Aenean sodales arcu metus, vitae dictum ipsum bibendum vitae. Nulla vel velit laoreet, ultrices justo at, suscipit est. Aliquam volutpat semper lacinia.

                    Etiam mattis leo lacus. Aliquam eget felis ac felis dapibus pharetra. Suspendisse potenti. Cras ultrices diam ut ante convallis placerat sit amet ut tortor. Nulla hendrerit leo eu lectus aliquet venenatis. Phasellus nulla tellus, sagittis vel lobortis eu, egestas et elit. Curabitur pulvinar nisl dui, a interdum lorem placerat sed. Vestibulum sed tincidunt sem. Sed sem arcu, pretium at rutrum sit amet, finibus sit amet lorem. Etiam blandit lobortis nisl. Phasellus purus odio, rhoncus quis nisi a, vulputate egestas est. Proin ornare purus ac accumsan ultricies. Phasellus et cursus risus, sed posuere turpis. 
                </p>
            </div>
            <div class="2xl:w-[42rem] sm:w-[28rem] w-[20rem]">
                <Grid cols={5} rows={30}>
                    <Cell col={1} row={1} colSpan={1} rowSpan={8}>
                        <div class="mt-auto">
                            <ViewableImage alt="A scene showing a reflection between two sides of the character Madeline from Celeste's psyche" src="celeste1.png">
                                Lorem ipsum
                            </ViewableImage>
                        </div>
                    </Cell>
                    <Cell col={2} row={1} colSpan={2} rowSpan={8}>
                        <ViewableImage alt="A scene showing a reflection between two sides of the character Madeline from Celeste's psyche" src="celeste2.png">
                            Lorem ipsum
                        </ViewableImage>
                    </Cell>
                    <Cell col={4} row={1} colSpan={1} rowSpan={8}>
                        <div class="mt-auto">
                            <ViewableImage alt="Character Madeline from Celeste battling her alter-ego with a golden feather" src="celeste3.png">
                                Lorem ipsum
                            </ViewableImage>
                        </div>
                    </Cell>
                    <Cell col={5} row={1} colSpan={1} rowSpan={8}>
                        <div class="mt-auto">
                            <ViewableImage alt="Character Madeline from Celeste battling her alter-ego with a golden feather" src="celeste4.png">
                                Lorem ipsum
                            </ViewableImage>
                        </div>
                    </Cell>
                    <Cell col={1} row={9} colSpan={2} rowSpan={8}>
                        <ViewableImage alt="Character Lapis from Steven Universe dressed like the Batter from OFF" src="lapis2.png">
                            Lorem ipsum
                        </ViewableImage>
                    </Cell>
                    <Cell col={3} row={9} colSpan={3} rowSpan={12}>
                        <ViewableImage alt="Character Lapis from Steven Universe with what appears to be wings elevating her in the air" src="lapis1.png">
                            Lorem ipsum
                        </ViewableImage>
                    </Cell>
                    <Cell col={1} row={17} colSpan={2} rowSpan={8}>
                        <ViewableImage alt="Character Paraffin from the Terraria Split Mod" src="paraffin.png">
                            Lorem ipsum
                        </ViewableImage>
                    </Cell>
                    <Cell col={3} row={21} colSpan={2} rowSpan={8}>
                        <ViewableImage alt="Character Lapis from Steven Universe collecting the rain in her hands as she stands in a puddle with an umbrella protecting her" src="lapis3.png">
                            Lorem ipsum
                        </ViewableImage>
                    </Cell>
                    <Cell col={5} row={21} colSpan={1} rowSpan={4}>
                        <ViewableImage alt="A collection of a few poses of the Character Lapis from Steven Universe" src="lapisall.png">
                            Lorem ipsum
                        </ViewableImage>
                    </Cell>
                    <Cell col={1} row={23} colSpan={2} rowSpan={8}>
                        <ViewableImage alt="Character Perfect Heart from OMORI holding a wine glass in the air" src="perfectheart.png">
                            Lorem ipsum
                        </ViewableImage>
                    </Cell>
                </Grid>
            </div>
        </div>
    </div>
</div>