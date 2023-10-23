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
    background: url('/img/burger.jpg') no-repeat 0 -350px;
    background-size:cover;
    width: 100%;
    height: 65vh;
    display: flex;
    align-items: center;
    justify-content: flex-start;
}

h1 {
    padding: 2%;
    width: 500px;
    padding-left: 5%;
    color: #fff;
    text-align: center;
    font-size: 4.5rem;
    background-color: #222;
}
</style>