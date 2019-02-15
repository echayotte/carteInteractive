<template>
    <div>
        <div v-for="subCategory in subCategories" :key="subCategory.id" @click="showSelectedSubCategories(subCategory)" class="sub m-2">
            {{ subCategory.name }}
        </div>
    </div>
</template>


<script>
    export default {
        props: ["subCategories"],

        methods: {
            showSelectedSubCategories(SelectedChildren) {
                //pass the result to Menu file
                this.$emit("event2", SelectedChildren);
            }
        }
    };
</script>


<style scoped>
    .sub {
        color: #007bff;
        text-transform: lowercase;
        padding-left: 5%;
        font-family: "Quicksand", sans-serif;
    }
    .sub::first-letter {
        text-transform: uppercase;
    }
    .sub:hover {
        color: rgba(29, 74, 122, 0.733);
        cursor: pointer;
    }
</style>