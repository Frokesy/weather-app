<script lang="ts">
import { defineComponent } from "vue";
import SearchBox from "../components/SearchBox.vue";

export default defineComponent({
  name: "HomeView",
  components: { SearchBox }
})
</script>

<template>
  <main>
    <SearchBox />
  </main>
</template>
