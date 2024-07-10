<template>
  <div class="about-container">
    <div class="about">
      <h1 class="about-today">Weather-Today program</h1>
      <p>
        Weather App is a web application that allows you to get weather
        information anywhere just by typing the name of the city. The
        application is easy to use, available for quick weather updates.
      </p>
      <p>
        The app uses an API to retrieve weather data. Shows fluctuations in air
        temperature during the day. Also provides humidity and wind data.
      </p>
      <p>
        The app is built using web technologies such as Vue.js, HTML, CSS, and
        JavaScript, making it a light and fast app.
      </p>
      <p>
        The Weather-Today program is simple and intuitive. This will help you to
        know the weather forecast for the day.
      </p>
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  setup() {
    return {};
  },
});
</script>

<style>
.about-container {
  background-image: url("../assets/about1.jpg");
  background-size: cover;
  background-position: bottom;
  height: 100vh;
  padding-top: 26px;
}
.about {
  width: 48%;
  min-width: 340px;
  display: flex;
  flex-direction: column;
  margin: 0px auto;
  padding-bottom: 20px;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  border-radius: 20px;
  transition: 0.4s;
}
.about-today {
  font-size: 26px;
  font-weight: 500;
  text-align: center;
  padding: 20px;
}
.about p {
  /* color: #fff; */
  font-size: 20px;
  font-weight: 500;
  padding: 4px 26px;
  text-align: justify;
}
</style>
