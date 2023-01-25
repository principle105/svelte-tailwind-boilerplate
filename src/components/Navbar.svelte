<script lang="ts">
    import { onMount } from "svelte";
    import { link } from "svelte-spa-router";
    import active from "svelte-spa-router/active";
    import gsap, { Expo } from "gsap";

    import FaBars from "svelte-icons/fa/FaBars.svelte";
    import FaTimes from "svelte-icons/fa/FaTimes.svelte";

    const barTl = gsap.timeline({ reversed: true });
    3;

    onMount(() => {
        barTl.set("#bar", {
            className:
                "fixed inset-0 z-30 bg-zinc-900 bg-opacity-80 flex backdrop-blur-lg flex-col justify-center items-center text-4xl gap-7 text-zinc-300",
        });
        barTl.set("#bar > *", {
            y: 50,
            opacity: 0,
        });
        barTl.set("#open", {
            display: "none",
            duration: 0,
        });
        barTl.to("#close", {
            display: "block",
            duration: 0,
        });
        barTl.to("#bar", {
            duration: 0.3,
            ease: Expo.easeInOut,
        });
        barTl.to("#bar > *", {
            duration: 0.35,
            opacity: 1,
            y: 10,
            stagger: 0.2,
            ease: Expo.easeInOut,
        });
    });

    const toggleNav = () => {
        // Checking if the hamburger nav is visible
        if (
            window
                .getComputedStyle(document.getElementById("toggle"))
                .getPropertyValue("display") === "none"
        )
            return;

        if (barTl.reversed()) {
            barTl.timeScale(1).reversed(false);
        } else {
            barTl.reversed(true).time(0);
        }
    };

    const pages = [
        { name: "Page1", href: "/page1" },
        { name: "Page2", href: "/page2" },
        { name: "Page3", href: "/page3" },
    ];
</script>

<header class="flex justify-between items-center py-8">
    <a href="/" use:link>
        <span class="text-3xl text-zinc-50 font-bold hidden sm:block">
            Website Name
        </span>
        <img
            src="https://i.imgur.com/Z4QEDUE.png"
            alt="logo"
            class="h-14 rounded-full block sm:hidden"
        />
    </a>
    <nav
        class="text-zinc-400 text-lg justify-between gap-20 hidden opacity-0 lg:flex lg:opacity-100"
        id="bar"
    >
        {#each pages as { href, name }}
            <a {href} use:link use:active on:click={toggleNav}>{name}</a>
        {/each}
    </nav>

    <button
        class="w-9 h-9 block lg:hidden text-zinc-200 z-50"
        aria-label="toggle navigation"
        id="toggle"
        on:click={toggleNav}
    >
        <div id="open">
            <FaBars />
        </div>
        <div id="close" class="hidden">
            <FaTimes />
        </div>
    </button>
</header>

<style>
    :global(a.active) {
        @apply text-gray-50 underline;
    }
</style>
