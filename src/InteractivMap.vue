<template>
    <div class="container-fluid">
        <div class="row">
            <Menu v-on:event1="showSelectedSubCategories" :categories="jsonPlaces"/>
            <CityMap :subCategoriesSelected="watchsubCategoriesSelected"/>
        </div>
    </div>
</template>


<script>
    import Menu from "./components/Menu";
    import CityMap from "./components/CityMap";
    import jsonFile from "./assets/places.json";

    export default {
        name: "InteractivMap",
        components: {
            Menu,
            CityMap
        },

        data() {
            return {
                jsonPlaces: jsonFile,
                watchsubCategoriesSelected: {}
            };
        },

        methods: {
            showSelectedSubCategories(SelectedChildren) {
                //finally get the result from CityMap, passing from Subcategory, then Menu
                this.watchsubCategoriesSelected = SelectedChildren;
            }
        }
    };
</script>


<style>
</style>
