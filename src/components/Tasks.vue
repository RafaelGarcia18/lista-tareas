<template>
  <v-card>
    <v-card-title primary-title>
      {{ taskObject.tittle }}
    </v-card-title>
    <v-card-text>
      <v-row align="center" class="mx-0">
        <v-chip color="primary" outlined>
          {{ taskObject.priority }}
        </v-chip>
      </v-row>
    </v-card-text>
    <v-card-text>
      <div>{{ taskObject.responsible }}</div>
      <div>{{ taskObject.description }}</div>
    </v-card-text>
    <v-card-actions>
      <v-btn block color="red" dark @click="removeCat"> Eliminar </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: "Tasks",
  props: ["taskObject", "index"],
  data() {
    return {
      tasksStorage: [],
    };
  },

  created() {
    if (localStorage.getItem("tasks")) {
      try {
        this.tasksStorage = JSON.parse(localStorage.getItem("tasks"));
      } catch (e) {
        localStorage.removeItem("tasks");
      }
    }
  },
  methods: {
    removeCat() {
      console.log("Se presiono");
      this.tasksStorage.splice(this.index, 1);
      this.saveCats();
    },
    saveCats() {
      const parsed = JSON.stringify(this.tasksStorage);
      localStorage.setItem("tasks", parsed);
    },
  },
};
</script>

<style></style>
