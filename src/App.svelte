<script>
  import MovieTile from "./components/MovieTile.svelte";
  import MovieOverlay from "./components/MovieOverlay.svelte";
  let name = "MovieMate";
  import { onMount } from "svelte";
  import axios from "axios";

  let movieList = [];
  let movieData = null;
  let searchValue = "";
  let apiKey = import.meta.env.VITE_OMDB_API_KEY;
  let errors = "";
  let selectedMovie = null;

  const handleInput = (e) => {
    searchValue = e.target.value;
    searchValue?.length > 0 ? searchData() : (errors = "");
  };
  const searchData = async () => {
    const url = `https://omdbapi.com/?s=${searchValue}&apikey=${apiKey}`;

    const response = await axios.get(url);
    if (response.data.Response === "True") {
      movieList = response.data.Search;
      console.log("movieList: ", response.data);
      errors = "";
    } else {
      console.log("error: ", response.data.Error);
      errors = response.data.Error;
      if (response.data.Error === "Too many results.") {
        errors = errors + " Please keep typing!";
      } else if (response.data.Error === "Movie not found!") {
        errors = errors + " Please check your spelling.";
      }
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
    window.scrollTo(0, 0);
    console.log(window.scroll);
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
      <div class="movie-list">
        {#each movieList as movie}
          {#if movie}
            <button class="tile-button" on:click={handleMovieClick(movie)}>
              <MovieTile {movie} />
            </button>
          {:else}
            <p>not found</p>
          {/if}
        {/each}
      </div>
    {:else}
      <p>{errors}</p>
    {/if}
  </div>
</main>
