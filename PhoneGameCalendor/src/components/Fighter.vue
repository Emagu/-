<template>
    <table>
        <tr>
            <td>
                <select>
                    <option v-for="(item, index) in Type" :key="index" :value="item.Value">{{item.Display}}</option>
                </select>
            </td>
            <td>
                
            </td>
        </tr>
    </table>
</template>

<script setup>
  import {reactive} from "@vue/reactivity";
  const Type = reactive([
    {Value: "屬性", Display: "屬性"},
    {Value: "攻擊方式", Display: "攻擊方式"},
    {Value: "特性", Display: "特性"},
    {Value: "轉魂技能", Display: "轉魂技能"}
  ]);
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