<script lang="ts">
import SetupNavigation from "./components/SetupNavigation.vue";
import { defineComponent } from "vue";

export default defineComponent({
  name: "App",
  components: {
    SetupNavigation,
  },
});
</script>

<template>
    <div class="body">
      <SetupNavigation />
      <RouterView />
    </div>
</template>

<style scoped>
    .body {
      margin: 0;
      padding: 0;
    }
</style>
