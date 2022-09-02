<template>
  <div class="search">
    <input type="text" placeholder="Search for any city here...">
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
    name: "SearchBox",
    

})
</script>

<style>
  .search {
    width: 80%;
    margin: 0 auto;
  }
  .search input {
    width: 100%;
    padding: 10px;
    border: none;
    background: transparent;
    border-bottom: 1px solid #ccc;
    color: #ccc;
    font-size: 1rem;
  }
  ::placeholder {
    color: #ccc;
  }
  .search input:hover {
    border: none;
    outline: none;
    border-bottom: 1px solid #ccc;
  }
  .search input:focus {
    border: none;
    outline: none;
    border-bottom: 1px solid #ccc;
  }
</style>