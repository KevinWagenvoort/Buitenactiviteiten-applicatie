<template>
    <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
        <b-navbar-brand><NuxtLink to="/">Buitenactiviteiten</NuxtLink></b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
            <b-nav-item><NuxtLink to="/routes">Alle routes</NuxtLink></b-nav-item>
            <b-nav-item><NuxtLink to="/routes">Routes aanmaken</NuxtLink></b-nav-item>
        </b-navbar-nav>
        </b-collapse>
    </b-navbar>
    </div>
</template>

<style scoped>
    a {
        color:black;
    }

    .nuxt-link-exact-active {
        font-weight: bold;
    }
</style>