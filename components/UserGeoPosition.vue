<template>
  <div>
    <p>Huidige positie gebruiker: </p>
    <p v-if="location">latitude : {{this.location.latitude}}, longitude: {{this.location.longitude}}</p>
    <p v-else-if="!location">Nog geen positie!</p>
  </div>
</template>

<script>
  import Vue from 'vue'

  export default Vue.extend({
    name: 'UserGeoPositionComponent',
    data: function () {
      return {
        location: false,
      }
    },
    beforeMount: function () {
      navigator.geolocation.watchPosition((position) => {
        this.location = position.coords;
      });
    }
  })
</script>
