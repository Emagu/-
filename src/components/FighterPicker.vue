<template>
  <tr>
    <td>
      {{data.標題}}
    </td>
    <td >
      <select v-if="data.類型=='屬性'" v-model="data.屬性">
        <option v-for="(item, index) in 屬性分類" :key="index" :value="index">{{item.Display}}</option>
      </select>
      <select v-if="data.類型=='攻擊方式'" v-model="data.屬性">
        <option v-for="(item, index) in 攻擊分類" :key="index" :value="index">{{item.Display}}</option>
      </select>
      <select v-if="data.類型=='技能'" v-model="data.屬性">
        <option v-for="(item, index) in 技能分類" :key="index" :value="index">{{item.Display}}</option>
      </select>
      <select v-if="data.類型=='特性'" v-model="data.屬性">
        <option v-for="(item, index) in 特性分類" :key="index" :value="index">{{item.Display}}</option>
      </select>
      <select v-if="data.類型=='奧義類型'" v-model="data.屬性">
        <option v-for="(item, index) in 奧義類型" :key="index" :value="index">{{item.Display}}</option>
      </select>
      <div v-if="Is轉魂技能()">
        隨機<input width="30px" type="number" min="0" />奧義魂
        <input width="30px" type="number" min="0" />技能魂
          <input width="30px" type="number" min="0" />加護魂
        轉換成
        <input width="30px" type="number" min="0" />奧義魂
        <input width="30px" type="number" min="0" />技能魂
        <input width="30px" type="number" min="0" />加護魂
        <select>
          <option>奧義</option>
          <option>技能</option>
          <option>加護</option>
        </select>魂
        <select>
          <option>所有</option>
          <option>專屬</option>
        </select>
        計量上升
        <input width="30px" type="number" min="0" />% 持續
        <select>
          <option>1T</option>
          <option>2T</option>
          <option>3T</option>
          <option>戰鬥結束</option>
        </select>
      </div>
      <div v-if="data.數值類型=='%' || data.數值類型=='Point'"><input type="number" min="0" v-model="data.數值" /><label v-if="data.數值類型=='%'">%</label></div>
      <div v-if="data.數值類型 == 'Text'"><input type="text" v-model="data.數值" /></div>
    </td>
  </tr>
</template>
<script setup>
  import {ref, reactive} from "@vue/reactivity";
  import elements from "../database/Common/Element.json";
  import attackTypes from "../database/Common/AttackType.json";
  import finalSkill from "../database/Common/FinalSkill.json";
  import inborn from "../database/Fighter/Inborn.json";
  import Skill from "../database/Fighter/Skill.json";
  const 屬性分類 = reactive(elements);
  const 攻擊分類 = reactive(attackTypes);
  const 特性分類 = reactive(inborn);
  const 技能分類 = reactive(Skill);
  const 奧義類型 = reactive(finalSkill);
</script>
<script>
export default {
  name: "LeaderPicker",
  props: {
    data: Object
  },
  methods: {
    Is轉魂技能() {
      return this.data.類型=='技能' && this.data.屬性 == 1;
    },
  },
};
</script>

<style scoped>
</style>
