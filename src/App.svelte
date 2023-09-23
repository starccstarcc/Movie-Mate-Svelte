<script>
  import MovieTile from "./components/MovieTile.svelte"
  let name = 'You';
  import { onMount } from 'svelte';
  import axios from 'axios';

  let movieList = [];
  let movieData = null; // Define movieData at the component level
  let searchValue = 'war';
  let apiKey = process.env.OMDB_API_KEY;

const handleInput = (e) => {
  searchValue = e.target.value
}
  const searchData = async () => {
    const url = `https://omdbapi.com/?s=${searchValue}&apikey=${apiKey}`;
console.log(url)
    try {
      const response = await axios.get(url);
      movieList = response.data.Search;
      console.log(response.data);
    } catch (err) {
      console.error(err.message);
    }
  };

  const recommendData = async () => {
    const url = "https://api.consumet.org/movies/dramacool/info?id=drama-detail/vincenzo";

    try {
      const { data } = await axios.get(url);
      movieData = data; // Assign the response data to movieData
      console.log(movieData);
    } catch (err) {
      console.error(err.message);
    }
  };

  onMount(() => {
    recommendData();
  });
</script>

<main>

  <h1>Hello {name}!</h1>
  <input type="text" on:input={handleInput}>
  <button type="button" on:click={searchData}>search</button>

  <div>
    {#if movieData}
      <h5>Movie Title: {movieData.title}</h5>
      <p>Description: {movieData.description}</p>
      <!-- Display other movie information here -->
    {:else}
      <p>Loading...</p>
    {/if}
    {#each movieList as movie}
    {#if movie}
      <MovieTile movieTitle={movie.Title} moviePoster={movie.Poster} movieImg={movie.image}/>
    {:else}
      <p>not found</p>
    {/if}

    {/each}
  </div>
</main>

<style>
  main {
  text-align: center;
  padding: 1em;
  margin: 0 auto;
}

h1 {
  color: #ff3e00;
  text-transform: uppercase;
  font-size: 4em;
  font-weight: 100;
}

@media (min-width: 640px) {
  main {
    max-width: none;
  }
}

</style>
