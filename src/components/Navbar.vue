<template >
    <header>
        <nav>
            <RouterLink id="logo-url" class="links" to="/"><img :src="logo" :alt="alt" id="logo"></RouterLink>
            <RouterLink class="links" to="/">Home</RouterLink>
            <RouterLink class="links" to="/pedidos">Pedidos</RouterLink>
        </nav>
    </header>
</template>

<script>
import { RouterLink } from 'vue-router'

export default {
    name: 'Navbar',

    props: ['logo', 'alt']
}
</script>
<style scoped>
nav {
    background-color: #222;
    border-bottom: 4px solid #111;
    padding: 15px 50px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
}

#logo-url {
    margin: auto;
    margin-left: 0;
}

#logo {
    max-width: 40px;
    max-height: 40p;
}

.links {
    margin: 12px;
    text-decoration: none;
    font-size: 1.8rem;
    color: #fcba03;
    transition: .5s;
}

.links:hover {
    color: #fff
}
</style>