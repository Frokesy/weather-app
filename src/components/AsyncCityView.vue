<template>
    <div>
      <div v-if="route.query.preview === 'true'">
         <span class="preview">You are viewing this in preview mode</span>
      </div>
    </div>
 
    <div>
        <h1>{{ route.params.city }}</h1>
        <p class="">
          {{ new Date(weatherData?.currentTime).toLocaleDateString(
              "en-US",
              {
                  weekday: "short",
                  month: "long",
                  day: "2-digit",
              }
          ) 
          }}
          {{ 
          new Date(weatherData?.currentTime).toLocaleTimeString(
              "en-US",
              {
                  hour: "2-digit",
                  minute: "2-digit",
              }
          ) 
          }}
        </p>
        <span>{{ weatherData?.current.temp }}&deg;</span>
        <p>Feels like {{ weatherData?.current.feels_like }}&deg;</p>
        <p>{{ weatherData?.current.weather[0].description }}</p>
        <img :src="`https://openweathermap.org/img/wn/${weatherData?.current.weather[0].icon}@2x.png`" alt="weather-icon">
    </div>
    <hr>
    <div>
        <h2>Hourly Weather</h2>
        <div class="hourly">
            <div v-for="hour in weatherData?.hourly" :key="hour.dt">
                <p>{{ new Date(hour.dt * 1000).toLocaleTimeString("en-US", { hour: "2-digit", minute: "2-digit" }) }}</p>
                <img :src="`https://openweathermap.org/img/wn/${hour?.weather[0].icon}@2x.png`" alt="weather-icon">
                <p>{{ hour.temp }}&deg;</p>
            </div>  
        </div>
    </div>

    <hr>
    <div>
        <h2>Weekly Weather</h2>
        <div class="weekly">
            <div v-for="day in weatherData?.daily" :key="day.dt">
                <p>{{ new Date(day.dt * 1000).toLocaleDateString("en-US", { weekday: "short" }) }}</p>
                <img :src="`https://openweathermap.org/img/wn/${day?.weather[0]. icon}@2x.png`" alt="weather-icon" />
                <p>H: {{ day.temp.max }}&deg;</p>
                <p>L: {{ day.temp.min }}&deg;</p>
            </div>
        </div>   
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
            weatherData: null as any,
        }
    },
    async mounted () {
        const getWeatherData = async () => {
            try {
                const weatherData = await axios.get(`https://api.openweathermap.org/data/3.0/onecall?lat=${this.route.query.lat}&lon=${this.route.query.lng}&exclude={part}&appid=5fbdce717539e1f16120b7e52b90e251&units=metric`)

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
  .hourly {
    display: flex;
    justify-content: space-between;
    flex-direction: row;
    max-width: screen;
    width: 100%;
    overflow-x: scroll;
  } 
  .weekly {
    display: flex;
    justify-content: space-between;
    flex-direction: row;
    max-width: screen;
    width: 100%;
  } 
</style>