<template>
  <tr>
    <td>
      <select v-model="data.類型" @change="ChangeType(data)">
        <option v-for="(item, index) in Type" :key="index" :value="item.Value">{{item.Display}}</option>
      </select>
    </td>
    <td>
      <select v-if="data.類型=='屬性'" v-model="data.屬性">
        <option v-for="(item, index) in 屬性分類" :key="index" :value="item.Value">{{item.Display}}</option>
      </select>
      <select v-if="data.類型=='攻擊方式'" v-model="data.屬性">
        <option v-for="(item, index) in 攻擊分類" :key="index" :value="item.Value">{{item.Display}}</option>
      </select>
      <select v-if="data.類型=='特性'" v-model="data.屬性">
        <optgroup v-for="(group, gindex) in 特性分類" :key="gindex" :label="group.label">
          <option v-for="(item, index) in group.elementes" :key="index" :value="item.Value">{{item.Display}}</option>
        </optgroup>
      </select>
      <select v-if="data.類型=='技能'" v-model="data.屬性">
        <option v-for="(item, index) in 技能分類" :key="index" :value="item.Value">{{item.Display}}</option>
      </select>
    </td>
    <td style="min-width:20px"><div v-if="data.類型=='屬性' || data.類型=='攻擊方式'"><input type="number" min="0" v-model="data.數值" />%</div></td>
    <td><button @click="add">+</button></td>
    <td><button @click="remove(dkey)">-</button></td>
  </tr>
</template>
<script setup>
  import {ref, reactive} from "@vue/reactivity";
  const Type = reactive([
    {Value: "屬性", Display: "屬性"},
    {Value: "攻擊方式", Display: "攻擊方式"},
    {Value: "特性", Display: "特性"},
    {Value: "技能", Display: "技能"}
  ]);
  const 屬性分類 = reactive([
    {Value: "風", Display: "風"},
    {Value: "火", Display: "火"},
    {Value: "水", Display: "水"},
    {Value: "地", Display: "地"},
    {Value: "空", Display: "空"},
    {Value: "光", Display: "光"},
    {Value: "暗", Display: "暗"}
  ]);
  const 攻擊分類 = reactive([
    {Value: "物理", Display: "物理"},
    {Value: "魔力", Display: "魔力"}
  ]);
  const 特性分類 = reactive([
    {
      label: "命力",
      elementes:[
        {Value: "命力減防", Display: "敵方全體-6%防禦"},
        {Value: "命力會心抗減", Display: "敵方全體-9%會心抗性"},
        {Value: "命力加工", Display: "己方前排+6%攻擊"},
        {Value: "命力貫穿抗減", Display: "敵方全體-9%貫穿抗性"}
      ]
    },
    {
      label: "咒力",
      elementes:[
        {Value: "咒力加攻", Display: "己方前排+6%攻擊"}
      ]
    }
  ]);
  const 技能分類 = reactive([
    {Value: "地白老", Display: "地白老"},
    {Value: "風蜥蜴", Display: "風蜥蜴"},
    {Value: "光拉米", Display: "光拉米"},
    {Value: "光靜", Display: "光靜"},
    {Value: "空中二", Display: "空中二"}
  ]);
  const ChangeType = (d)=>{
    switch(d.類型)
    {
      case "屬性":
        d.屬性 = 屬性分類[0].Value;
        break;
      case "攻擊方式":
        d.屬性 = 攻擊分類[0].Value;
        break;
      case "特性":
        d.屬性 = 特性分類[0].elementes[0].Value;
        break;
      case "技能":
        d.屬性 = 技能分類[0].Value;
        break;
    }
  };
</script>
<script>
export default {
  name: "LeaderPicker",
  props: {
    dkey: Number,
    data: Object,
    add: Function,
    remove: Function
  }
};
</script>

<style scoped>
</style>
