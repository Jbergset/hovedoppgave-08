<script>
    import { onMount } from "svelte";

    const API_KEY = "6fb8a769aee04be38d2c3e7c14e4d77c";
    const URL = `https://newsapi.org/v2/top-headlines?country=us&q=corona&sortBy=publishedAt&apiKey=${API_KEY}`;
	let articles = [];
	
	
	onMount(async function() {
    const response = await fetch(URL);
    const json = await response.json();
    articles = json["articles"];
    });

    function changeLanguage() {

    }
</script>

<h1> De siste nyhetene fra USA angående Corona Viruset </h1>

<div class="konteiner">
        {#each articles as article}
            <div class="card">
                <img alt="artikkel bilder"src="{article.urlToImage}">
                <div class="card-body">
                    <h3>{article.title}</h3>
                    <p> {article.description} </p>
                    <a href="{article.url}">Les artikkelen</a>
                </div>
            </div>
        {/each}
</div>

<style>
h1 {
    color: orangered;
    font-family: 'kalam';
}

.konteiner {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
    grid-gap: 20px;
	
}

.konteiner > .card img {
    max-width: 100%;
}
</style>
