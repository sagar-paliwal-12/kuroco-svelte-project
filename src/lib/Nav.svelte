<script>
  export let activeNav;

  const navMapping = {
    "/": "Home",
    "/services": "Services",
    "/about": "About Us",
    "/inquiry": "Inquiry",
  };
</script>

<nav class="navbar navbar-expand-lg navbar-light bg-light">
  <div class="container-fluid">
    <button
      class="navbar-toggler"
      type="button"
      data-mdb-toggle="collapse"
      data-mdb-target="#navbarSupportedContent"
      aria-controls="navbarSupportedContent"
      aria-expanded="false"
      aria-label="Toggle navigation"
    >
      <i class="fas fa-bars" />
    </button>

    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <a class="navbar-brand mt-2 mt-lg-0" href="/">
        <img
          src="https://kuroco-svelte-project.g.kuroco-img.app/files/user/hotel_logo.png"
          height="40"
          alt="TMG Logo"
          loading="lazy"
        />
      </a>
      <ul class="navbar-nav me-auto mb-2 mb-lg-0 justify-content-center">
        {#each Object.entries(navMapping) as [key, value]}
          <li class="nav-item">
            <a
              class="nav-link {key == activeNav ? 'active-nav' : ''}"
              href={key}>{value}</a
            >
          </li>
        {/each}
      </ul>
    </div>
  </div>
</nav>

<style>
  img {
    margin-right: 40px;
  }
  li {
    padding: 0 10px;
  }
  .nav-link {
    color: rgba(255, 255, 255, 0.5) !important;
  }
  .nav-link:hover {
    color: #d6a870 !important;
  }
  .navbar {
    background-color: #28282b !important;
  }
  .active-nav {
    color: #9b6e44 !important;
  }
  .navbar-light .navbar-toggler {
    color: #fff !important;
  }
  @media (max-width: 800px) {
    .navbar-brand {
      display: none;
    }
  }
</style>
