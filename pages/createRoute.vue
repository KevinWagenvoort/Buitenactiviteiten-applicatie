<template>
    <b-container>
        <b-row>
            <b-col>
                <h1 class="text-center">Route aanmaken</h1>
            </b-col>
        </b-row>
        <div>
            <b-form-group id="routeTitleGroup" label="Titel" label-for="routeTitle">
                <b-form-input type="text" id="routeTitle" trim></b-form-input>
            </b-form-group>
            <b-form-group id="routeDescriptionGroup" label="Omschrijving" label-for="routeDescription">
                <b-form-textarea id="routeDescription" trim></b-form-textarea>
            </b-form-group>
        </div>
        <hr class="mt-2 mb-3"/>
        <b-row>
            <b-col>
                <h2 class="text-center">Point of interrest toevoegen <b-button variant="outline-success" @click="incrementPoiAmount()">+</b-button></h2>
            </b-col>
        </b-row>
        <div v-for="index in poiAmount" :key="index">
            <b-form-group id="poiTitleGroup" label="Titel" label-for="poiTitle">
                <b-form-input type="text" id="poiTitle" trim></b-form-input>
            </b-form-group>
            <b-form-group id="poiDescriptionGroup" label="Omschrijving" label-for="poiDescription">
                <b-form-textarea id="poiDescription" trim></b-form-textarea>
            </b-form-group>
            <b-form-group id="poiLongitudeGroup" label="Longitude" label-for="poiLongitude">
                <b-form-input type="number" id="poiLongitude" trim></b-form-input>
            </b-form-group>
            <b-form-group id="poiLatitudeGroup" label="Latitude" label-for="poiLatitude">
                <b-form-input type="number" id="poiLatitude" trim></b-form-input>
            </b-form-group>
            <b-form-group id="poiImageUploadGroup" label="Afbeelding" label-for="poiImageUpload">
                <b-form-file type="file" id="poiImageUpload" placeholder="Kies een afbeelding of plaats deze hier..." drop-placeholder="Plaats afbeelding hier..."></b-form-file>
            </b-form-group>
            <hr class="mt-2 mb-3"/>
        </div>
        <div>
            <b-button variant="success" @click="console.debug('Send to api')">Opslaan</b-button>
        </div>
    </b-container>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
    data: function() {
        return {
            poiAmount: 0
        }
    },
    methods: {
        incrementPoiAmount: function() {
            this.poiAmount++;
        }
    }
})
</script>