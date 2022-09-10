<script lang="ts">
import { defineComponent } from "vue";
import AsyncCityView from "../components/AsyncCityView.vue";
import { useRoute } from "vue-router";
import CityViewSkeleton from "../components/CityViewSkeleton.vue";
    
    export default defineComponent({
    components: { AsyncCityView, CityViewSkeleton },
    data() {
        return {
            route: useRoute(),        
        }
    }
})
</script>

<template>
  <div>
        <AsyncCityView />    
  </div>
</template>

<style>

</style>