<template></template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "DarkMode",
  setup() {
    document.documentElement.setAttribute("data-dark", "true");
    document.body.classList.add("darker");
  },
});
</script>
<style scoped lang="scss">
@media (prefers-color-scheme: dark) {
  [data-dark="true"] .darker {
    color: #fff;
    background-color: #000;
  }
}
</style>
