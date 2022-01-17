<template>
  <div class="text-center">
    <h1>Opmerking werking</h1>
    <p>Applicatie werkt op hardcoded data, applicatie zou eigenlijk aan een api moeten hangen</p>
    <p>Gebruiker posities wordt opgehaald doormiddel van de javascript navigator. Dit is niet altijd accuraat en beter alternatief zou er een zijn van google/mapbox/etc.</p>
    <p>Applicatie genereert een statische kaart die ingezoomd staat zodat alle pois in beeld zijn.</p>
    <p>De gebruiker wordt aangegeven met een marker met daarin in poppetje. In principe als de gebruiker zou bewegen dan beweegt deze ook me.</p>
    <p>Als je binnen 25 meter bent van een POI dan wordt deze opengeklapt (Je kunt nep bewegen met de knoppen boven de kaart, dit verlaagt de afstand. Is alleen voor debugging/testing bedoeld)</p>
    <p>Een poi kun je afvinken dan wordt deze weer dichtgeklapt en wordt de marker groen op de kaart (Dit zou normaal ook naar de api gestuurd worden, zodat je progressie wordt onthouden)</p>
    <p>Route aanmaken bevat een formulier waarbij je alle benodige gegevens kan invoeren (Deze zou dan naar de api worden verstuurd)</p>
    <p>PS: Opmaak ben ik totaal niet goed in, dus ik maak gebruiker voor bootstrap-vue ook heb ik niet een alternatieve opmaak gemaakt voor de telefoon, maar alles werkt nog wel gewoon</p>
    <h1>Rest opmerkingen</h1>
    <p>Het was even wennen om vue/nuxt onder de knie te krijgen, maar heb +- 10 uur ingestoken en merk nu al dat ik vloeiender taken uitwerkte</p>
    <p>Misschien moet er voor gebruik een eigen certficaat worden toegevoegd <a href="https://stackoverflow.com/a/57895543" target="_blank">Uitleg hier</a></p>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage'
})
</script>
