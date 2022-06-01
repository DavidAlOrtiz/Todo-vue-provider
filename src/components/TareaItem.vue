<template>
  <div
    class="
      alert alert-warning
      mt-3
      d-flex
      justify-content-between
      aling-items-center
    "
  >
    <p class="m-0 " :class="{'tachado-Texto' : tarea.estado}">{{ tarea.texto }}</p>
    <div>
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="16"
        height="16"
        fill="currentColor"
        class="bi bi-arrow-clockwise mx-2 text-success"
        viewBox="0 0 16 16"
        role="button"
        @click="modificar(tarea.id)"
        v-if="tarea.estado"
      >
        <path
          fill-rule="evenodd"
          d="M8 3a5 5 0 1 0 4.546 2.914.5.5 0 0 1 .908-.417A6 6 0 1 1 8 2v1z"
        />
        <path
          d="M8 4.466V.534a.25.25 0 0 1 .41-.192l2.36 1.966c.12.1.12.284 0 .384L8.41 4.658A.25.25 0 0 1 8 4.466z"
        />
      </svg>
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="16"
        height="16"
        fill="currentColor"
        class="bi bi-check-circle-fill mx-2 text-success"
        viewBox="0 0 16 16"
        role="button"
        @click="modificar(tarea.id)"
        v-else
      >
        <path
          d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zm-3.97-3.03a.75.75 0 0 0-1.08.022L7.477 9.417 5.384 7.323a.75.75 0 0 0-1.06 1.06L6.97 11.03a.75.75 0 0 0 1.079-.02l3.992-4.99a.75.75 0 0 0-.01-1.05z"
        />
      </svg>
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="16"
        height="16"
        fill="currentColor"
        class="bi bi-x-circle-fill text-danger"
        viewBox="0 0 16 16"
        role="button"
        @click="eliminarTarea(tarea.id)"
      >
        <path
          d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zM5.354 4.646a.5.5 0 1 0-.708.708L7.293 8l-2.647 2.646a.5.5 0 0 0 .708.708L8 8.707l2.646 2.647a.5.5 0 0 0 .708-.708L8.707 8l2.647-2.646a.5.5 0 0 0-.708-.708L8 7.293 5.354 4.646z"
        />
      </svg>
    </div>
  </div>
</template>

<script>
import { inject } from "@vue/runtime-core";
export default {
  props: {
    tarea: {
      type: Object,
      required: true,
    },
  },
  setup() {
    const tareas = inject("tareas");

    const eliminarTarea = (id) => {
      tareas.value = tareas.value.filter((t) => t.id !== id);
    };

    const modificar = (id) => {
      tareas.value = tareas.value.map((t) => {
        if (t.id == id) {
          t.estado = !t.estado;
        }
        return t;
      });
    };

    return {
      eliminarTarea,
      modificar,
    };
  },
};
</script>

<style scoped>
  .tachado-Texto {
    text-decoration: line-through;
  }
</style>>
