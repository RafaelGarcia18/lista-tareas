<template>
  <!-- <v-container>
    <v-row>
      <v-col>
        <div>
          <p class="text-center text-h5">Lista de tareas</p>
        </div>
      </v-col>
    </v-row>
    <hello-world /> -->

  <div>
    <v-container>
      <tarea-form></tarea-form>
      <v-row>
        <v-col
          cols="12"
          sm="6"
          md="4"
          v-for="(task, index) in tasks"
          :key="index"
        >
          <tarea :taskObject="task"></tarea>
        </v-col>
      </v-row>
    </v-container>
  </div>
  <!-- </v-container> -->
</template>

<script>
import Tarea from "../components/Tasks.vue";
import TareaForm from "../components/TareaForm.vue";

export default {
  name: "Home",
  data: () => {
    return {
      tasks: [
        {
          tittle: "Titulo 1",
          responsible: "Rafael",
          description: "Esta es una descripcion",
          priority: "low",
        },
        {
          tittle: "Titulo 1",
          responsible: "Rafael",
          description: "Esta es una descripcion",
          priority: "high",
        },
        {
          tittle: "Titulo 1",
          responsible: "Rafael",
          description: "Esta es una descripcion",
          priority: "medium",
        },
        {
          tittle: "Titulo 1",
          responsible: "Rafael",
          description: "Esta es una descripcion",
          priority: "low",
        },
      ],
    };
  },
  components: {
    TareaForm,
    Tarea,
  },
};
</script>
