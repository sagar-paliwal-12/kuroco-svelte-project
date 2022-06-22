<script>
  export let media_res, ref;

  let message = "";
  let error = "";
  let loading = false;

  let formType = "subscribe";

  const handleSubscribe = async () => {
    if (message || error) {
      message = "";
      error = "";
      return;
    }
    loading = true;
    const formInputElements = Array.from(ref).filter(
      (elm) => elm.tagName.toLowerCase() === "input"
    );

    const body = formInputElements
      .map((elm) => ({ [elm.name]: elm.value }))
      .reduce((prev, cur) => ({ ...prev, ...cur }), {});

    if (formType === "sendMail") {
      body.mail_to = body.email;
      delete body.email;
    }

    try {
      const submit = await fetch(
        `${import.meta.env.VITE_BASE_URL}/rcms-api/3/${formType}`,
        {
          method: "POST",
          body: JSON.stringify({
            ...body,
          }),
          headers: {
            "Content-Type": "application/json",
          },
        }
      );

      const data1 = await submit.json();

      if ("messages" in data1) {
        message = data1.messages[0] || "Successfull!";
      } else {
        message = data1.errors[0].message;
      }

    } catch (err) {
      error = err;
    } finally {
      loading = false;
    }
  };
</script>

<footer class="bg-dark text-center text-white">
  <div class="container-fluid row p-4 pb-0 justify-content-between">
    <section class="mb-4 col-lg-4">
      {#each media_res.list as item}
        <a
          class="btn btn-outline-light btn-floating m-1"
          href={item.ext_3}
          target="_blank"
          role="button"
        >
          <i class="fab fa-{item.ext_2}" />
        </a>
      {/each}
    </section>
    <section class="col-lg-5">
      {#if loading}
        <p>Subscribing, please wait...</p>
      {:else}
        <form on:submit|preventDefault={handleSubscribe} bind:this={ref}>
          <div class="row d-flex justify-content-center">
            <div class="col-md-5 col-7">
              {#if !message && !error}
                <div class="form-outline form-white mb-4">
                  <input
                    type="email"
                    name="email"
                    id="form5Example29"
                    class="form-control"
                    aria-label="readonly input example"
                    required
                  />
                  <label class="form-label" for="form5Example29"
                    >email</label
                  >
                </div>
              {:else if message}
                <p class="mt-1">{message}</p>
              {:else if error}
                <p>{error}</p>
              {/if}
            </div>
            <!--Grid column-->

            <!--Grid column-->
            <div class="col-auto">
              <!-- Submit button -->
              {#if !message && !error}
              <div class="dropdown">
                <button
                  class="btn btn-primary dropdown-toggle"
                  type="button"
                  id="dropdownMenuButton"
                  data-mdb-toggle="dropdown"
                  aria-expanded="false"
                >
                  Submit
                </button>
                <ul class="dropdown-menu" aria-labelledby="dropdownMenuButton">
                  <li><button type="submit" on:click={() => formType="subscribe/1"} class="btn btn-li"><p>Subscribe</p></button></li>
                  <li><button type="submit" on:click={() => formType="unsubscribe/1"} class="btn btn-li"><p>Unsubscribe</p></button></li>
                  <li><button type="submit" on:click={() => formType="sendMail"} class="btn btn-li"><p>Send Test Email</p></button></li>
                </ul>
              </div>
              {:else}
              <button type="submit" class="btn btn-outline-light mb-4">
                Go Back
              </button>
              {/if}
            </div>
            <!--Grid column-->
          </div>
          <!--Grid row-->
        </form>
      {/if}
    </section>
    <!-- Section: Form -->
  </div>
  <div class="copyright p-3" style="background-color: rgba(0, 0, 0, 0.2);">
    © 2022 Copyright:
    <a href="#">restrosite.com</a>
  </div>
</footer>

<style>
  .container-fluid {
    background-color: #2d2d2d !important;
    margin: 0;
  }
  .copyright,
  a {
    text-align: center;
    color: rgba(255, 255, 255, 0.5);
  }
  .form-outline.form-white .form-control {
    border: 1px dotted;
  }
  .form-label {
    top: 5px;
    background-color: #2d2d2d;
    padding: 0 5px;
  }
  .btn-li {
    box-shadow: none;
  }
  li:not(:last-child) {
    border-bottom: 1px solid #eee;
  }
  li p {
    margin-bottom: 0;
  }
  li:hover p{
    color: #1266f1;
  }
</style>
