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
  font-family: Staatliches,Open Sauce,Albert Sans,Poppins,sans-serif;
  width: 50%;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
}

@media screen and (max-width: 768px) {
  .body {
    font-family: Staatliches,Open Sauce,Albert Sans,Poppins,sans-serif;
    width: 90%;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
  }
  }
</style>
