<template>
  <div class="container">
    <input v-model="task.title" placeholder="Adicionar Tarefa">
    <select v-model="task.project">
        <option disabled value="">Tipo task</option>
        <option>Front-End</option>
        <option>Back-End</option>
        <option>Devops</option>
    </select>
    <input id="date" type="date" v-model="task.dueTo">
    <button> <a href="" v-on:click="post()"> Adicionar Task </a></button>
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
 .tasks{
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 50%;
    background-color: #d8dcba;
  }
</style>