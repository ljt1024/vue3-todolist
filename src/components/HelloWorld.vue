<template>
  <div class="container">
    <table class="gridtable">
      <tr>
        <th>id</th>
        <th>name</th>
        <th>age</th>
        <th>action</th>
      </tr>
      <tr v-for="item in dataList" :key="item.id">
        <td>{{ item.id }}</td>
        <td>{{ item.username }}</td>
        <td>{{ item.age }}</td>
        <td>
          <button @click="del(item.id)">delete</button>
        </td>
      </tr>
      <tr v-if="dataList.length<1" >
        <td colspan="4">暂无数据</td>
      </tr>
    </table>
    <div class="form">
      <div>
        <span>username: </span><input type="text" placeholder="username" v-model="username">
      </div>
      <div>
        <span>age:</span><input type="text" placeholder="password" v-model="age" style="margin-left: 50px">
      </div>
      <div class="btn">
        <button @click="submit">提交</button>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue'
export default {
  name: 'HelloWorld',
  setup() {
    let dataList = ref([
      {username:'lbc',age:24,id:1},
      {username:'lb2',age:30,id:2}
    ])
    let username = ref('')
    let age = ref('')
    function del(id) {
      dataList.value = dataList.value.filter(item=>item.id!=id)
    }
    function vad() {
      if(username.value==''||age.value==''){
        alert('用户名或年龄不能为空')
        return false
      }else{
        return true
      }
    }
    function submit() {
      if(vad()){
        dataList.value.push({
          username:username.value,
          age:age.value,
          id:dataList.value.length+1
        })
      }
    }
     return {
       dataList,
       username,
       age,
       del,
       submit,
       vad
     }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .container{
    width: 1000px;
    margin: 0 auto;
  }
  .form{
    border: 1px solid #ccc;
    margin-top: 40px;
    padding: 40px;
  }
  .form div{
    margin-top: 20px;
  }
  .form div input{
    padding: 8px;
  }
  .btn button{
    padding: 6px 15px;
    background-color:dodgerblue;
    color: #fff;
    cursor: pointer;
    border-color: dodgerblue;
    border-radius: 4px;
    outline: skyblue
  }
  .btn button:focus{
    border-color: dodgerblue;
  }
  .btn button:hover{
    border-color:cornflowerblue;
    background-color: cornflowerblue;
  }
  table.gridtable {
    width: 100%;
    font-family: verdana,arial,sans-serif;
    font-size:11px;
    color:#333333;
    border-width: 1px;
    border-color: #666666;
    border-collapse: collapse;
  }
  table.gridtable th {
    border-width: 1px;
    padding: 8px;
    border-style: solid;
    border-color: #666666;
    background-color: #dedede;
  }
  table.gridtable td {
    border-width: 1px;
    padding: 8px;
    border-style: solid;
    border-color: #666666;
    background-color: #ffffff;
   }
</style>
