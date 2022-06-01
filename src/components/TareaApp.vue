<template>
  <h1>Tareas</h1>
  <TareasForm />
  <TareaItems
    v-for="tarea in tareas"  :key="tarea.id"
    :tarea="tarea"
  />
  <div class="alert alert-dark mt-3" v-if="tareas.length === 0 ">
      Sin Tareas Pendientes 🙌
  </div>
  {{tareas}}
</template>

<script>
import { ref } from '@vue/reactivity'
import { provide, watchEffect } from '@vue/runtime-core';
import TareasForm from './TareaForm.vue'
import TareaItems from './TareaItem.vue'
export default {
    components:{
        TareasForm,
        TareaItems
    },
    setup(){
        const tareas = ref([]);
        provide("tareas", tareas);

        if(localStorage.getItem("tareas")){
            tareas.value = JSON.parse(localStorage.getItem("tareas"));
        }

        watchEffect(()=>{
            localStorage.setItem("tareas", JSON.stringify(tareas.value))
        })

         return { 
             tareas
         }
    }
}
</script>

<style>

</style>