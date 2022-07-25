<template>
    <table>
        <Picker v-for="(item, index) in data.elements" :key="index" :data="item"></Picker>
    </table>
</template>

<script setup>
    import Picker from "./FighterPicker.vue";
</script>
<script>
export default {
    props: {
        data: Object
    }
}
</script>

<style scoped>
</style>