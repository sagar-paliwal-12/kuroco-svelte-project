<script>
    export let data, media_res;

    let email = "";

    let message = "";
    let error = "";

    const form_fields = data.details.cols;

    const handleSubscribe = async () => {
        if (message) {
            email="";
            message="";
            error = "";
            return;
        }
        try {
            const submit = await fetch(`${import.meta.env.VITE_BASE_URL}/rcms-api/3/form?id=3`, {
                method: "POST",
                body: JSON.stringify({
                    from_mail: email,
                }),
                headers: {
                    'Content-Type': 'application/json'
                },
            })

            const data1 = await submit.json();
            message = data1.messages[0];
        } catch(err) {
            error = err;
        }
    }

</script>

<footer class="bg-dark text-center text-white">
    <div class="container-fluid row p-4 pb-0 justify-content-between">
      <section class="mb-4 col-lg-4">
        {#each media_res.list as item}
            <a class="btn btn-outline-light btn-floating m-1" href={item.ext_3} role="button">
                <i class="fab fa-{item.ext_2}"></i>
            </a>
        {/each}
      </section>
      <section class="col-lg-5">
        <form on:submit|preventDefault={handleSubscribe} ref="form">
          <!--Grid row-->
          <div class="row d-flex justify-content-center">
            <!--Grid column-->
            <div class="col-md-5 col-7">
              <!-- Email input -->
                {#if !message && !error}
                {#each Object.entries(form_fields) as [key, value]}
                {#if value.required === 2}
                    <div class="form-outline form-white mb-4">
                        <input type="text" name="{value.title}" id="form5Example29" class="form-control" aria-label="readonly input example" bind:value={email} />
                        <label class="form-label" for="form5Example29">{value.title}</label>
                    </div>
                {/if}
                {/each}
                {:else if message}
                <p>{message}</p>
                {:else if error}
                <p>{error}</p>
                {/if}
            </div>
            <!--Grid column-->
  
            <!--Grid column-->
            <div class="col-auto">
              <!-- Submit button -->
              <button type="submit" class="btn btn-outline-light mb-4">
                {#if !message}
                Subscribe
                {:else}
                Submit another email
                {/if}
              </button>
            </div>
            <!--Grid column-->
          </div>
          <!--Grid row-->
        </form>
      </section>
      <!-- Section: Form -->
    </div>
    <div class="copyright p-3" style="background-color: rgba(0, 0, 0, 0.2);">
      © 2020 Copyright:
      <a href="https://mdbootstrap.com/">restrosite.com</a>
    </div>
</footer>

<style>
    .copyright, a {
        text-align: center;
        color: rgba(255, 255, 255, 0.5)
    }
    .form-outline.form-white .form-control {
        border: 1px dotted;
    }
</style>