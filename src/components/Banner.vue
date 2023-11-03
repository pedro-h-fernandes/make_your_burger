<template>
    <div id="main-banner">
        <h1>Make your Burger</h1>
        
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
    width: 100%;
    height: 72vh;
    display: flex;
    align-items: center;
    justify-content: flex-start;
}

h1 {
    padding: 2%;
    width: 35%;
    padding-left: 5%;
    color: #fff;
    text-align: center;
    font-size: 4.5rem;
    background-color: #222;
}

@media screen and (max-width: 777px){
    h1{
        font-size: 3.5rem;
    }
}
@media screen and (max-width: 375px){
    h1{
        font-size: 2.5rem;
    }
}
</style>