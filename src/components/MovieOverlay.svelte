<script>
  export let selectedMovie;
  import { createEventDispatcher } from "svelte";

  const dispatch = createEventDispatcher();

  function closeOverlay() {
    dispatch("closeOverlay");
  }
</script>

<overlay>
  <div class="overlay-container">
    <div class="overlay-content">
      <div class="img"><img src={selectedMovie.Poster} alt="" /></div>
      <a href={selectedMovie.Url}>
        <div class="title">{selectedMovie.Title}</div>
      </a>
      <button class="close-button" on:click={closeOverlay}>&times;</button>
    </div>
  </div>
</overlay>
