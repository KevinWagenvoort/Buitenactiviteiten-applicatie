<template>
  <div>
    <p>Huidige positie gebruiker: </p>
    <p v-if="hasLocation">latitude : {{this.location.latitude}}, longitude: {{this.location.longitude}}</p>
    <p v-else-if="!hasLocation">Nog geen positie!</p>
  </div>
</template>

<script lang="ts">
  import Vue from 'vue'

  export default Vue.extend({
    name: 'UserGeoPositionComponent',
    data: function () {
      return {
        hasLocation: false,
        location: {},
      }
    },
    beforeMount: function () {
      navigator.geolocation.watchPosition((position) => {
        this.hasLocation = true;
        this.location = position.coords;
      });
    }
  })
</script>
