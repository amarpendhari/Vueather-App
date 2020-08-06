<template>
  <div class="current">
    <div class="d-flex-aic">
      <p class="degrees">
        <b
          style="font-family: sans-serif"
          v-if="current.temp.day"
        >{{ Math.round(current.temp.day)}}&deg;C</b>
        <b style="font-family: sans-serif" v-else>{{ Math.ceil(current.temp)}}&deg;C</b>
      </p>
      <div class="cw">
        <img
          class="mt-25"
          :src="(`https://openweathermap.org/img/wn/${current.weather[0].icon}@2x.png`)"
          :alt="current.weather[0].main"
        />
        <span class="mt-25">({{current.weather[0].main}})</span>
      </div>
    </div>
    <div class="Chart">
      <Chart></Chart>
    </div>
    <div class="d-flex p-10">
      <div class="HP">
        <span class="max">
          <b>Pressure</b>
        </span>
        <p>{{ current.pressure }} hpa</p>
      </div>
      <div class="HP">
        <span class="max">
          <b>Humidity</b>
        </span>
        <p>{{ current.humidity }} %</p>
      </div>
    </div>
    <div class="time">
      <div>
        <span class="max">Sunrise</span>
        <br />
        <span class="min">{{ current.sunrise | moment}}</span>
      </div>
      <div>
        <span class="max">Sunset</span>
        <br />
        <span class="min">{{ current.sunset | moment}}</span>
      </div>
    </div>
    <div class="movingsun">
      <img src="../assets/images/movingSun.png" />
    </div>
  </div>
</template>

<script>
import moment from "moment-timezone";
import Chart from "./Chart";
export default {
  name: "Current",
  components: {
    Chart
  },
  props: ["current"],
  filters: {
    moment: function(date) {
      return moment(date * 1000).format("HH:mma z");
    }
  },
  methods: {}
};
</script>

<style>
</style>