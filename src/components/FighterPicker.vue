<template>
  <tr>
    <td>
      {{data.標題}}
    </td>
    <td >
      <select v-if="data.類型=='屬性'" v-model="data.屬性">
        <option v-for="(item, index) in 屬性分類" :key="index" :value="item.Value">{{item.Display}}</option>
      </select>
      <select v-if="data.類型=='攻擊方式'" v-model="data.屬性">
        <option v-for="(item, index) in 攻擊分類" :key="index" :value="item.Value">{{item.Display}}</option>
      </select>
      <select v-if="data.類型=='技能'" v-model="data.屬性">
        <option v-for="(item, index) in 技能分類" :key="index" :value="item.Value">{{item.Display}}</option>
      </select>
      <select v-if="data.類型=='特性'" v-model="data.屬性">
        <option v-for="(item, index) in 特性分類" :key="index" :value="item.Value">{{item.Display}}</option>
      </select>
      <select v-if="data.類型=='奧義類型'" v-model="data.屬性">
        <option v-for="(item, index) in 奧義類型" :key="index" :value="item.Value">{{item.Display}}</option>
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
    </td>
  </tr>
</template>
<script setup>
  import {ref, reactive} from "@vue/reactivity";
  
  const 屬性分類 = reactive([
    {Value: "未選擇", Display: "未選擇"},
    {Value: "風", Display: "風"},
    {Value: "火", Display: "火"},
    {Value: "水", Display: "水"},
    {Value: "地", Display: "地"},
    {Value: "空", Display: "空"},
    {Value: "光", Display: "光"},
    {Value: "暗", Display: "暗"}
  ]);
  const 攻擊分類 = reactive([
    {Value: "未選擇", Display: "未選擇"},
    {Value: "物理", Display: "物理"},
    {Value: "魔力", Display: "魔力"}
  ]);
  const 特性分類 = reactive([
    {Value: '總員-加護增幅I',Display: '每3回合增加4加護計量'},
    {Value: '總員-加護增幅II',Display: '每3回合增加6加護計量'},
    {Value: '總員-技能增幅I',Display: '每3回合增加3技能點'},
    {Value: '總員-技能增幅II',Display: '每3回合增加5技能點'},
    {Value: '總員-奧義增幅I',Display: '每3回合增加自身1奧義計量'},
    {Value: '總員-奧義增幅II',Display: '每3回合增加自身2奧義計量'},
    {Value: '總員-先手加護I',Display: '開場增加7加護計量'},
    {Value: '總員-先手加護II',Display: '開場增加11加護計量'},
    {Value: '總員-先手技能I',Display: '開場增加4技能點'},
    {Value: '總員-先手技能II',Display: '開場增加6技能點'},
    {Value: '總員-先手奧義I',Display: '開場增加自身3奧義計量'},
    {Value: '總員-先手奧義II',Display: '開場增加自身5奧義計量'},
    {Value: '總員-加護急速I',Display: '前3回合 每回合增加3加護計量'},
    {Value: '總員-加護急速II',Display: '前3回合 每回合增加5加護計量'},
    {Value: '總員-奧義急速II',Display: '前3回合 每回合增加自身1奧義技量'},
    {Value: '總員-奧義急速II',Display: '前3回合 每回合增加自身2奧義技量'},
    {Value: '總員-奧義急速III',Display: '前3回合 每回合增加自身3奧義技量'}
  ]);
  const 技能分類 = reactive([
    {Value: "未選擇", Display: "未選擇"},
    {Value: "轉魂", Display: "轉魂類型"},
    {Value: "攻擊", Display: "攻擊類型"},
    {Value: "防禦", Display: "防禦類型"},
    {Value: "特殊", Display: "特殊類型"}
  ]);
  
  const 奧義類型 = reactive([
    {Value: "未選擇", Display: "未選擇"},
    {Value: "群攻", Display: "群攻奧義"},
    {Value: "單體", Display: "單體奧義"},
  ]);
  const 可選技能 = reactive([
    {Value: "未選擇", Display: "未選擇"},
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
    data: Object
  },
  methods: {
    Is轉魂技能() {
      return this.data.類型=='技能' && this.data.屬性 == '轉魂';
    },
  },
};
</script>

<style scoped>
</style>
