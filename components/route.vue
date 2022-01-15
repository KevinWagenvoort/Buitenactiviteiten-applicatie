<template>
    <div>
        <h1>{{ route.title }}</h1>
        <b-button :to="{name: 'activeRoute', params: { route: JSON.stringify(route) } }">Start deze route</b-button>
    </div>
</template>

<script>
    export default {
        props: ['route']
    }
</script>