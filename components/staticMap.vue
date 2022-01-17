<template>
    <img width="500" class="mapboxStaticMap" v-bind:src="'https://api.mapbox.com/styles/v1/mapbox/outdoors-v11/static/'+ poisString +'/auto/'+width+'x'+height+'@2x?access_token=pk.eyJ1Ijoia2V2aWIxMzM3IiwiYSI6ImNqcDg2cGk2ZjBrcnMzdm8wd2Zjc3R6b2oifQ.quWVgUCWuWb_EJgMMQY9eA&attribution=false&logo=false'">
</template>

<script lang="ts">
    import Vue from "vue";

    export default Vue.extend({
        props: {
            centerLongitude: Number,
            centerLatitude: Number,
            pois: Array,
            completedPois: Array,
            width: Number,
            height: Number
        },
        data: function () {
            return {
                poisString: ""
            }
        },
        methods: {
            updateMarkers: function() {
                // Default poi string with current location pin
                this.poisString = `pin-s-pitch+285A98(${this.centerLongitude},${this.centerLatitude})`;

                // Add all pois to string
                this.pois.map((poi: any, index: number) => {
                    if (this.completedPois.includes(index)) {
                        this.poisString += `,pin-s-heart+5ffa01(${poi['longitude']},${poi['latitude']})`
                    } else {
                        this.poisString += `,pin-s-heart+ea4335(${poi['longitude']},${poi['latitude']})`
                    }
                })
            }
        },
        created: function() {
            this.updateMarkers();
        },
        watch: {
            centerLongitude: function() {
                this.updateMarkers();
            },
            centerLatitude: function() {
                this.updateMarkers();
            },
            completedPois: function() {
                this.updateMarkers();
            }
        }
    });
</script>