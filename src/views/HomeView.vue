<template>
  <v-container>
    <v-row>
      <v-col cols="12" sm="10" md="5" class="mx-auto">
        <v-card>
          <v-card-text>
            <v-form v-model="valid" ref="form">
              <v-text-field
                label="Titulo"
                outlined
                :rules="[rules.required]"
                required
                v-model="tasktemplate.tittle"
                dense
              >
              </v-text-field>
              <v-text-field
                label="Responsable"
                outlined
                required
                :rules="[rules.required]"
                v-model="tasktemplate.responsible"
                dense
              >
              </v-text-field>
              <v-text-field
                label="Descripcion"
                outlined
                required
                :rules="[rules.required]"
                v-model="tasktemplate.description"
              >
              </v-text-field>
              <v-combobox
                v-model="tasktemplate.priority"
                :items="priority"
                label="Prioridad"
                outlined
                required
                :rules="[rules.required]"
                dense
              ></v-combobox>
              <v-btn color="primary" block @click="addTask">Agregar</v-btn>
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
        <tarea :taskObject="task" :index="index" v-on:update="updateTask" />
      </v-col>
    </v-row>
    <v-snackbar v-model="snackbar" timeout="2000">
      Falta uno o varios valores en el formulario
    </v-snackbar>
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
      rules: {
        required: (value) => !!value || "Required.",
      },
      valid: false,
      snackbar: false,
    };
  },
  components: {
    Tarea,
  },
  mounted() {
    this.updateTask();
  },
  methods: {
    addTask() {
      if (this.valid) {
        this.tasksStorage.push(this.tasktemplate);
        this.tasktemplate = {
          tittle: "",
          responsible: "",
          description: "",
          priority: "",
        };
        this.saveTask();
      } else {
        this.snackbar = true;
      }
      this.$refs.form.resetValidation();
    },

    saveTask() {
      const parsed = JSON.stringify(this.tasksStorage);
      localStorage.setItem("tasks", parsed);
    },
    updateTask() {
      if (localStorage.getItem("tasks")) {
        try {
          this.tasksStorage = [];
          this.tasksStorage = JSON.parse(localStorage.getItem("tasks"));
        } catch (e) {
          localStorage.removeItem("tasks");
        }
      }
    },
  },
};
</script>
