<template>
    <div id="main-banner">
        <div class="back">
            <h1>Make Your Burguer</h1>
        </div>
    </div>
</template>

<script>
export default {
    name:"Banner"
}
</script>

<style scoped>

#main-banner{
    background-image: url(/public/img/burger.jpg);
    background-position: -0 -450px;
    background-size: cover;
    height: 600px;
    display: flex;
    justify-content: flex-start;
    align-items: center;
}
@media only screen and (min-width: 700px){
    #main-banner{
        background-position: -500px -450px;
        background-size: auto;
    }
}

#main-banner .back{
    backdrop-filter: blur(70px);
    background-color: #22222252;
    padding: 20px 40px;
    border-radius: 10px;
}
#main-banner .back h1{
    z-index: 1;
    color: #fff;
    text-align: center;
    font-size: 60px;

}
</style>