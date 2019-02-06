<template>
  <div class="about">
    <h1>This is an about page</h1>
    <button @click="volverHome()">Volver a home</button>
  </div>
</template>
<script>
export default {
  created() {
    setTimeout(() => this.$router.push("/"), 2000);
  },
  methods: {
    volverHome() {
      this.$router.push("/"); //home
    }
  }
};
</script>
