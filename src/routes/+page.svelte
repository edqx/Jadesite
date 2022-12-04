<script lang="ts">
    import { onDestroy, onMount } from "svelte";
    import { goto } from "$app/navigation";
    import { browser } from "$app/environment";

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
            return section.getBoundingClientRect().top < windowInnerHeight;
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
    <div class="flex flex-col w-[58rem]" id="edith" bind:this={projectSectionElements[0]}>
        <span class="text-4xl">Edith</span>
        <p>
            Is this a dagger which I see before me,<br>
            The handle toward my hand? Come, let me clutch thee.<br>
            I have thee not, and yet I see thee still.<br>
            Art thou not, fatal vision, sensible<br>
            To feeling as to sight? or art thou but<br>
            A dagger of the mind, a false creation,<br>
            Proceeding from the heat-oppressed brain?<br>
            I see thee yet, in form as palpable<br>
            As this which now I draw.<br>
            Thou marshall'st me the way that I was going;<br>
            And such an instrument I was to use.<br>
            Mine eyes are made the fools o' the other senses,<br>
            Or else worth all the rest; I see thee still,<br>
            And on thy blade and dudgeon gouts of blood,<br>
            Which was not so before. There's no such thing:<br>
            It is the bloody business which informs<br>
            Thus to mine eyes. Now o'er the one halfworld<br>
            Nature seems dead, and wicked dreams abuse<br>
            The curtain'd sleep; witchcraft celebrates<br>
            Pale Hecate's offerings, and wither'd murder,<br>
            Alarum'd by his sentinel, the wolf,<br>
            Whose howl's his watch, thus with his stealthy pace.<br>
            With Tarquin's ravishing strides, towards his design<br>
            Moves like a ghost. Thou sure and firm-set earth,<br>
            Hear not my steps, which way they walk, for fear<br>
            Thy very stones prate of my whereabout,<br>
            And take the present horror from the time,<br>
            Which now suits with it. Whiles I threat, he lives:<br>
            Words to the heat of deeds too cold breath gives.
        </p>
    </div>
    <div class="flex flex-col w-[58rem] mt-14" id="miss-you-on-the-train" bind:this={projectSectionElements[1]}>
        <span class="text-4xl">I miss you on the train</span>
        <p>
            When I consider everything that grows<br>
            Holds in perfection but a little moment,<br>
            That this huge stage presenteth nought but shows<br>
            Whereon the stars in secret influence comment;<br>
            When I perceive that men as plants increase,<br>
            Cheered and check'd even by the selfsame sky,<br>
            Vaunt in their youthful sap, at height decrease,<br>
            And wear their brave state out of memory;<br>
            Then the conceit of this inconstant stay<br>
            Sets you most rich in youth before my sight,<br>
            Where wasteful Time debateth with Decay<br>
            To change your day of youth to sullied night;<br>
            And all in war with Time for love of you,<br>
            As he takes from you, I engraft you new.
        </p>
    </div>
    <div class="flex flex-col w-[58rem] mt-14" id="chicago" bind:this={projectSectionElements[2]}>
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