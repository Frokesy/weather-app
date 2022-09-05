<template>
    <div class="nav-group">
        <div class="logo">
          <img src="../assets/images/cloudy.gif" alt="logo">
          <h2>Webbot</h2>
        </div>
        <div class="city">
          <span>Add City</span>
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
    name: "SetupNavigation",
    data() {
        return {
            Text: "Hello world from SetupNavigation",
        };
    },

});
</script>

<style>
  .nav-group {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    width: 50%;
    align-items: center;
    margin: 30px auto;
  }
  .nav-group h2 {
    font-size: 1.5rem;
  }
  .logo {
    display: flex;
    gap: 10px;
  }
  img {
    width: 3rem;
  }
  .city {
    font-size: 1.2rem;
  }

@media screen and (max-width: 768px) {
  .nav-group {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    width: 90%;
    align-items: center;
    margin: 30px auto;
  }
  .nav-group h2 {
    font-size: 1.5rem;
  }
  .logo {
    display: flex;
    gap: 10px;
  }
  img {
    width: 3rem;
  }
  .city {
    font-size: 1.2rem;
  }
}
</style>