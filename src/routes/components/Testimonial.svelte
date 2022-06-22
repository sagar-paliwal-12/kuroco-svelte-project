<script>
    export let data;
</script>
<div id="carouselExampleCaptions" class="carousel slide" data-mdb-ride="carousel">
    <center><h1 class="fw-bold text-white">TESTIMONIAL</h1></center>
    <div class="carousel-inner">
        {#each data.list as item, index}
        <div class="carousel-item {index === 0 ? 'active' : ''}">
            <div class="carousel-item-child d-md-block">
                <p><i class="fas fa-quote-left"></i>{item.body}</p>
                <h5>{item.name}</h5>
                <h6>{item.ext_01}</h6>
            </div>
        </div>
        {/each}
    </div>
    <button class="carousel-control-prev" type="button" data-mdb-target="#carouselExampleCaptions" data-mdb-slide="prev">
      <span class="carousel-control-prev-icon" aria-hidden="true"></span>
      <span class="visually-hidden">Previous</span>
    </button>
    <button class="carousel-control-next" type="button" data-mdb-target="#carouselExampleCaptions" data-mdb-slide="next">
      <span class="carousel-control-next-icon" aria-hidden="true"></span>
      <span class="visually-hidden">Next</span>
    </button>
  </div>

<style>
    #carouselExampleCaptions {
        padding: 40px 0;
        background-color: #4f4f4f;
    }
    .carousel-item-child {
        padding-top: 1.25rem;
        padding-bottom: 1.25rem;
        color: #fff;
        text-align: center;
    }
    .carousel-item-child p {
        border: 1px dotted;
        border-radius: 8px;
        padding: 10px;
        max-width: 50%;
        margin-left: 25%;
    }
    .fa-quote-left::before {
        position: relative;
        left: -10px;
        top: -21px;
        padding: 0 5px;
        background-color: #4f4f4f;
    }
</style>