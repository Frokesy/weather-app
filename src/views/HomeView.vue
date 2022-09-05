<script lang="ts">
import { defineComponent, ref } from "vue";
import axios from "axios";

export default defineComponent({
  name: "HomeView",
  data() {
    return {
      searchInput: '' as String | Number,
      searchResults: [] as Array<any>, 
    }
  },
  updated() {
    const Token = 'pk.eyJ1IjoiZnJva2VzIiwiYSI6ImNsN2tnODRoMTA2Z28zb25sbTA3aWk1Z2EifQ.g_6YVlr32dq2k9DB1fFLcA'
    const getSearchResults = async () => {
      const result = await axios.get(`https://api.mapbox.com/geocoding/v5/mapbox.places/${this.searchInput}.json?access_token=${Token}&types=place&autocomplete=true&limit=5`)
      this.searchResults = result.data.features
    }
    getSearchResults()
  }
})
</script>

<template>
  <main>
    <div class="search">
      <input type="text" v-model="searchInput" placeholder="Search for any city here...">
      <ul>
        <li v-for="searchResult in searchResults" :key="searchResult.id">{{ searchResult.place_name }}</li>
      </ul>
    </div>
  </main>
</template>

<style>
  .search {
    width: 50%;
    margin: 0 auto;
  }
  .search input {
    width: 100%;
    padding: 10px 0px;
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
    box-shadow: 1px 1px 1px #000;
  }
  ul {
    box-shadow: 0 0 10px #000;
    padding: 2px;
    display: flex;
    flex-direction: column;
    color: #ccc;
  }
  li {
    padding: 10px;
    border-bottom: 1px solid #ccc;
    list-style-type: none;
  }
  
  @media screen and (max-width: 768px) {
    .search {
      width: 80%;
      margin: 0 auto;
    }
    .search input {
      width: 100%;
      padding: 10px 0px;
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
      border-bottom: 1px solid #ccc;
      box-shadow: 1px 1px 1px #000;
    }
    ul {
      box-shadow: 0 0 10px #000;
      padding: 2px;
      display: flex;
      flex-direction: column;
      color: #ccc;
    }
    li {
      padding: 10px;
      border-bottom: 1px solid #ccc;
      list-style-type: none;
    }
  }
</style>