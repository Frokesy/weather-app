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
    width: 4rem;
  }
  .time {
    font-family: 'Rampart One', cursive;
    font-size: 1.5rem;
    color: #ccc;
  }
  @media screen and (max-width: 768px) {
    .logo {
      display: flex;
      justify-content: space-between;
      gap: 0.2rem;
      font-size: 0.5rem;
      text-transform: capitalize;
    }
    .logo h2 {
      font-size: 20px;
    }
    .logo img {
      width: 3rem;
      height: 5rem;
    }
    .time {
      font-family: 'Rampart One', cursive;
      font-size: 12px;    }
  }
</style>