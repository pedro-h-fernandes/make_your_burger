<template>
    <div id="main-banner" class="container-fluid row">
        <div id="titulo" class="col-4 col-md-5 col-xlg-5 p-5 justify-content-end">
            <h1>Make your Burger</h1> 
        </div>
    </div>
</template>

<script>
export default {
    name: 'Banner',
}
</script>

<style scoped>
#main-banner {
    background: url('/img/burger.jpg');
    background-size:cover;
    background-position: center center;
    height: 72vh;
    display: flex;
    align-items: center;
    justify-content: flex-start;
}

#titulo{
    background-color: #222;
}

h1 {
    padding: 2%;
    font-size: 3vw;
    padding-left: 5%;
    color: #fff;
    text-align: center;
    background-color: #222;
}


@media screen and (max-width: 425px){
    h1{
        font-size: 4vw;
    }
}
</style>