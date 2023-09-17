<script>
export let movieTitle;
export let movieUrl;
export let movieImg;

</script>

<tile>
<div class="container">
    <div class="img"><img src={movieImg} alt=""></div>
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
    margin-bottom: 2rem;
    padding: 2%;
    border-radius: 2rem;
}
img{
    max-width:200px; 
    border-radius: 2rem;

}
</style>