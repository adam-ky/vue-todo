<template>
  <footer>
    <p>Copyright &copy; 2023</p>
    <router-link to="/about">About</router-link>
  </footer>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "AppFooter",
});
</script>

<style scoped>
footer {
  margin-top: 30px;
  text-align: center;
}
</style>
