<template>
  <div class="flex-container">
    <table>
      <tr>
        <td>加護</td>
        <td><button @click="ChangePick(0, '加護')">編輯</button></td>
      </tr>
      <tr>
        <td>先鋒1</td>
        <td><button @click="ChangePick(1, '先鋒1')">編輯</button></td>
      </tr>
      <tr>
        <td>先鋒2</td>
        <td><button @click="ChangePick(2, '先鋒2')">編輯</button></td>
      </tr>
      <tr>
        <td>先鋒3</td>
        <td><button @click="ChangePick(3, '先鋒3')">編輯</button></td>
      </tr>
      <tr>
        <td>候補1</td>
        <td><button @click="ChangePick(4, '候補1')">編輯</button></td>
      </tr>
      <tr>
        <td>候補2</td>
        <td><button @click="ChangePick(5, '候補2')">編輯</button></td>
      </tr>
    </table>
    <h1>編輯區</h1>
    <component v-if="EditIndex.Index > -1" :is="EditIndex.Index == 0 ? Leader : Fighter" :data="GetData()"></component>
  </div>
</template>

<script setup>
  import Leader from "./components/Leader.vue";
  import Fighter from "./components/Fighter.vue";
  import {reactive} from "@vue/reactivity";
  const EditIndex = reactive({
    Index: -1,
    Name: ""
  });
  const EditData = reactive([]);
  const GetData = ()=>{
    var result = EditData[EditIndex.Index];
    if(result == null)
    {
      EditData.push({
        name: EditIndex.Name,
        elements : [{
          類型: "屬性",
          屬性: "風",
          數值: 0
        }]
      });
      return GetData();
    }
    return result;
  };
  const ChangePick = (Index, Name)=>{
    console.log(Index);
    console.log(Name);
    EditIndex.Index= Index;
    EditIndex.Name= Name;
    console.log(EditIndex.Index);
  };
</script>

<style>
.grid-container {
  display: grid;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
table td {
  border: 1px solid #333;
}
</style>
