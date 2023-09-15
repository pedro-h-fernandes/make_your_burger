<template >
    <header>
            <nav>
                <RouterLink class="links" to="/"><img src="" alt="logo de hambueger" id="logo"></RouterLink>
                <RouterLink class="links" to="/">Home</RouterLink>
                <RouterLink class="links" to="/pedidos">Pedidos</RouterLink>
            </nav>
    </header>
</template>

<script>
import { RouterLink } from 'vue-router'

export default {
    name: 'Navbar',
}
</script>
<style scoped>
    nav {
        display: flex;
        justify-content: flex-start;
    }

    .links {
        margin: 0 10px;
    }
</style>