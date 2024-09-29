<template>
  <header class="bg-light py-3">
    <div class="container d-flex justify-content-between align-items-center">
      <div class="d-flex align-items-center">
        <img src="../assets/vuejslogo.png" alt="Vue Logo" class="logo">
        <img src="../assets/markdownlogo.png" alt="Markdown Logo" class="logo ms-3">
        <h1 class="ms-3">MarkDown Translator</h1>
      </div>
      <button class="btn btn-outline-dark" @click="toggleTheme">
        Cambiar a {{ darkTheme ? 'Tema Claro' : 'Tema Oscuro' }}
      </button>
    </div>
  </header>
</template>

<script>
export default {
  data() {
    return {
      darkTheme: false,
    };
  },
  methods: {
    toggleTheme() {
      this.darkTheme = !this.darkTheme;
      document.body.classList.toggle('dark-theme', this.darkTheme);
    },
  },
};
</script>

<style scoped>
.logo {
  height: 40px;
}
h1 {
  font-size: 1.8rem;
  font-weight: bold;
  margin: 0;
}
</style>
