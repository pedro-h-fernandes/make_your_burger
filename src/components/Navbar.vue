<template >
    <header>
        <nav class="navbar fixed-top navbar-expand-sm py-4 px-5 d-flex justify-content-md-between" data-bs-theme="dark">
            <div class="container-fluid d-flex justify-content-space-between">
                <RouterLink id="logo-url" class="links" to="/"><img :src="logo" :alt="alt" id="logo"></RouterLink>

                <button id="toggler-btn" class="navbar-toggler" type="button" data-bs-toggle="collapse"
                    data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false"
                    aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>


                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                    <ul class="navbar-nav ms-auto my-2 my-lg-0">
                        <li class="nav-item">
                            <RouterLink class="links" to="/">Home</RouterLink>
                        </li>
                        <li class="nav-item">
                            <RouterLink class="links" to="/pedidos">Pedidos</RouterLink>
                        </li>
                    </ul>
                </div>
            </div>
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

#logo {
    max-width: 40px;
    max-height: 40px;
}

nav{
    background-color: #222;
}

.links {
    margin: 12px;
    text-decoration: none;
    font-size: 1.9rem;
    color: #fcba03;
    transition: .5s;
}

.links:hover {
    color: #fff
}
</style>