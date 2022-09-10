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
      <RouterView v-slot="{Component}">
        <Transition name="page" mode="out-in">
          <component :is="Component" />
        </Transition>
      </RouterView>
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

.page-enter-active,
.page-leave-active {
  transition: 600ms ease all;
}

.page-enter-from,
.page-leave-to {
  opacity: 0;
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
