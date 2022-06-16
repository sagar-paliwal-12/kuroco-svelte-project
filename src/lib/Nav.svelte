<script>
    import { get } from 'svelte/store';

    import { profile } from '../stores.js'
    let email = "";
    let password = "";

    let status = get(profile);
    let loginStatus = "";
    let resultMessage = null;

    let message = "";
    let error = "";

    let messageColor = {
        "success": "green",
        "failure": "red",
    }

    const handleLogin = async () => {
        try {
            const res = await fetch(`${import.meta.env.VITE_BASE_URL}/rcms-api/4/login`, {
                method: "POST",
                body: JSON.stringify({
                    email,
                    password,
                }),
                headers: {
                    'Content-Type': 'application/json'
                },
            })

            if (res.status === 200) {
                profile.set(true)
                status = true
                localStorage.setItem("authenticated", true)
                message = "Login Successful";
            } else {
                message = "Login Unsuccessful";
            }   

        } catch(err) {
            error = err;
        }
    }

    const handleLogout = async () => {
        try {
            await fetch(`${import.meta.env.VITE_BASE_URL}/rcms-api/4/logout`, {method: "POST"})
            localStorage.setItem("authenticated", false)
            profile.set(false)
            status = false;
        } catch (err) {
        }
    }
</script>

<nav class="navbar navbar-expand-lg navbar-light bg-light">
    <!-- Container wrapper -->
    <div class="container-fluid">
        <!-- Toggle button -->
        <button
            class="navbar-toggler"
            type="button"
            data-mdb-toggle="collapse"
            data-mdb-target="#navbarSupportedContent"
            aria-controls="navbarSupportedContent"
            aria-expanded="false"
            aria-label="Toggle navigation"
        >
            <i class="fas fa-bars"></i>
        </button>
  
      <!-- Collapsible wrapper -->
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <!-- Navbar brand -->
        <a class="navbar-brand mt-2 mt-lg-0" href="/">
            <img
                src="https://mdbcdn.b-cdn.net/img/logo/mdb-transaprent-noshadows.webp"
                height="15"
                alt="MDB Logo"
                loading="lazy"
            />
        </a>
        <ul class="navbar-nav me-auto mb-2 mb-lg-0 justify-content-center">
            <li class="nav-item">
                <a class="nav-link" href="/">Home </a>
            </li>
            <li class="nav-item">
                <a class="nav-link" href="/services">Services</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" href="/about">About Us</a>
            </li>
            <li class="nav-item">
                <a class="nav-link" href="/inquiry">Inquiry</a>
            </li>
        </ul>
      </div>
      {#if !status}
      <button type="button" class="btn btn-primary" data-mdb-toggle="modal" data-mdb-target="#exampleModal">
        Login
      </button>
      {:else}
      <button type="button" class="btn btn-primary" on:click={() => handleLogout()}>
        Logout
      </button>
      {/if}
    </div>
</nav>

<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
        <div class="modal-content">
        <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
            <button type="button" class="btn-close" data-mdb-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
            <form on:submit|preventDefault={() => handleLogin()}>
                <!-- Email input -->
                <!-- {#if loginStatus !== null}
                <p style="color: {messageColor[loginStatus]}">{resultMessage}</p>
                {/if} -->
                <div class="form-outline mb-4">
                  <input name="email" type="email" id="form1Example1" class="form-control" bind:value={email}/>
                  <label class="form-label" for="form1Example1">Email address</label>
                </div>
              
                <!-- Password input -->
                <div class="form-outline mb-4">
                  <input name="password" type="password" id="form1Example2" class="form-control" bind:value={password} />
                  <label class="form-label" for="form1Example2">Password</label>
                </div>
              
                <!-- 2 column grid layout for inline styling -->
                <div class="row mb-4">
                  <div class="col d-flex justify-content-center">
                    <!-- Checkbox -->
                    <div class="form-check">
                      <input class="form-check-input" type="checkbox" value="" id="form1Example3" checked />
                      <label class="form-check-label" for="form1Example3"> Remember me </label>
                    </div>
                  </div>
              
                  <div class="col">
                    <!-- Simple link -->
                    <a href="#!">Forgot password?</a>
                  </div>
                </div>
              
                <!-- Submit button -->
                <button type="submit" class="btn btn-primary btn-block">Sign in</button>
              </form>
        </div>
        <!-- <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-mdb-dismiss="modal">Close</button>
            <button type="button" class="btn btn-primary">Save changes</button>
        </div> -->
        </div>
    </div>
</div>

<style>
    img {
        margin-right: 40px;
    }
    li {
        padding: 0 10px;
    }
    .nav-link {
        color: rgba(255,255,255,0.5) !important
    }
    .nav-link:hover {
        color: rgba(255,255,255,1) !important
    }
    .navbar {
        background-color: rgba(38,38,38,var(--mdb-bg-opacity))!important;
    }
</style>
