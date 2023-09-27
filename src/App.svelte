<script>
  import MovieTile from "./components/MovieTile.svelte";
  import MovieOverlay from "./components/MovieOverlay.svelte";
  let name = "MovieMate";
  import { onMount } from "svelte";
  import axios from "axios";

  let movieList = [];
  let movieData = null; // Define movieData at the component level
  let searchValue = "";
  let apiKey = import.meta.env.VITE_OMDB_API_KEY;
  let errors = "";
  let selectedMovie = null;
  const handleInput = (e) => {
    searchValue = e.target.value;
    searchData();
  };
  const searchData = async () => {
    const url = `https://omdbapi.com/?s=${searchValue}&apikey=${apiKey}`;

    const response = await axios.get(url);
    if (response.data.Response === "True") {
      movieList = response.data.Search;
      errors = "";
    } else {
      console.log("error: ", response.data.Error);
      errors = response.data.Error;
      movieList = [];
    }
  };

  const recommendData = async () => {
    const url =
      "https://api.consumet.org/movies/dramacool/info?id=drama-detail/vincenzo";

    try {
      const { data } = await axios.get(url);
      movieData = data;
      console.log("movieData: ", movieData);
    } catch (err) {
      console.error(err.message);
    }
  };

  function handleMovieClick(movie) {
    selectedMovie = movie;
    console.log("selectedMovie: ", selectedMovie);
  }

  function handleCloseOverlay() {
    selectedMovie = null;
  }

  onMount(() => {
    // recommendData();
  });
</script>

<main>
  <h1>Welcome to {name}!</h1>
  <div class="controlls">
    <input type="text" placeholder="Start typing.." on:input={handleInput} />
    {#if movieList.length > 0}
      <button type="button" on:click={searchData}>Update</button>
    {/if}
  </div>
  {#if selectedMovie}
    <MovieOverlay {selectedMovie} on:closeOverlay={handleCloseOverlay} />
  {/if}
  <div>
    <!-- {#if movieData}
      <h5>Movie Title: {movieData.title}</h5>
      <p>Description: {movieData.description}</p>
    {:else}
      <p>Loading...</p>
    {/if} -->
    {#if movieList.length > 0}
      <h5>
        ({movieList.length} results)
      </h5>
      <ul>
        {#each movieList as movie}
          {#if movie}
            <button on:click={handleMovieClick(movie)}>
              <MovieTile {movie} />
            </button>
          {:else}
            <p>not found</p>
          {/if}
        {/each}
      </ul>
    {:else}
      <p>{errors}</p>
    {/if}
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
