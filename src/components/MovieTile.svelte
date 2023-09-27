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
