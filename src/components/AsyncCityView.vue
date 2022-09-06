<template>
  
</template>

<script lang="ts">
import axios from "axios";
import { defineComponent } from "vue";
import { useRoute } from "vue-router";

export default defineComponent({
    data() {
        return{
            route: useRoute()
        }
    },
    async mounted () {
        const getWeatherData = async () => {
            try {
                const weatherData = await axios.get(`https://api.openweathermap.org/data/3.0/onecall?lat=${this.route.query.lat}&lon=${this.route.query.lng}&exclude={part}&appid=5fbdce717539e1f16120b7e52b90e251&units=imperial`)

                //calculate current date and time
                const currentDate = new Date().getTimezoneOffset() * 60 * 1000;
                const utc = weatherData.data.current.dt * 1000 + currentDate;
                weatherData.data.currentTime = utc + 1000 * weatherData.data.timezone_offset;

                //calculate hourly weather offset
                weatherData.data.hourly.forEach((hour: any) => {
                    const utc = hour.dt * 1000 + currentDate;
                    hour.currentTime = utc + 1000 * weatherData.data.timezone_offset;
                });

                return weatherData.data
            } catch (error) {
                
            }
        }
        const weatherData = await getWeatherData();
        console.log(weatherData)
    }
})
</script>

<style>

</style>