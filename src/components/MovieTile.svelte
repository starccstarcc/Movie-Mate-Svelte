<script>
export let movieTitle;
export let movieUrl;
export let moviePoster;

</script>

<tile>
<div class="container">
    <div class="img"><img src={moviePoster} alt=""></div>
    <a href={movieUrl}>
        <div class="title">{movieTitle}</div>
    </a>
</div>
</tile>

<style>
.container{
    display: flex;
    align-items: center;
    justify-content: space-evenly;
    background-color: antiquewhite;
    padding: 2%;
    border-radius: 2rem;
    max-width: 618px;
    margin: 2rem auto;
}
img{
    max-width:200px; 
    border-radius: 2rem;

}
</style>