<template>
  <v-container>
    <v-row>
      <v-col cols="12" sm="10" md="5" class="mx-auto">
        <v-card>
          <v-card-text>
            <v-form>
              <v-text-field
                label="Titulo"
                outlined
                v-model="tasktemplate.tittle"
                dense
              >
              </v-text-field>
              <v-text-field
                label="Responsable"
                outlined
                v-model="tasktemplate.responsible"
                dense
              >
              </v-text-field>
              <v-text-field
                label="Descripcion"
                outlined
                v-model="tasktemplate.description"
              >
              </v-text-field>
              <v-combobox
                v-model="tasktemplate.priority"
                :items="priority"
                label="Prioridad"
                outlined
                dense
              ></v-combobox>
              <v-btn color="primary" block @click="addCat">Agregar</v-btn>
            </v-form>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <v-row>
      <v-col
        cols="12"
        sm="6"
        md="4"
        v-for="(task, index) in tasksStorage"
        :key="index"
      >
        <tarea :taskObject="task" :index="index" />
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Tarea from "../components/Tasks.vue";

export default {
  name: "Home",
  data: () => {
    return {
      tasksStorage: [],
      priority: ["High", "Medium", "Low"],
      tasktemplate: {
        tittle: "",
        responsible: "",
        description: "",
        priority: "",
      },
    };
  },
  components: {
    Tarea,
  },
  mounted() {
    if (localStorage.getItem("tasks")) {
      try {
        this.tasksStorage = JSON.parse(localStorage.getItem("tasks"));
      } catch (e) {
        localStorage.removeItem("tasks");
      }
    }
  },
  methods: {
    addCat() {
      this.tasksStorage.push(this.tasktemplate);
      this.tasktemplate = {
        tittle: "",
        responsible: "",
        description: "",
        priority: "",
      };
      this.saveCats();
    },

    saveCats() {
      const parsed = JSON.stringify(this.tasksStorage);
      localStorage.setItem("tasks", parsed);
    },
  },
};
</script>
