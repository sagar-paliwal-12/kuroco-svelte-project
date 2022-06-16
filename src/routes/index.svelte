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

<div class="container justify-content-center text-center my-4">
    <h4>Lorem ipsum dolor sit amet consectetur adipisicing elit. 
        Totam magnam, placeat perferendis neque quisquam consequuntur minima fuga adipisci labore aliquam voluptatibus iste? 
        Ullam reprehenderit maxime quae iure exercitationem voluptatum porro.
        Lorem ipsum dolor sit amet consectetur adipisicing elit. 
        Totam magnam, placeat perferendis neque quisquam consequuntur minima fuga adipisci labore aliquam voluptatibus iste? 
        Ullam reprehenderit maxime quae iure exercitationem voluptatum porro.
        Lorem ipsum dolor sit amet consectetur adipisicing elit. 
        Totam magnam, placeat perferendis neque quisquam consequuntur minima fuga adipisci labore aliquam voluptatibus iste? 
        Ullam reprehenderit maxime quae iure exercitationem voluptatum porro.
    </h4>
    <a href="/about">
        <button type="button" class="btn btn-dark">More about us</button>
    </a>
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


