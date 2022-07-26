<template>
  <tr>
    <td>
      <select v-model="data.類型" @change="ChangeType(data)">
        <option v-for="(item, index) in Type" :key="index" :value="item.Display">{{item.Display}}</option>
      </select>
    </td>
    <td>
      <select v-if="data.類型=='屬性'" v-model="data.屬性">
        <option v-for="(item, index) in 屬性分類" :key="index" :value="index">{{item.Display}}</option>
      </select>
      <select v-if="data.類型=='攻擊方式'" v-model="data.屬性">
        <option v-for="(item, index) in 攻擊分類" :key="index" :value="index">{{item.Display}}</option>
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
  import elements from "../database/Common/Element.json";
  import attackTypes from "../database/Common/AttackType.json";
  import inborn from "../database/Leader/Inborn.json";
  import Attr from "../database/Leader/Attr.json";
  import Skill from "../database/Leader/Skill.json";
  const Type = reactive(Attr);
  const 屬性分類 = reactive(elements);
  const 攻擊分類 = reactive(attackTypes);
  const 特性分類 = reactive(inborn);
  const 技能分類 = reactive(Skill);
  const ChangeType = (d)=>{
    switch(d.類型)
    {
      case "屬性":
        d.屬性 = 0;
        break;
      case "攻擊方式":
        d.屬性 = 0;
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
