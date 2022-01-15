<template>
    <div v-if="hasParams">
        <h1>{{ title }}</h1>
        <p>Deze route wordt nu getracked {{ id }}</p>
        <div>
            <li v-for="(poi, index) in pois" :key="index">
                <p>{{ poi.title }}</p>
                <p>latitude : {{poi.latitude}}, longitude: {{poi.longitude}}</p>
                <p v-if="hasLocation">Afstand: {{ poi.distance }} meter</p>
            </li>
        </div>
    </div>
</template>

<script lang="ts">
    import Vue from 'vue'

    export default Vue.extend({
        props: ['route'],
        data: function () {
            let pois : any[] = [];

            return {
            hasParams: false,
            title: "TITLE",
            id : "ID",
            pois: pois,
            hasLocation: false,
            }
        },
        beforeMount: function () {
            if (this.$route.params.route) {
                let routeParam = JSON.parse(this.$route.params.route);

                this.hasParams = true;
                this.title = routeParam.title;
                this.id = routeParam.id;
                let pois : any[] = routeParam.pois;

                
                navigator.geolocation.watchPosition((position) => {
                    this.hasLocation = true;

                    // Calculate distance to poi
                    pois.map(poi => {
                        poi['distance'] = calculateDistanceInMeters(poi["latitude"], poi["longitude"], position.coords.latitude, position.coords.longitude);
                    })

                    this.pois = pois;
                });
            }
        }
    })

    function calculateDistanceInMeters(lat1: number, lon1: number, lat2: number, lon2: number) {
            var R = 6371; // Radius of the earth in km
            var dLat = deg2rad(lat2-lat1);  // deg2rad below
            var dLon = deg2rad(lon2-lon1); 
            var a = 
                Math.sin(dLat/2) * Math.sin(dLat/2) +
                Math.cos(deg2rad(lat1)) * Math.cos(deg2rad(lat2)) * 
                Math.sin(dLon/2) * Math.sin(dLon/2)
                ; 
            var c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a)); 
            var d = R * c; // Distance in km
            return Math.round(d * 1000);
        }

    function deg2rad(deg: number) {
        return deg * (Math.PI/180)
    }
</script>