<template>
  <div>
    <v-card>
      <v-card-title primary-title>
        {{ taskObject.tittle }}
      </v-card-title>
      <v-card-text>
        <p>{{ taskObject.responsible }}</p>
        <p>{{ taskObject.description }}</p>
      </v-card-text>
    </v-card>
    <pre>{{ task }}</pre>
  </div>
</template>

<script>
export default {
  name: "Tasks",
  props: ["taskObject"],
};
</script>

<style></style>
