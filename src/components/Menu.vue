<template>
    <div class="col-md-3">

        <div v-for="category in categories" :key="category.id">

            <b-btn v-b-toggle="category.id" variant="primary" class="btn-block m-1 button text-left" >
                {{ category.name }}
            </b-btn>


            <b-collapse :id="category.id">
                <Subcategory v-on:event2="showSelectedSubCategories" :subCategories="category.children"/>
            </b-collapse>

        </div>

    </div>
</template>


<script>
    import Subcategory from "./Subcategory";

    export default {
        props: ["categories"],

        components: {
            Subcategory
        },

        methods: {
            showSelectedSubCategories(SelectedChildren) {
                //pass again the result from Subcategory to IntercativMap file
                this.$emit("event1", SelectedChildren);
            }
        }
    };
</script>


<style scoped>
    button {
        font-weight: bolder;
        font-family: "Quicksand", sans-serif;
    }
    button::first-letter {
        text-transform: uppercase;
    }
</style>