<template>
    <div class="nav-group">
        <div class="logo">
          <img src="../assets/images/cloudy.gif" alt="logo">
          <h2>WEBBOT</h2>
        </div>
        <div class="city">
          Local Time: {{ time }}
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { useRoute, useRouter } from "vue-router";
import { uid } from "uid";

export default defineComponent({
    name: "SetupNavigation",
    data() {
        return {
            time: new Date().toLocaleTimeString("en-US", {
                hour: "2-digit",
                minute: "2-digit",
            }),
            route: useRoute(),
            router: useRouter(),
            savedCities: [] as any,
        };
    },
});
</script>

<style>
  .nav-group {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .logo {
    display: flex;
    gap: 1rem;
  }
  img {
    width: 5em;
  }
</style>