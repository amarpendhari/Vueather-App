<template>
  <div v-if="loading" class="lds-spinner">
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
  </div>

  <button v-else class @click="daily(day)">
    <p class="today">{{ day.dt | moment }}</p>
    <div class="d-flex-aic-jcc">
      <span class="max">{{ Math.round(day.temp.max) }}&deg;</span>
      <span class="min">{{ Math.round(day.temp.min) }}&deg;</span>
    </div>

    <img v-if="day.weather[0].main == 'Rain'" src="../assets/images/rain.png" />
    <img v-else-if="day.weather[0].main == 'Clouds'" src="../assets/images/cloud.png" />
    <img v-else-if="day.weather[0].main == 'Haze'" src="../assets/images/sun.png" />
    <img v-else src="../assets/images/weather.png" />
    <p class="weather">{{ day.weather[0].main }}</p>
  </button>
</template>

<script>
import moment from "moment-timezone";
export default {
  name: "Day2Day",
  props: ["day", "loading", "daily"],
  data() {
    return {};
  },
  filters: {
    moment: function(date) {
      return moment(date * 1000)
        .format("dddd")
        .slice(0, 3);
    }
  },
  methods: {}
};
</script>

<style>
</style>
