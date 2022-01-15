<template>
    <div v-if="routes.length > 0" id="routesList">
        <li v-for="(route, index) in routes" :key="index">
            <route :key="route.id" :route="route"/>
        </li>
    </div>
</template>

<script lang="ts">
    import Vue from 'vue'

    export default Vue.extend({
    name: 'routes',
    data: function () {
        return {
            routes: [{}]
        }
    },
    beforeMount: function () {
        this.routes = [
            {
                "id": "A134",
                "title": "Bospad advontuur",
                "pois": [
                    {
                        "title": "Bezienswaardigheid: De wilde Bes",
                        "image": "https://picsum.photos/600/300/?image=25",
                        "description": "Als je vanuit dit punt om je heen kijkt zie je in de verte een oude boederij liggen genaamd “De wilde Bes”. Deze boederij is gebouwt in het jaar 1902. Gedurende de tweede wereldoorlog werd deze woning gebruikt als buurtcentrum. Het plaatselijke verzet organiseerde hier in het geheim bijeenkomsten. Tegenwoordig staat deze boederij op de Unesco werelderfgoed lijst en word het [foto] door de plaatselijke bevolking gebruikt voor de wekelijkste sjoelwestrijden. [link naar wikipedia pagina met meer informatie]",
                        "latitude": 52.291779,
                        "longitude": 5.965167
                    },
                    {
                        "title": "Opdracht: Tel de berkenbomen",
                        "image": "https://picsum.photos/600/300/?image=12",
                        "description": "Tel hoeveel berkenbomen er op dit kruispunt staan.",
                        "latitude": 52.294779,
                        "longitude": 5.965567
                    }
                ]
            },
            {
                "id": "A134",
                "title": "Bospad advontuur 2",
                "pois": [
                    {
                        "title": "Bezienswaardigheid: De wilde Bes",
                        "description": "Als je vanuit dit punt om je heen kijkt zie je in de verte een oude boederij liggen genaamd “De wilde Bes”. Deze boederij is gebouwt in het jaar 1902. Gedurende de tweede wereldoorlog werd deze woning gebruikt als buurtcentrum. Het plaatselijke verzet organiseerde hier in het geheim bijeenkomsten. Tegenwoordig staat deze boederij op de Unesco werelderfgoed lijst en word het [foto] door de plaatselijke bevolking gebruikt voor de wekelijkste sjoelwestrijden. [link naar wikipedia pagina met meer informatie]",
                        "latitude": 52.291779,
                        "longitude": 5.965167
                    },
                    {
                        "title": "Opdracht: Tel de berkenbomen",
                        "description": "Tel hoeveel berkenbomen er op dit kruispunt staan.",
                        "latitude": 52.294779,
                        "longitude": 5.965567
                    }
                ]
            },
        ];
    }
    })
</script>