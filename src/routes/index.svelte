<script context="module">
    export const load = async ({fetch}) => {
        const res = await fetch(`${import.meta.env.VITE_BASE_URL}/rcms-api/3/form-answers?inquiry_id=5`);
        const data = await res.json();

        const home = await fetch(`${import.meta.env.VITE_BASE_URL}/rcms-api/6/slider/7`);
        const home_res = await home.json();
        console.log(home_res)
        
        return {
            props: {
                data,
                home_res,
            },
        };
    };
</script>

<script>
    export let data, home_res;
    import Testimonial from "../components/Testimonial.svelte";
    import HomeSlider from "../components/HomeSlider.svelte";
</script>

<HomeSlider slider_res={home_res.details.ext_1} />

<div class="container justify-content-center row my-4">
  <div class="col-lg-8">
    <h5>{home_res.details.ext_2}
    </h5>
    <ul class="mt-4">
      {#each home_res.details.ext_3 as item}
        <li>{item}</li>
      {/each}
    </ul>
    <a href="/about">
        <button type="button" class="btn btn-dark">More about us</button>
    </a>
  </div>
</div>

<Testimonial data={data} />

<div class="container p-4">
    <section class="">
      <div class="row d-flex justify-content-center">
        <div class="col-lg-6">
          <center><h1 class="fw-bold">AERIAL VIEW</h1></center>
          <div class="ratio ratio-16x9">
            <iframe
              class="shadow-1-strong rounded"
              src={home_res.details.ext_4.url}
              title={home_res.details.ext_4.title}
              allowfullscreen
            ></iframe>
          </div>
        </div>
      </div>
    </section>
</div>


