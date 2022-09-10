<template>
  <div v-if="weatherData">
    <div>
      <div class="preview" v-if="route.query.preview === 'true'">
         <span>You are currently viewing this in preview mode, an update on this will be provided later</span>
      </div>
    </div>
 
    <div class="city-view">
        <h1>{{ route.params.city }}</h1>
        <img :src="`https://openweathermap.org/img/wn/${weatherData?.current.weather[0].icon}@2x.png`" alt="weather-icon">
        <p class="weather-description">{{ weatherData?.current.weather[0].description }}</p>
        <span class="temp">{{ weatherData?.current.temp }}&deg;</span>
        <p class="rest">Feels like {{ weatherData?.current.feels_like }}&deg;</p>
        <p class="rest">
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
    </div>
    <div class="horizontal-rule"></div>
    <div>
        <h2>Hourly Weather</h2>
        <div class="hourly">
            <div v-for="hour in weatherData?.hourly" :key="hour.dt">
                <span>{{ new Date(hour.dt * 1000).toLocaleTimeString("en-US", { hour: "2-digit", minute: "2-digit" }) }}</span>
                <img :src="`https://openweathermap.org/img/wn/${hour?.weather[0].icon}@2x.png`" alt="weather-icon">
                <p>{{ hour.temp }}&deg;</p>
            </div>  
        </div>
    </div>
    
    <div>
        <h2>Weekly Weather</h2>
        <div class="weekly">
            <div class="weekly-data" v-for="day in weatherData?.daily" :key="day.dt">
                <p class="weekday">{{ new Date(day.dt * 1000).toLocaleDateString("en-US", { weekday: "long" }) }}</p>
                <img :src="`https://openweathermap.org/img/wn/${day?.weather[0].icon}@2x.png`" alt="weather-icon" />
                <div class="min-max">
                    <p>H: {{ day.temp.max }}&deg;</p>
                    <p>L: {{ day.temp.min }}&deg;</p>
                </div>
            </div>
        </div>   
    </div>
  </div>
  <div v-else>
    <CityViewSkeleton />
  </div>
 </template>


<script lang="ts">
import axios from "axios";
import { defineComponent } from "vue";
import { useRoute } from "vue-router";
import CityViewSkeleton from "./CityViewSkeleton.vue";

export default defineComponent({
    data() {
        return {
            route: useRoute(),
            weatherData: null as any,
        };
    },
    async mounted() {
        const getWeatherData = async () => {
            try {
                const weatherData = await axios.get(`https://api.openweathermap.org/data/3.0/onecall?lat=${this.route.query.lat}&lon=${this.route.query.lng}&exclude={part}&appid=5fbdce717539e1f16120b7e52b90e251&units=metric`);
                //calculate current date and time
                const currentDate = new Date().getTimezoneOffset() * 60 * 1000;
                const utc = weatherData.data.current.dt * 1000 + currentDate;
                weatherData.data.currentTime = utc + 1000 * weatherData.data.timezone_offset;
                //calculate hourly weather offset
                weatherData.data.hourly.forEach((hour: any) => {
                    const utc = hour.dt * 1000 + currentDate;
                    hour.currentTime = utc + 1000 * weatherData.data.timezone_offset;
                });
                //flicker delay
                await new Promise((resolve) => setTimeout(resolve, 500));
                return weatherData.data;
            }
            catch (error) {
            }
        };
        this.weatherData = await getWeatherData();
    },
    components: { CityViewSkeleton }
})
</script>

<style>
    /* width */
::-webkit-scrollbar {
    width: 5px;
    height: 8px;
  }  
  /* Track */
  ::-webkit-scrollbar-track {
    box-shadow: inset 0 0 3px grey;
    border-radius: 10px; 
  }
   
  /* Handle */
  ::-webkit-scrollbar-thumb {
    background: #888; 
    border-radius: 10px;
  }
  
  /* Handle on hover */
  ::-webkit-scrollbar-thumb:hover {
    background: #BAC3B8; 
  }
  .hourly {
    display: flex;
    width: 100%;
    overflow-x: scroll;
    margin: 30px auto;
    gap: 3.5rem;
    text-align:center;
  } 
  .hourly p {
    margin-bottom: 40px;
    font-family: 'Rampart One', cursive;

  }
  .weekly {
    display: flex;
    justify-content: space-between;
    flex-direction: column;
    max-width: screen;
    width: 100%;
  }
  .weekly-data {
    display: flex;
    justify-content: space-evenly;
    margin: 0 auto;
    text-align: center;
    margin-bottom: 5px;
    width: 110%;
  }
  .min-max {
    font-family: 'Rampart One', cursive;
  }
  .weekly img {
    width: 60px;
    height: 60px;
  }
  .weekday {
    font-size: 1.2rem;
    font-weight: bold;
    }
  .preview {
    background: #222222;
    color: #BAC3B8;
    width: 100%;
    padding: 10px;
    text-align: center;
    margin-top: 15px;
  } 
  .city-view {
    align-items: center;
    text-align: center;
  }
  .city-view h1 {
    font-size: 3.5rem;
    margin-top: 20px;
    margin-bottom: 0;
    font-family: 'Rampart One', cursive;
    color: #ccc
  }
  .city-view img {
    width: 10em;
  }
  .city-view .weather-description {
    font-size: 1.5rem;
    margin-top: 0;
    margin-bottom: 0;
    color: #ccc
  }
  .temp {
    font-size: 3rem;
    margin-top: 0;
    margin-bottom: 0;
    font-family: 'Rampart One', cursive;
    color: #ccc
  }
  .rest {
    font-size: 1.2rem;
    color: #ccc
  }
  h2 {
    font-size: 2rem;
    margin-bottom: 20px;
    font-family: 'Rampart One', cursive;
    color: #ccc
  }
    .horizontal-rule {
        border-bottom: 1px solid #ccc;
        margin-top: 20px;
        margin-bottom: 20px;
    }
  @media screen and (max-width: 768px) {
    .weekly-data {
        display: flex;
        justify-content: space-between;
        margin: 0 auto;
        text-align: center;
        margin-bottom: 5px;
        font-size: 11px;
        width: 100%;
      }
      .weekly {
        display: flex;
        justify-content: space-between;
        flex-direction: column;
        max-width: screen;
        width: 100%;
      }
      .min-max {
        font-family: 'Rampart One', cursive;
      }
      .weekly img {
        width: 60px;
        height: 60px;
      }
      .weekday {
        font-size: 1.2rem;
        font-weight: bold;
        }
      .preview {
        background: #222222;
        color: #BAC3B8;
        width: 100%;
        font-size: 10px;
        padding: 10px;
        text-align: center;
        margin-top: 15px;
      } 
      .city-view {
        align-items: center;
        text-align: center;
      }
      .city-view h1 {
        font-size: 2.8rem;
        margin-top: 20px;
        margin-bottom: 0;
        font-family: 'Rampart One', cursive;
        color: #ccc
      }
      .city-view img {
        width: 10em;
      }
      .city-view .weather-description {
        font-size: 1.2rem;
        margin-top: 0;
        margin-bottom: 0;
        color: #ccc
      }
      .temp {
        font-size: 2.8rem;
        margin-top: 0;
        margin-bottom: 0;
        font-family: 'Rampart One', cursive;
        color: #ccc
      }
      .rest {
        font-size: 1rem;
        color: #ccc
      }
      h2 {
        font-size: 1.7rem;
        margin-bottom: 20px;
        font-family: 'Rampart One', cursive;
        color: #ccc
      }
      .hourly {
        display: flex;
        width: 100%;
        overflow-x: scroll;
        margin: 30px auto;
        gap: 3rem;
        font-size: 11px;
        text-align:center;
      } 
      .hourly p {
        margin-bottom: 40px;
        font-family: 'Rampart One', cursive;
      } 
      }
</style>