<template>
  <div
    class="weather"
    :class="
      typeof weather?.main != 'undefined' && weather?.main.temp - 273.15 > 16
        ? 'warm'
        : ''
    "
  >
    <main class="main">
      <div id="main-city">
        <div class="search-box">
          <input
            id="city"
            type="text"
            class="search-bar"
            placeholder="Search..."
            v-model="city"
            @keyup.enter="fetchData"
          />
          <button id="form-btn" @click="fetchData" type="submit">add</button>

          <!-- <div class="error">
            <p>{{ error }}</p>
          </div> -->
        </div>
      </div>

      <div v-if="weather?.main" class="weather-container">
        <div class="weather-wrap">
          <div class="location-box">
            <div class="location">
              {{ weather?.name }}, {{ weather?.sys.country }}
              <div class="date">{{ dateBuilder() }}</div>
            </div>
            <div id="block-bottom">
              <div class="group-time">
                <p id="time">{{ weather?.time }}</p>
              </div>
            </div>
          </div>

          <div class="weather-box">
            <div class="temp">
              {{ Math.round(weather?.main.temp - 273.15).toFixed(1) }}°c
              <div class="quality">
                <div class="weather-now-temp-minmax">
                  <span class="min-max">
                    Low:
                    {{ Math.round(weather.main.temp_min - 273.15).toFixed() }}°C
                  </span>
                  <span class="min-max">
                    High:{{
                      Math.round(weather.main.temp_max - 273.15).toFixed()
                    }}°C
                  </span>
                </div>
                <div class="humidity-wind">
                  <span class="humidity"
                    >Humidity: {{ weather.main.humidity }}%</span
                  >
                  <span class="humidity"
                    >Wind: {{ Math.round(weather.wind.speed) }} m/s</span
                  >
                </div>
              </div>
              <div class="weather">{{ weather?.weather[0].main }}</div>
            </div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import { defineComponent, computed, ref } from "vue";
import { useWeatherStore } from "@/store";

export default defineComponent({
  setup() {
    const city = ref("");

    const store = useWeatherStore();
    const weather = computed(() => store.weatherData);
    function fetchData() {
      store.getWeatherData(city.value);
    }

    function dateBuilder() {
      let d = new Date();

      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      let time = d.getHours() + ":" + d.getMinutes() + ":" + d.getSeconds();
      return `${day} ${date} ${month} ${year} ${time} `;
    }

    return {
      city,
      weather,
      fetchData,
      dateBuilder,
    };
  },
});
</script>
<style scoped>
.weather-container {
  margin-bottom: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.weather {
  background-image: url("../assets/about3.jpg");
  background-size: cover;
  background-position: center;
  transition: 0.4s;
}
.weather.warm {
  background-image: url("../assets/warm-bg2.jpg");
  background-size: cover;
  background-position:  top;
  transition: 0.4s;
}
.main {
  display: flex;
  flex-direction: column;
  align-items: center;
}
#main-city {
  display: flex;
  justify-content: space-between;
  width: 60%;
  min-width: 300px;
  margin: 0 auto;
}
.search-box {
  width: 100%;
  margin-bottom: 30px;
  display: flex;
  gap: 10px;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 6px 10px;
  color: #313131;
  font-size: 18px;
  appearance: none;
  border: none;
  outline: none;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 10px;
  transition: 0.4s;
  cursor: pointer;
}
#form-btn {
  width: 26%;
  font-size: 16px;
  border-radius: 10px;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  color: #000;
  font-weight: 400;
  border: 1px transparent;
  transition: background-color 0.3s ease-in-out;
  cursor: pointer;
}

#block-bottom {
  display: flex;
}
.group-time {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: flex-end;
}
#current-time {
  margin: 0 0 7px 10px;
  font-size: 32px;
}
.location-box .location {
  display: flex;
  flex-direction: column;
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.5);
  gap: 30px;
}
.location-box .date {
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}
.weather-box {
  text-align: center;
}
.weather-box .temp {
  display: inline-block;
  padding: 20px 45px;
  color: #fff;
  font-size: 82px;
  font-weight: 700;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 20px 0;
}
.min-max {
  display: flex;
  padding: 0 0 20px 0;
}
.humidity {
  padding: 0 20px;
}
.weather-box .weather {
  background: none;
  color: #fff;
  font-size: 38px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.quality {
  display: flex;
  justify-content: center;
  align-items: center;
  display: flex;
  flex-direction: column;
  gap: 12px;
  color: #fff;
  font-size: 18px;
  font-weight: 500;
  font-style: italic;
  margin-top: 12px;
}
</style>
