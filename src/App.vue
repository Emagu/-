<template>
  <div class="flex-container">
    <table>
      <tr>
        <td>加護</td>
        <td><button @click="ChangePick(0, '加護', 'Leader')">編輯</button></td>
      </tr>
      <tr>
        <td>先鋒1</td>
        <td><button @click="ChangePick(1, '先鋒1', 'Fighter')">編輯</button></td>
      </tr>
      <tr>
        <td>先鋒2</td>
        <td><button @click="ChangePick(2, '先鋒2', 'Fighter')">編輯</button></td>
      </tr>
      <tr>
        <td>先鋒3</td>
        <td><button @click="ChangePick(3, '先鋒3', 'Fighter')">編輯</button></td>
      </tr>
      <tr>
        <td>候補1</td>
        <td><button @click="ChangePick(4, '候補1', 'Fighter')">編輯</button></td>
      </tr>
      <tr>
        <td>候補2</td>
        <td><button @click="ChangePick(5, '候補2', 'Fighter')">編輯</button></td>
      </tr>
      <tfoot>
        <td>
        </td>
        <td>
          <button>匯入</button>
          <button>匯出</button>
        </td>
      </tfoot>
    </table>
    <h1>編輯區</h1>
    <component v-if="EditIndex.Index > -1" :is="EditIndex.Index == 0 ? Leader : Fighter" :data="GetData()"></component>
  </div>
</template>

<script setup>
  import Leader from "./components/Leader.vue";
  import Fighter from "./components/Fighter.vue";
  import FighterAttr from "./database/Fighter/Attr.json";
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
      if(EditIndex.Type == 'Leader')
      {
        EditData.push({
          name: EditIndex.Name,
          type: EditIndex.Type,
          elements : [{
            類型: "屬性",
            屬性: 0,
            數值: 0
          }]
        });
      }
      else
      {
        var newFighterAttr = [];
        FighterAttr.forEach(type => {
          newFighterAttr.push({
            標題: type.Display,
            類型: type.Value,
            屬性: 0,
            數值類型: type.Type,
            數值: type.Type == "Text" ? "" : 0
          })
        });
        EditData.push({
          name: EditIndex.Name,
          type: EditIndex.Type,
          elements : newFighterAttr
        });
      }
      return GetData();
    }
    return result;
  };
  const ChangePick = (Index, Name, Type)=>{
    EditIndex.Index = Index;
    EditIndex.Name = Name;
    EditIndex.Type = Type;
  };
  localStorage.TestData = "test";
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
button {
  background-color: aqua;
}
</style>
