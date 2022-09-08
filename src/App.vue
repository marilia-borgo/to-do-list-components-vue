<template>
  <div id="app">
    <TaskList v-if="!formsShow" ></TaskList>
    <button v-on:click="formsShow=true"> Criar nova Task</button>
    <div class="mostrarformulario" v-if="formsShow">
      <TaskForm></TaskForm>
    </div>
  </div>
 
</template>

<script>

import TaskList from "./components/TaskList.vue"
import TaskForm from "./components/TaskForm.vue"




export default {
  name: "App",
  components: {
    TaskList,
    TaskForm,
},
data: function(){
  return{
    formsShow: false,
}
}}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}


</style>
