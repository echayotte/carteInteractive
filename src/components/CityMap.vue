<template>
    <div class="col-md-9">
        <div id="cityMap" class="map"></div>
    </div>
</template>


<script>
    import svgIcons from "../assets/icons.json";

    // voir tuto : https://travishorn.com/interactive-maps-with-vue-leaflet-5430527353c8
    export default {
        props: ["subCategoriesSelected"],

        data() {
            return {
                map: null,
                tileLayer: null,
                markerList: []
            };
        },

        mounted() {
            this.initMap();
        },

        methods: {
            initMap() {
                this.map = L.map("cityMap").setView([44.4491, 1.454], 14);
                this.tileLayer = L.tileLayer(
                    "https://cartodb-basemaps-{s}.global.ssl.fastly.net/rastertiles/voyager/{z}/{x}/{y}.png",
                    {
                        maxZoom: 18,
                        attribution:
                            '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>, &copy; <a href="https://carto.com/attribution">CARTO</a>'
                    }
                );

                this.tileLayer.addTo(this.map);
            }
        },

        watch: {
            subCategoriesSelected: {
                handler() {

                    // this.subCategoriesSelected.places = array of "places" property from places.json
                    let SelectedSubCategoryPlacesList = this.subCategoriesSelected.places;
                    let infosOfAllPlaces = [];

                    if (SelectedSubCategoryPlacesList) {

                        for (let marker of this.markerList) {
                            this.map.removeLayer(marker);
                        }

                        for (let place in SelectedSubCategoryPlacesList) {
                            let infoPlace = [];

                            infoPlace.push(SelectedSubCategoryPlacesList[place].lat);
                            infoPlace.push(SelectedSubCategoryPlacesList[place].lon);
                            infoPlace.push(SelectedSubCategoryPlacesList[place].description);
                            infosOfAllPlaces.push(infoPlace);
                        }

                        for (let infoOfOnePlace in infosOfAllPlaces) {
                            let longitude = infosOfAllPlaces[infoOfOnePlace][0];
                            let latitude = infosOfAllPlaces[infoOfOnePlace][1];
                            let customIcon = L.icon({
                                iconUrl: svgIcons[this.subCategoriesSelected.icon],
                                iconSize: [30, 30]
                            });

                            let marker = L.marker([longitude, latitude], {
                                icon: customIcon
                            })
                                .bindPopup(infosOfAllPlaces[infoOfOnePlace][2])
                                .addTo(this.map);

                            this.markerList.push(marker);
                        }
                    }
                }
            }
        }
    };
</script>


<style scoped>
    .map {
        height: 100vh;
        width: 100vw;
    }
</style>



