<script context="module">
  export const load = async ({ fetch }) => {
    const res = await fetch(
      `${import.meta.env.VITE_BASE_URL}/rcms-api/3/services?topics_group_id=7`
    );
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

  import { goto } from "$app/navigation";

  const handleCardClick = (id) => {
    goto(`/services/${id}`);
  };
</script>

<div class="container my-4">
  <center><h1 class="fw-bold">OUR SERVICES</h1></center>
  <div class="row row-cols-1 row-cols-md-3 g-4">
    {#each data.list as item}
      <div class="col" on:click={() => handleCardClick(item.topics_id)}>
        <div class="card h-100">
          <img
            src={item.ext_3.url}
            class="card-img-top"
            alt="Hollywood Sign on The Hill"
          />
          <div class="card-body">
            <h5 class="card-title">{item.subject}</h5>
            <p class="card-text">
              {item.ext_2}
            </p>
          </div>
        </div>
      </div>
    {/each}
  </div>
</div>

<style>
  .card-img-top {
    height: 200px;
  }
  .card {
    cursor: pointer;
  }
  .card:hover {
    background-color: #4f4f4f;
    color: #fff;
  }
</style>
