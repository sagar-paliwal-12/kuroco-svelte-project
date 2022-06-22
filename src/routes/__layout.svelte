<script context="module">
    export const load = async ({url, fetch}) => {
        const activeNav = url.pathname;
        
        const media = await fetch(`${import.meta.env.VITE_BASE_URL}/rcms-api/7/social-media`);
        const media_res = await media.json();
        
        return {
            props: {
                media_res,
                activeNav,
            },
        };
    };
</script>

<script>
    import Nav from "$lib/Nav.svelte"
    import Footer from "$lib/Footer.svelte";
    export let media_res, activeNav;
</script>

<div class="container-fluid">
    <Nav activeNav={activeNav} />
    <slot />
    <Footer media_res={media_res} />
</div>

<style>
    .container-fluid {
        height: 100vh;
        margin: 0;
        padding: 0;
    }
</style>