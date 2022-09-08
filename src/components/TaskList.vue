<template>
<div class="TaskList">
  <div class="tasks">
    <div v-for="tarefa in tasks" class="card" :key="tarefa.id">
      <p class="lead">{{ tarefa.title }}</p>
      <p>Terminar até: {{tarefa.dueTo}}</p>
      <div class="badge"><span>{{ tarefa.project }}</span></div>
      
      <button v-on:click.prevent="showEdit(tarefa.id)">Editar</button>
      <button v-on:click.prevent="deleteTask(tarefa.id)"><a href="">Excluir</a></button>
      <div class="edit"  v-if="tarefa.isShow" >
      <input v-model="tarefa.title" placeholder="Adicionar Tarefa">
    <select v-model="tarefa.project">
        <option disabled value="">Tipo task</option>
        <option>Front-End</option>
        <option>Back-End</option>
        <option>Devops</option>
    </select>
    <input id="date" type="date" v-model="tarefa.dueTo">
    <button> <a href="" v-on:click="updateTasks(tarefa.id, tarefa.title,tarefa.project,tarefa.dueTo)"> Atualizar task </a></button>
  </div>
    </div>

  </div>
</div>
</template>

<script>
import axios from 'axios'

export default {
name: "TaskList", 
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
  async showEdit(id){
    const taskData = {
    isShow: true
  }
  const req = await axios.patch(`http://localhost:3000/tasks/${id}`, taskData)
  .then((response => {
    console.log('Tarefa salva', response.data)
  }))
  this.getTasks()
    },
updateTasks(id,title,project,dueTo){
  const taskData = {
    title: title,
    project: project,
    dueTo: dueTo,
    isShow:false
  }
  axios.put(`http://localhost:3000/tasks/${id}`, taskData)
  .then((response => {
    console.log('Tarefa salva', response.data)
  }))
},
  
 

getTasks() {
  axios.get('http://localhost:3000/tasks')
  .then(response => this.tasks = response.data)
  .catch(function (error) {
  console.log(error);

});
},
setResults () {
        this.tasks = response.data;
},
async deleteTask(id){
      const req = await axios.delete(`http://localhost:3000/tasks/${id}`)
      this.getTasks()
}
},
created(){
  this.getTasks()
},
};
</script>


<style>
  .TaskList{
    display: flex;
    flex-direction: column;
    align-items: center;
   
}
  .tasks{
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 50%;
    background-color: #d8dcba;
  }

  .card{
    margin: 20px;
    background-color: #a4a883;
    width: 90%;

  }

  span{
    background-color: bisque;
    margin-right: 0%;
  }
  button{
    margin: 5px;
    color: #a4a883;
    background-color: #d8dcba;
    border: 0px;
    margin-left: 20px;
  }

  a{
    text-decoration: none;
    color: #a4a883;
  }
</style>