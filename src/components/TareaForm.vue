<template>
  <div>
    <v-card class="mx-auto" max-width="400">
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
          <v-btn color="primary" block>Agregar</v-btn>
        </v-form>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  name: "TareaForm",

  data: () => ({
    tasktemplate: {
      tittle: "",
      responsible: "",
      description: "",
      priority:""
    },
  }),
};
</script>
