<svelte:head>
	<title>Statistics</title>
</svelte:head>


<script>
    import { onMount } from "svelte";

    const API_KEY = "YOUR_API_KEY_HERE";
    const URL = "CORONA STAT URL";
    let stats = [];

    onMount(async function() {
        const response = await fetch(URL);
        const json = await response.json();
        stats = json["stats"];
    });
</script>

<h1>Here is statistics about the Corona Virus around the world</h1>

<div class="container">
    {#each stats as stat}
        <div class="card">
            <h1>{stats.info.title}</h1>
            <div class="card-body">
                <h3>Test!</h3>
            </div>
        </div>
    {/each}
</div>
