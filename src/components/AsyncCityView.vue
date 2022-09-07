<template>
    <div>
      <div v-if="route.query.preview === 'true'">
         <span class="preview">You are viewing this in preview mode</span>
      </div>
    </div>
 
    <div>
        <h1>{{ route.params.city }}</h1>
        <p class="" v-if="weatherData">
          {{ new Date(weatherData.currentTime).toLocaleDateString(
              "en-US",
              {
                  weekday: "short",
                  month: "long",
                  day: "2-digit",
              }
          ) 
          }}
          {{ 
          new Date(weatherData.currentTime).toLocaleTimeString(
              "en-US",
              {
                  hour: "2-digit",
                  minute: "2-digit",
              }
          ) 
          }}
        </p>
        <!-- <span>{{ weatherData.current.feels_like }}</span> -->
    </div>
 </template>


<script lang="ts">
import axios from "axios";
import { defineComponent } from "vue";
import { useRoute } from "vue-router";

export default defineComponent({
    data() {
        return{
            route: useRoute(),
            weatherData: {} as any,
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

                return weatherData.data;       
            } catch (error) {
                
            }
        }
        this.weatherData = await getWeatherData()
        console.log(this.weatherData)
    }
})
</script>

<style>

</style>