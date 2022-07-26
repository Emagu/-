<template>
    <table>
        <Picker v-for="(item, index) in data.elements" :key="index" :dkey="index" :data="item" :add="add" :remove="remove"></Picker>
    </table>
</template>

<script setup>
    import Picker from "./LeaderPicker.vue";
    var data1 = defineProps();
    const add = ()=>{
        data1.data.elements.push({
            類型: "屬性",
            屬性: 0,
            數值: 0
        });
    }
    const remove = (index)=>{
        data1.data.elements.splice(index, 1);
    }
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