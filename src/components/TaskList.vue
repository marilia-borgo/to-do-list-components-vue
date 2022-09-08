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
    margin-top: 10%;
    padding: 1%;
    width: 50%;
    filter: drop-shadow(17px 26px 21px #321450);
    background-color: #29132e;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .card{
    margin: 2px;
    background-color: #eeaecc;
    width: 90%;
    position: relative;
    overflow: hidden;
    transition: 0.2s;
    letter-spacing: 4px;
   
  }
 

  span{
    background-color: rgb(60, 216, 227);
    margin-right: 0%;
  }
  button{
    margin: 5px;
    color: #a4a883;
    background-color: #403ea1 ;
    border: 0px;
    margin-left: 1px;
  }

  a{
    text-decoration: none;
    color: #a4a883;
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