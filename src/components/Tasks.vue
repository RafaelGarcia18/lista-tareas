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
      <v-btn block color="red" dark @click="removeTask"> Eliminar </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: "Tasks",
  props: ["taskObject", "index"],
  data() {
    return {};
  },

  created() {},
  methods: {
    removeTask() {
      var tasksStorage = JSON.parse(localStorage.getItem("tasks"));
      tasksStorage.splice(this.index, 1);
      const parsed = JSON.stringify(tasksStorage);
      localStorage.setItem("tasks", parsed);
      this.$emit("update");
    },
  },
};
</script>

<style></style>
