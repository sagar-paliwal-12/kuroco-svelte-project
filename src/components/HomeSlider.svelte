<script>
  export let slider_res;
</script>

<div id="carouselDarkVariant" class="carousel slide carousel-fade carousel-dark" data-mdb-ride="carousel">
    <div class="carousel-indicators">
      <button
        data-mdb-target="#carouselDarkVariant"
        data-mdb-slide-to="0"
        class="active"
        aria-current="true"
        aria-label="Slide 1"
      ></button>
      <button
        data-mdb-target="#carouselDarkVariant"
        data-mdb-slide-to="1"
        aria-label="Slide 1"
      ></button>
      <button
        data-mdb-target="#carouselDarkVariant"
        data-mdb-slide-to="2"
        aria-label="Slide 1"
      ></button>
    </div>

    <div class="carousel-inner">
      <!-- Single item -->
      {#each slider_res.list as item, index}
      <div class="carousel-item {index === 0 ? 'active' : ''}">
        <img src={item.ext_1.url} class="d-block w-100" alt="Motorbike Smoke"/>
        <div class="carousel-caption d-none d-md-block">
          <h5>{item.subject}</h5>
          <p>{item.ext_1.desc}</p>
        </div>
      </div>
      {/each}
    </div>
    <!-- Inner -->
  
    <!-- Controls -->
    <button class="carousel-control-prev" type="button" data-mdb-target="#carouselDarkVariant" data-mdb-slide="prev">
      <span class="carousel-control-prev-icon " aria-hidden="true"></span>
      <span class="visually-hidden">Previous</span>
    </button>
    <button class="carousel-control-next" type="button" data-mdb-target="#carouselDarkVariant" data-mdb-slide="next">
      <span class="carousel-control-next-icon" aria-hidden="true"></span>
      <span class="visually-hidden">Next</span>
    </button>
</div>

<style>
  .carousel-control-prev-icon {
      background-color: rgba(255, 255, 255, 1) !important;
      height: 40px;
      border-bottom-right-radius: 8px;
      border-top-right-radius: 8px;
  }
  .carousel-control-next-icon {
      background-color: rgba(255, 255, 255, 1) !important;
      height: 40px;
      border-bottom-left-radius: 8px;
      border-top-left-radius: 8px;
  }
  .carousel-control-next-icon::after, .carousel-control-prev-icon::after {
      color: #000 !important;
  }
</style>