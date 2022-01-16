<template>
    <b-container v-if="hasParams">
        <b-row>
            <b-col>
                <h1>{{ title }}</h1>
            </b-col>
            <b-col>
                <b-button @click="debugDistance += 50">Nep dicherbij lopen</b-button>
                <b-button @click="debugDistance -= 50">Nep verderweg lopen</b-button>
            </b-col>
        </b-row>
        <b-row>
            <b-col>
                <template v-for="(poi, index) in pois">
                    <div v-if="completedPois.includes(index)" :key="index" class="card completed">
                        <div class="card-header">{{poi.title}} - Afgevinkt</div>
                    </div>
                    <b-card v-else-if="poi.distance <= distanceTrigger" :key="index" :header="poi.title + ' - Afstand: ' + poi.distance" :img-src="poi.image">
                        <p class="card-text mt-2">{{ poi.description }}</p>
                        <b-button @click="completePoi(index)">Afvinken</b-button>
                    </b-card>
                    <div v-else-if="poi.distance > distanceTrigger" :key="index" class="card outOfReach">
                        <div class="card-header">{{poi.title}} - Afstand: {{ poi.distance }}</div>
                    </div>
                </template>
            </b-col>
            <b-col v-if="hasLocation">
                <StaticMap
                    :centerLongitude="userLongitude"
                    :centerLatitude="userLatitude"
                    :pois="pois"
                    :completedPois="completedPois"
                />
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
            let completedPois : number[] = [];

            return {
            debugDistance: 0,    
            distanceTrigger: 25,
            hasParams: false,
            title: "TITLE",
            id : "ID",
            pois: pois,
            hasLocation: false,
            userLatitude: 0,
            userLongitude: 0,
            completedPois: completedPois
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
                    this.userLatitude = position.coords.latitude;
                    this.userLongitude = position.coords.longitude;

                    // Calculate distance to poi
                    pois.map(poi => {
                        poi['distance'] = calculateDistanceInMeters(poi["latitude"], poi["longitude"], position.coords.latitude, position.coords.longitude) - this.debugDistance;
                    })

                    this.pois = pois;
                }, (err) => {
                    console.error(err);
                }, {
                    enableHighAccuracy: true,
                    maximumAge: 0
                });
            }
        },
        methods: {
            completePoi: function(index: number) {
                if (!this.completedPois.includes(index)) this.completedPois.push(index);
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