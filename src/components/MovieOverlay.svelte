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

<style>
  .overlay-container {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.7);
    backdrop-filter: blur(6px);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 999;
  }

  .overlay-content {
    background-color: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.2);
  }

  .close-button {
    position: absolute;
    top: 10px;
    right: 10px;
    cursor: pointer;
    font-size: 20px;
  }
</style>
