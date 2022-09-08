<template>
<div class="center">
  <div class="container">
    
    <input v-model="task.title" placeholder="Tarefa">
    <select v-model="task.project">
        <option disabled value="">Qual a área?</option>
        <option>Front-End</option>
        <option>Back-End</option>
        <option>Devops</option>
    </select>
    <input id="date" type="date" v-model="task.dueTo">
    <button> <a href="" v-on:click="post()"> Adicionar Task </a></button>
</div>
</div>
</template>

<script>
import axios from 'axios'
export default {
    name:"TaskForm",
    data: function(){
  return{
    tasks: [],
    task: {
      "id": '',
      "title":'',
      "dueTo": '',
      "project": '',
      "usuario": '',
      isShow:false,
    },
  }
},
methods:{
    async post(){
        const task = this.task
        const req = await axios.post('http://localhost:3000/tasks',task)
  },
}
}
</script>

<style>
.center{
    display: flex;
    flex-direction: column;
    align-items: center;
    }
.container{
    margin-top: 10%;
    padding: 1%;
    width: 50%;
    filter: drop-shadow(17px 26px 21px #321450);
    background-color: #29132e;
    display: flex;
    flex-direction: column;
    align-items: center;
}

input, select{
    
  margin: 20px;
  height: 48px;
  width: 91%;
  font-weight: 500;
  border-radius: 4px;
  font-size: 14px;
  line-height: 22px;
  letter-spacing: 0.5px;
  outline: none;
  color: #29132e;
  background-color: #eeaecc;
  border: none;
  -webkit-transition: all 200ms linear;
  transition: all 200ms linear;
  box-shadow: 0 4px 8px 0 #15151533;
}
</style>