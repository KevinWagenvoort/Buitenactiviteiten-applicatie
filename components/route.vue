<template>
    <b-col class="route text-center">
        <h1>{{ route.id }}: {{ route.title }}</h1>
        <p>{{ route.description }}</p>
        <b-button :to="{name: 'activeRoute', params: { route: JSON.stringify(route) } }">Start deze route</b-button>
        <hr />
    </b-col>
</template>

<script>
    export default {
        props: ['route']
    }
</script>