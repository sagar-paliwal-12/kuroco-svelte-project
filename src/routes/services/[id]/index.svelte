<script context="module">
    export const load = async ({url, params, fetch}) => {
        const id = await params.id;
        const res = await fetch(`${import.meta.env.VITE_BASE_URL}/rcms-api/3/services/${id}`);
        const data = await res.json();
        
        return {
            props: {
                data,
            },
        };
    };
</script>

<script>
    import ServicesImage from "../../../components/ServicesImage.svelte";

    export let data;
</script>

<div class="container-fluid" style="--image_url: url({data.details.ext_3.url});">
    <div class="col-12 service-body justify-content-center container">
        <h1>{data.details.ext_1}</h1>
        <h4>{data.details.ext_2}</h4>
    </div>
</div>

<div class="features">
    <div class="container">
        <center><h2>Key features: -</h2></center>
        <div class="row justify-content-center">
            <div class="col-lg-4">
                <ul>
                    {#each data.details.ext_5 as key}
                    <li>{key}</li>
                    {/each}
                </ul>
            </div>
        </div>
    </div>
</div>

<ServicesImage data={data} />

<style>
    .container-fluid {
        background-size: cover;
        background-repeat: no-repeat;
        background-attachment: fixed;
        background-image: linear-gradient(rgba(255,255,255,0.6), rgba(255,255,255,0.6)), var(--image_url);
        color: black;
    }
    .service-body {
        padding: 40px 0;
        width: 70%;
        justify-content: center;
        text-align: center;
    }
    .features {
        background-color: #4f4f4f;
        color: #fff;
        padding: 16px 0 ;
    }
</style>

