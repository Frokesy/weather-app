<script lang="ts">
import { defineComponent } from "vue";
import AsyncCityView from "../components/AsyncCityView.vue";
import axios from "axios";
import { useRoute } from "vue-router";
    
    export default defineComponent({
    components: { AsyncCityView },
    data() {
        return {
            route: useRoute(),        
        }
    }
})
</script>

<template>
  <div>
    <Suspense>
        <AsyncCityView />
        <template #fallback>
            loading...
        </template>
    </Suspense>
  </div>
</template>

<style>

</style>