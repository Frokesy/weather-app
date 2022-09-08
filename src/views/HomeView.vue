<script lang="ts">
import { defineComponent, ref } from "vue";
import axios from "axios";
import { useRouter } from "vue-router";

export default defineComponent({
  name: "HomeView",
  data() {
    return {
      searchInput: '' as String | Number,
      searchResults: [] as Array<any>,
      error: false as Boolean,
      router: useRouter() 
    }
  },
  methods: {
     previewCity (searchResult: any) {
      console.log(searchResult)
       const [city, state] = searchResult.place_name.split(', ');
       console.log(city, state)
       this.router.push({
        name: 'CityView',
        params: {
          city,
          state
        },
        query: {
          lat: searchResult.geometry.coordinates[1],
          lng: searchResult.geometry.coordinates[0],
          preview: 'true'
        }
       })
    }
  },
  updated() {
    const Token: String = 'pk.eyJ1IjoiZnJva2VzIiwiYSI6ImNsN2tnODRoMTA2Z28zb25sbTA3aWk1Z2EifQ.g_6YVlr32dq2k9DB1fFLcA'
    try {
      const getSearchResults = async () => {
      const result = await axios.get(`https://api.mapbox.com/geocoding/v5/mapbox.places/${this.searchInput}.json?access_token=${Token}&types=place&autocomplete=true&limit=5`)
      this.searchResults = result.data.features
    }
    getSearchResults()
    } catch (err) {
      this.error = true
    }
  }
})
</script>

<template>
  <main>
    <div class="search">
      <input type="text" v-model="searchInput" placeholder="Search for any city here...">
      <ul v-if="searchInput">
        <p v-if="error">Something went wrong, please try again</p>
        <li v-for="searchResult in searchResults" :key="searchResult.id" @click="previewCity(searchResult)">{{ searchResult.place_name }}</li>
      </ul>
    </div>
  </main>
</template>

<style>
  .search {
    width: 100%;
    margin: 0 auto;
  }
  .search input {
    padding: 10px 0px;
    border: none;
    width: 100%;
    background: transparent;
    border-bottom: 1px solid #ccc;
    color: #d9c2a5;
    font-size: 1rem;
  }
  ::placeholder {
    color: #d9c2a5;
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
    color: #d9c2a5;
  }
  li {
    padding: 10px;
    border-bottom: 1px solid #ccc;
    list-style-type: none;
    cursor: pointer;

  }
  
  @media screen and (max-width: 768px) {
    .search {
      margin: 0 auto;
    }
    .search input {
      padding: 10px 0px;
      border: none;
      background: transparent;
      border-bottom: 1px solid #ccc;
      color: #d9c2a5;
      font-size: 1rem;
    }
    ::placeholder {
      color: #d9c2a5;
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
      color: #d9c2a5;
    }
    li {
      padding: 10px;
      border-bottom: 1px solid #ccc;
      list-style-type: none;
      cursor: pointer;
    }
  }
</style>