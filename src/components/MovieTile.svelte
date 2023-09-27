<script>
  export let movie;
</script>

<tile>
  <div class="container">
    <div class="img"><img src={movie.Poster} alt="" /></div>
    <a href={movie.Url}>
      <div class="title">{movie.Title}</div>
    </a>
  </div>
</tile>

<style>
  tile {
    cursor: pointer;
  }
  .container {
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    background-color: antiquewhite;
    padding: 2%;
    border-radius: 2rem;
    max-width: 618px;
    margin: 2rem auto;
  }
  img {
    max-width: 200px;
    border-radius: 2rem;
  }
</style>
