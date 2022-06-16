<script context="module">
    export const load = async ({url, fetch}) => {
        const activeNav = url.pathname;
        const res = await fetch(`${import.meta.env.VITE_BASE_URL}/rcms-api/3/form/3`);
        const data = await res.json();
        
        const media = await fetch(`${import.meta.env.VITE_BASE_URL}/rcms-api/7/social-media`);
        const media_res = await media.json();
        
        return {
            props: {
                data,
                media_res,
                activeNav,
            },
        };
    };
</script>

<script>
    import Nav from "$lib/Nav.svelte"
    import Footer from "$lib/Footer.svelte";
    export let data, media_res, activeNav;
</script>

<div class="container-fluid">
    <Nav activeNav={activeNav} />
    <slot />
    <Footer data={data} media_res={media_res} />
</div>

<style>
    .container-fluid {
        height: 100vh;
        margin: 0;
        padding: 0;
    }
</style>