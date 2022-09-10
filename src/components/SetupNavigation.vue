<template>
    <div class="nav-group">
        <div class="logo">
          <img src="../assets/images/partly-cloudy.png" alt="logo">
          <h2>webbot</h2>
        </div>
        <div class="time">
          Local Time: {{ date }}
        </div>
    </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
    name: "SetupNavigation",
    data() {
        return {
           date: new Date().toLocaleTimeString("en-US", {
                hour: "2-digit",
                minute: "2-digit",
            }),
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
    font-family: 'Rampart One', cursive;
    font-size: 1.5rem;
    text-transform: capitalize;
  }
  img {
    width: 4em;
  }
  .time {
    font-family: 'Rampart One', cursive;
    font-size: 1.5rem;
    color: #ccc;
  }
  @media screen and (max-width: 768px) {
    .logo {
      display: flex;
      gap: 0.5rem;
      font-family: 'Rampart One', cursive;
      font-size: 1rem;
      text-transform: capitalize;
    }
    img {
      width: 5em;
    }
    .time {
      font-family: 'Rampart One', cursive;
      font-size: 1.1rem;
      color: #fff;
    }
  }
</style>