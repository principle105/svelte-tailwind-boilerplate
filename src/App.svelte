<script lang="ts">
    import Router from "svelte-spa-router";

    import Navbar from "./components/Navbar.svelte";
    import Footer from "./components/Footer.svelte";

    import Home from "./pages/Home.svelte";

    const routes = {
        "/": Home,
    };
</script>

<div class="m-auto w-11/12 sm:w-5/6 lg:w-3/4 grow">
    <Navbar />

    <main>
        <Router {routes} />
    </main>
</div>

<Footer />

<style global>
    @tailwind utilities;
    @tailwind components;
    @tailwind base;
</style>
