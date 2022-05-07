<template>
  <div>
    <h2>Gatos</h2>
    <div v-for="(cat, n) in cats" :key="n">
      <p>
        <span class="cat">{{ cat }}</span>
        <button @click="removeCat(n)">Eliminar</button>
      </p>
    </div>

    <p>
      <input v-model="newCat" />
      <button @click="addCat">Agregar gato</button>
    </p>
  </div>
</template>

<script>
export default {
  name: "LocasStorage",
  data: () => {
    return {
      cats: [],
      newCat: null,
    };
  },
  mounted() {
    if (localStorage.getItem("cats")) {
      try {
        this.cats = JSON.parse(localStorage.getItem("cats"));
      } catch (e) {
        localStorage.removeItem("cats");
      }
    }
  },
  methods: {
    addCat() {
      // asegurarse que el usuario efectivamente ha escrito algo
      if (!this.newCat) {
        return;
      }

      this.cats.push(this.newCat);
      this.newCat = "";
      this.saveCats();
    },
    removeCat(x) {
      this.cats.splice(x, 1);
      this.saveCats();
    },
    saveCats() {
      const parsed = JSON.stringify(this.cats);
      localStorage.setItem("cats", parsed);
    },
  },
};
</script>

<style></style>
