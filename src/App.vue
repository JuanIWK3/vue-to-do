<script lang="ts">
import { defineComponent } from "@vue/runtime-core";
import Todo from "./components/Todo.vue";
export default defineComponent({
  components: {
    Todo,
  },
});
</script>

<template>
  <Todo />
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
