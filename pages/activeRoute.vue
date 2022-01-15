<template>
    <b-container v-if="hasParams">
        <b-row>
            <b-col>
                <h1>{{ title }}</h1>
            </b-col>
            <b-col>
                {{debugDistance}}
                <b-button @click="debugDistance += 50">Nep dicherbij lopen</b-button>
                <b-button @click="debugDistance -= 50">Nep verderweg lopen</b-button>
            </b-col>
        </b-row>
        <b-row>
            <b-col>
                <template v-for="(poi, index) in pois">
                    <b-card v-if="poi.distance <= distanceTrigger" :key="index" :header="poi.title + ' - Afstand: ' + poi.distance" :img-src="poi.image">
                        <p class="card-text mt-2">{{ poi.description }}</p>
                    </b-card>
                    <div v-else-if="poi.distance > distanceTrigger" :key="index" class="card outOfReach">
                        <div class="card-header">Opdracht: Tel de berkenbomen - Afstand: {{ poi.distance }}</div>
                    </div>
                </template>
            </b-col>
            <b-col>
                <b-img src="https://azuremapscodesamples.azurewebsites.net/SiteResources/screenshots/Snap-drawn-line-to-roads.jpg" />
            </b-col>
        </b-row>
    </b-container>
</template>

<script lang="ts">
    import Vue from 'vue';

    export default Vue.extend({
        props: ['route'],
        data: function () {
            let pois : any[] = [];

            return {
            debugDistance: 0,    
            distanceTrigger: 50,
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
                        poi['distance'] = calculateDistanceInMeters(poi["latitude"], poi["longitude"], position.coords.latitude, position.coords.longitude) - this.debugDistance;
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

<style scoped>
    .card.outOfReach {
        filter: grayscale(100);
    }
</style>