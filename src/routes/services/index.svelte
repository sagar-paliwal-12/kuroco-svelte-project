<script context="module">
    export const load = async ({fetch}) => {
        const res = await fetch(`${import.meta.env.VITE_BASE_URL}/rcms-api/3/services`);
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
<div class="container my-4">
    <div class="row row-cols-1 row-cols-md-3 g-4">
        {#each data.list as item}
        <div class="col" on:click={() => handleCardClick(item.topics_id)}>
          <div class="card h-100">
            <img src={item.ext_3.url} class="card-img-top" alt="Hollywood Sign on The Hill"/>
            <div class="card-body">
              <h5 class="card-title">{item.subject}</h5>
              <p class="card-text">
                {item.ext_2}
            </div>
          </div>
        </div>
        {/each}
    </div>
</div>


<div class="modal fade" id="exampleModal2" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
        <div class="modal-content">
        <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Modal title</h5>
            <button type="button" class="btn-close" data-mdb-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
            <form>
                <!-- Email input -->
                <!-- {#if loginStatus !== null}
                <p style="color: {messageColor[loginStatus]}">{resultMessage}</p>
                {/if} -->
                <div class="form-outline mb-4">
                  <input name="ext_1" type="email" id="form1Example1" class="form-control"/>
                  <label class="form-label" for="form1Example1">Email address</label>
                </div>
              
                <!-- Password input -->
                <div class="form-outline mb-4">
                  <input name="password" type="password" id="form1Example2" class="form-control"/>
                  <label class="form-label" for="form1Example2">Password</label>
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
    .card-img-top { 
        height: 200px;
    }
</style>