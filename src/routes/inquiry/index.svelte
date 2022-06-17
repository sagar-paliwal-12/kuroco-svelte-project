<script>
    import { onMount } from "svelte";
    import FormPlaceholder from './components/FormPlaceholder.svelte'

    let data = "";
    let activeTab = "enquiry";
    const tabList = {"enquiry": "6", "feedback": "5"}

    const handleLoad = async (id) => {
        if (id === "6") {
            activeTab = "enquiry";
        } else {
            activeTab = "feedback";
        }
        data = ""
        const res = await fetch(`${import.meta.env.VITE_BASE_URL}/rcms-api/3/form/${id}`);
        data = await res.json();
        
        return {
            props: {
                data,
            },
        };
    }
    onMount(() => handleLoad("6"))

    const refs = [];
    let message = "";
    let error = "";

    const handleFormSubmit = async (id) => {
        if (id === "") {
            message="";
            error = "";
            return;
        }
        const formInputElements = Array.from(refs[id]).filter(
            (elm) => elm.tagName.toLowerCase() === 'input' || elm.tagName.toLowerCase() === "textarea"
        )

        const body = formInputElements
        .map((elm) => ({ [elm.name]: elm.value }))
        .reduce((prev, cur) => ({ ...prev, ...cur }), {})

        try {
            const submit = await fetch(`${import.meta.env.VITE_BASE_URL}/rcms-api/3/form?id=${id}`, {
                method: "POST",
                body: JSON.stringify({
                    ...body,
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
<div class="container row justify-content-around">
    <div class="col-lg-3 col-12 my-4">
        <div
            class="nav flex-column nav-tabs text-center"
            id="v-tabs-tab"
            role="tablist"
            aria-orientation="vertical"
        >
        {#each Object.entries(tabList) as [tab, form_id]}
        <a
          class="nav-link {tab === activeTab ? "active" : ''}"
          id="v-tabs-{tab}-tab"
          data-mdb-toggle="tab"
          href="#v-tabs-{tab}"
          role="tab"
          aria-controls="v-tabs-{tab}"
          aria-selected="true"
          on:click={() => handleLoad(form_id)}
          >{tab}</a
        >
        {/each}
        </div>
    </div>
  
    <div class="col-lg-4 col-12 my-4">
        <div class="tab-content" id="v-tabs-tabContent">
            {#each Object.entries(tabList) as [tab, form_id], index}
            <div
                class="tab-pane fade row justify-content-center {activeTab === tab ? "show active": ""}"
                id="v-tabs-{tab}"
                role="tabpanel"
                aria-labelledby="v-tabs-{tab}-tab"
            >
                <div class="card">
                    <div class="card-body justify-content-center">
                        {#if !message && !error && data}
                        <h1>{data.details.inquiry_name}</h1>
                        <form on:submit|preventDefault={() => handleFormSubmit(form_id)} bind:this={refs[form_id]}>
                            {#each Object.entries(data.details.cols) as [key, value]}
                            {#if value.required != 0}
                            <div class="form-outline form-black mb-4">
                                {#if value.title === "message" || value.title === "issue"}
                                <textarea name={key} class="form-control" id="textAreaExample" rows="4"></textarea>
                                {:else}
                                <input type={value.title} name={key} id="form4Example1" class="form-control" />
                                {/if}
                                <label class="form-label" for="form4Example1">
                                    {value.title}
                                    {#if value.required === 2}
                                    <span>*</span>
                                    {/if}
                                </label>
                            </div>
                            {/if}
                            {/each}                        
                            <button type="submit" class="btn btn-primary btn-block mb-4 col-6">Send</button>
                        </form>
                        {:else if message}
                        <h4>{message}</h4>
                        <button on:click={() => handleFormSubmit("")} class="btn btn-primary btn-block mb-4 col-6">Submit another response</button>
                        {:else if error}
                        <h4>{error}</h4>
                        <button on:click={() => error = ""} class="btn btn-primary btn-block mb-4 col-6">Go back</button>
                        {:else}
                        <FormPlaceholder />
                        {/if}
                    </div>
                </div>
            </div>
            {/each}
        </div>
    </div>
</div>

<style>
    .container {
        min-height: 73vh;
    }
    label span {
        color: red;
    }
    .form-outline .form-control {
        border: 1px solid rgba(0, 0, 0, 0.8);
    }
    .form-label {
        top: 5px;
        background-color: #fff;
        padding: 0 5px;       
    }
    .form-control::-moz-focus-inner {
        border: 1px solid red;
    }
</style>