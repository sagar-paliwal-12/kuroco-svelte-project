<script context="module">
    export const load = async ({fetch}) => {
        const res = await fetch(`${import.meta.env.VITE_BASE_URL}/rcms-api/3/form-answers?inquiry_id=5`);
        const data = await res.json();

        const slider = await fetch(`${import.meta.env.VITE_BASE_URL}/rcms-api/6/slider`);
        const slider_res = await slider.json();
        
        return {
            props: {
                data,
                slider_res,
            },
        };
    };
</script>

<script>
    export let data, slider_res;
    import Testimonial from "../components/Testimonial.svelte";
    import HomeSlider from "../components/HomeSlider.svelte";
</script>

<HomeSlider slider_res={slider_res} />

<div class="container justify-content-center row my-4">
  <div class="col-lg-8">
    <h5>Perched in the serene setting of low top Nathdwara Hills, The Marutinandan Grand offers luxurious accommodations and thoughtfully curated amenities.
    </h5>
    <ul class="mt-4">
        <li>The hotel features a wellness center that offers rejuvenating therapies and a gymnasium for fitness enthusiasts. </li>
        <li>The hotel has a discotheque featuring throbbing music, perfect for night parties. </li>
        <li>Kids can have a fun-filled stay experience with the kids' play area.</li>
        <li>The in-house recreational club offers various indoor games.</li>
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
          <div class="ratio ratio-16x9">
            <iframe
              class="shadow-1-strong rounded"
              src="https://www.youtube.com/embed/vlDzYIIOYmM"
              title="YouTube video"
              allowfullscreen
            ></iframe>
          </div>
        </div>
      </div>
    </section>
</div>


