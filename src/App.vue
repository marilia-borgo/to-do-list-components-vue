<template>
  <div id="app">
    <div class="search-box">
    <button class="btn-search"><i class="fas fa-search"></i></button>
    <input type="text" class="input-search" placeholder="Tasks...">
  </div>

    <TaskList v-if="!formsShow" ></TaskList>
    <button class="novaTask" v-on:click="formsShow=true"> Criar nova Task</button>
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
  height: 100vh;
  background: #eeaecc;
  background: radial-gradient(circle, #eeaecc 0%, #403ea1 100%);
  

} 

.novaTask{
  margin-top: 3%;
  height: 60px;
  width: 230px;
}
.search-box{
  width: fit-content;
  height: fit-content;
  position: relative;
}
.input-search{
  height: 50px;
  width: 50px;
  border-style: none;
  padding: 5px;
  font-size: 18px;
  letter-spacing: 2px;
  outline: none;
  border-radius: 25px;
  transition: all .5s ease-in-out;
  background-color: #403ea1;
  padding-right: 40px;
  color:#fff;
}
.input-search::placeholder{
  color:rgba(255,255,255,.5);
  font-size: 18px;
  letter-spacing: 2px;
  font-weight: 100;
}
.btn-search{
  width: 50px;
  height: 50px;
  border-style: none;
  font-size: 20px;
  font-weight: bold;
  outline: none;
  cursor: pointer;
  border-radius: 50%;
  position: absolute;
  right: 0px;
  color:#ffffff ;
  background-color:transparent;
  pointer-events: painted;  
}
.btn-search:focus ~ .input-search{
  width: 300px;
  border-radius: 0px;
  background-color: transparent;
  border-bottom:1px solid rgba(255,255,255,.5);
  transition: all 500ms cubic-bezier(0, 0.110, 0.35, 2);
}
.input-search:focus{
  width: 300px;
  border-radius: 0px;
  background-color: transparent;
  border-bottom:1px solid rgba(255,255,255,.5);
  transition: all 500ms cubic-bezier(0, 0.110, 0.35, 2);
}

</style>
