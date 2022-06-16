<script>
    export let data;
</script>

<div id="carouselDarkVariant" class="container carousel slide carousel-fade carousel-dark" data-mdb-ride="carousel">
    <center><h2>Gallery</h2></center>
    <div class="carousel-inner">
        <!-- Single item -->
        {#each data.details.ext_4 as item, index}
        <div class="carousel-item {index === 0 ? 'active': ''}">
            <img src={item.url} class="d-block w-100" alt="Motorbike Smoke"/>
            <div class="carousel-caption d-none d-md-block">
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
    .carousel {
        width: 50%;
        padding: 16px;
    }
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
  .carousel-control-prev {
    left: -80px;
  }
  .carousel-control-next {
    right: -80px;
  }
  .carousel-control-next-icon::after, .carousel-control-prev-icon::after {
      color: #000 !important;
  }
</style>