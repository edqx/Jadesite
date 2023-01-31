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
                    To the right or below are just a few samples of concept art drawn for characters in a project going by the name "Edith". Edith is a passion project started by myself and a very close friend of mine and is currently one year into development, with it's demo a very early work in progress. Inspired by OMOCAT's "OMORI", Edith is a top-down RPG loveletter to the aformentioned title, with my primary role in its creation being art direction for both final pieces along with concept artwork and designs (with a secondary but still large focus on story and character development). The images to the right are clickable, and should display a small and relevant caption. The date at which each piece of concept art was made is written in red pen to give an idea as to which are early works and which are more recent.
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
                     To the right or below are some examples of the in-game spritework test animations done for the previously mentioned early unpolished demo currently being worked on for Edith, along with a screen recording containing some of them actually being used. These animations include: breathing, idling, attacking, jumping and crouching motions, as well as taking damage. While they don't look particuarly animated on their own, however once given context with each other, they flow well into one another for the type of gameplay we hope Edith is going to have. Some older attempts at these animations should be seen below the screen recording.
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
                    <ViewableImage src="/edithdemoexample.gif" alt="Demo of game showing animations in action">
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
                     To the right or below are some exaxmples of older animations done previously for Edith's gameplay. The style is competely different, and the animations themselves are included inside the sheets rather than being more freeform like the ones above. Whilst these are technically smoother, they're also far more difficult to work with and were proving a nightmare to make look good in production, so they were all scrapped and redone in favour of the ones shown above.
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
                    <ViewableImage src="/old_animations/edithdemoexaxmpleold.gif" alt="Demo of game showing animations in action">
                    </ViewableImage>
                </div>
            </div>
        </div>
    </div>
    <div class="lg:ml-38 relative flex flex-col">
        <div class="absolute -top-32" id="misc" bind:this={projectSectionElements[2]}></div>
        <div class="flex items-center flex-col xl:items-start xl:flex-row gap-16">
            <div class="mx-8 sm:mx-0 sm:w-[30rem]">
                <span class="text-4xl">Misc.</span>
                <p>
                    To the right or below are a few examples of miscellaneous artwork that I've done, some for practise, others for testing new techniques. Whilst there aren't too many examples shown, I think there's enough to give a general overview of my style(s) along with where my strengths and weakness lie when it comes to art. Posing and colouring are two of my main issues when it comes to drawing and are the things I'm currently working on improving, along with anatomy and perspective. 4 of the images on the right are in a sequence showing the improvement in my art from the idea to the execution (if they aren't laid out next to each other, they're the 4 with the orange and purple haired characters). All the images, however, should be clickable in order to enlarge and see their captions.
                </p>
            </div>
            <div class="2xl:w-[42rem] sm:w-[28rem] w-[20rem]">
                <Grid cols={5} rows={30}>
                    <Cell col={1} row={1} colSpan={1} rowSpan={8}>
                        <div class="mt-auto">
                            <ViewableImage alt="A scene showing a reflection between two sides of the character Madeline from Celeste's psyche" src="celeste1.png">
                                The 1st piece of artwork in a sequence of improvement. I wasn't too happy with how my idea for this fanart turned out, so I tried again.
                            </ViewableImage>
                        </div>
                    </Cell>
                    <Cell col={2} row={1} colSpan={2} rowSpan={8}>
                        <ViewableImage alt="A scene showing a reflection between two sides of the character Madeline from Celeste's psyche" src="celeste2.png">
                            The 2nd piece of artwork in a sequence of improvement. I tried drawing on a larger scale and adding some more framing and using a different brush to colour, however I didn't like how small the scope of the idea had turned out, so I tried again.
                        </ViewableImage>
                    </Cell>
                    <Cell col={4} row={1} colSpan={1} rowSpan={8}>
                        <div class="mt-auto">
                            <ViewableImage alt="Character Madeline from Celeste battling her alter-ego with a golden feather" src="celeste3.png">
                                The 3rd piece of artwork in a sequence of improvement. This time I completely redid the layout of the drawing to try and give it some nicer visuals, this was done in around 5 hours as part of an art competition.
                            </ViewableImage>
                        </div>
                    </Cell>
                    <Cell col={5} row={1} colSpan={1} rowSpan={8}>
                        <div class="mt-auto">
                            <ViewableImage alt="Character Madeline from Celeste battling her alter-ego with a golden feather" src="celeste4.png">
                                The 4th piece of artwork in a sequence of improvement. After the art competition, I went back and refined the piece I had made, making it larger and tweaking some layers. All of these drawings were done very close to one another in time, I was suprirsed myself at how much improvemnet I could make.
                            </ViewableImage>
                        </div>
                    </Cell>
                    <Cell col={1} row={9} colSpan={2} rowSpan={8}>
                        <ViewableImage alt="Character Lapis from Steven Universe dressed like the Batter from OFF" src="lapis2.png">
                            I really struggled with getting the hair to look natural in this pose, as trying to draw the hair from a front angle  was proving difficult to make look natural. Adding some wind to the hair however helped ease the process.
                        </ViewableImage>
                    </Cell>
                    <Cell col={3} row={9} colSpan={3} rowSpan={12}>
                        <ViewableImage alt="Character Lapis from Steven Universe with what appears to be wings elevating her in the air" src="lapis1.png">
                            The was the first of 3 small fanarts I did as a small practise project. I'm really happy with how this one turned out with the posing of the body and hair. The shading could be much better, however that wasn't my main focus at the time.
                        </ViewableImage>
                    </Cell>
                    <Cell col={1} row={17} colSpan={2} rowSpan={8}>
                        <ViewableImage alt="Character Paraffin from the Terraria Split Mod" src="paraffin.png">
                            On the left of this image is (for all intensive purposes) the first ever drawing I did on my graphics tablet, which eventually lead to everything else you see on this page and much, much more. To the right is an improved version, though I'm planning on doing another improvement piece.
                        </ViewableImage>
                    </Cell>
                    <Cell col={3} row={21} colSpan={2} rowSpan={8}>
                        <ViewableImage alt="Character Lapis from Steven Universe collecting the rain in her hands as she stands in a puddle with an umbrella protecting her" src="lapis3.png">
                            Drawing characters from behind is something I'm trying to work on getting better at, and I quite like how this piece turned out. It's also the first piece that I downloaded a custom brush for, in the form of the rain seen coming from the umbrella.
                        </ViewableImage>
                    </Cell>
                    <Cell col={5} row={21} colSpan={1} rowSpan={4}>
                        <ViewableImage alt="A collection of a few poses of the Character Lapis from Steven Universe" src="lapisall.png">
                            All 3 pieces of fanart done for this small practise project together, I'm happy with the way they turned out even if they are quite flawed. It was nice testing out different and new techniques on each one.
                        </ViewableImage>
                    </Cell>
                    <Cell col={1} row={23} colSpan={2} rowSpan={8}>
                        <ViewableImage alt="Character Perfect Heart from OMORI holding a wine glass in the air" src="perfectheart.png">
                            This was mainly a colour test done as part of a larger piece of artwork that I had planned which isn't shown here.
                        </ViewableImage>
                    </Cell>
                </Grid>
            </div>
        </div>
    </div>
</div>