<script context="module">
    export const load = async ({fetch}) => {
        const res = await fetch(`${import.meta.env.VITE_BASE_URL}/rcms-api/8/partners `);
        const data = await res.json();
        
        return {
            props: {
                data,
            },
        };
    };
</script>

<script>
    export let data;

    import { goto } from '$app/navigation';

    const handleCardClick = (id) => {
        goto(`/services/${id}`)
    }
</script>
<div class="container justify-content-center my-4">
    <div class="row justify-content-between">
        <div class="col-lg-7 py-4">
            <h5>Perched in the serene setting of low top Nathdwara Hills, The Marutinandan Grand offers luxurious accommodations and thoughtfully curated amenities.
            </h5>
            <ul class="mt-4">
                <li>The hotel features a wellness center that offers rejuvenating therapies and a gymnasium for fitness enthusiasts. </li>
                <li>The hotel has a discotheque featuring throbbing music, perfect for night parties. </li>
                <li>Kids can have a fun-filled stay experience with the kids' play area.</li>
                <li>The in-house recreational club offers various indoor games.</li>
            </ul>
        </div>
        <div class="col-lg-4">
            <div class="card text-center">
                <div class="card-header fw-bold">CONTACT US</div>
                <div class="card-body">
                  <h5 class="card-title">Udaipur</h5>
                  <p class="card-text">The Marutinandan Grand, NH. 8, Odan, Nathdwara, Rajasthan 313301</p>
                  <!-- <h5 class="card-title">Transit office</h5>
                  <p class="card-text">Sukhadia CirPanchwati, Udaipur, Rajasthan 313001</p> -->
                  <h5 class="card-title">Mobile</h5>
                  <p class="card-text">(+91)7297818022, 9950305525</p>
                  <h5 class="card-title">Email</h5>
                  <p class="card-text">sagarpaliwal.sp2@gmail.com</p>
                </div>
                <div class="card-footer text-muted">Visit soon</div>
              </div>
        </div>
    </div>
</div>

<div class="partners justify-content-center">
    <center><h1 class="py-4 fw-bold">OUR PARTNERS</h1></center>
    <div class="container">
        <div class="row g-4 justify-content-center">
            {#each data.list as item}
            <div class="col-5">
                <div class="card mb-3" >
                    <div class="row g-0">
                        <div class="col-md-5 bg-image" style="--image_url: url({item.ext_4.url});">
                        </div>
                        <div class="col-md-7">
                            <div class="card-body">
                                <h5 class="card-title">{item.ext_1}</h5>
                                <p class="card-text">
                                <small class="text-muted">{item.ext_2}</small>
                                </p>
                                <p class="card-text">
                                    {item.ext_3}
                                </p>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            {/each}
        </div>
    </div>
</div>

<style>
    .bg-image {
        background-image: var(--image_url);
        background-size: cover;
        background-repeat: no-repeat;
    }
    .partners {
        background-color: #4f4f4f;
    }
    .partners h1 {
        color: #fff;
    }
</style>