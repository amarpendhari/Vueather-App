<template>
  <div id="app">
    <div v-if="loading">
      <AppLoader></AppLoader>
    </div>
    <div v-else>
      <div v-if="alert" class="alert-msg">
        <transition name="fade" appear>
          <div class="alert">
            <p>Sorry. No Location Found !!!</p>
          </div>
        </transition>
      </div>
      <main :class="{ hide: alert}">
        <div class="search-box">
          <form @submit="SubmitForm">
            <input type="text" class="search-bar search" placeholder="Search...." v-model="query" />
            <button class="search">
              <img src="./assets/images/search.png" />
            </button>
          </form>
        </div>
        <div class="horizontal-Scroll">
          <div v-if="weather.daily" class="DDW">
            <div class="daily">
              <div :key="day.dt" v-for="day in weather.daily" class="day">
                <Day2Day :daily="current" :day="day"></Day2Day>
              </div>
            </div>
          </div>
          <div v-else style="margin-top: 10px">
            <ContentLoader></ContentLoader>
          </div>
        </div>

        <div class="Main">
          <div v-if="day">
            <Current :current="day"></Current>
          </div>
          <div v-else class="loader2">
            <ContentLoader></ContentLoader>
          </div>
        </div>
      </main>
    </div>
  </div>
</template>

<script>
//import moment from "moment-timezone";
import Day2Day from "./components/Day2Day";
import Current from "./components/Current";
import AppLoader from "./components/loader/AppLoader";
import ContentLoader from "./components/loader/ContentLoader";
export default {
  name: "App",
  components: {
    Current,
    Day2Day,
    AppLoader,
    ContentLoader
  },
  data() {
    return {
      api_key: process.env.VUE_APP_WEATHER_API_KEY,
      url_base: "https://api.openweathermap.org/data/2.5/",
      loading: false,
      alert: false,
      prev: "",
      query: "",
      lat: "",
      lon: "",
      daily: "",
      day: "",
      weather: {}
    };
  },
  methods: {
    SubmitForm(e) {
      e.preventDefault();
      this.anyLocation();
    },
    Alert() {
      alert("123123");
    },
    current(day) {
      //console.log(day);
      this.day = day;
    },
    fetchLocation() {
      this.loading = true;
      fetch(
        "https://geolocation-db.com/json/${process.env.VUE_APP_LOCATION_API_KEY}"
      )
        .then(res => res.json())
        .then(data => {
          this.lat = data.latitude;
          this.lon = data.longitude;
          this.query = data.city;
          this.prev = this.query;
          this.fetchCW();
        });
    },
    fetchCW() {
      fetch(
        `${this.url_base}onecall?lat=${this.lat}&lon=${this.lon}&units=metric&appid=${process.env.VUE_APP_WEATHER_API_KEY}`
      )
        .then(data => data.json())
        .then(res => {
          this.loading = false;
          this.weather = res;
          this.day = res.current;
          this.prev = this.query;
          //console.log(res);
        })
        .catch(err => {
          console.log(err);
        });
    },
    anyLocation() {
      fetch(
        `${this.url_base}weather?q=${this.query}&units=metric&appid=${process.env.VUE_APP_WEATHER_API_KEY}`
      )
        .then(data => data.json())
        .then(res => {
          this.lat = res.coord.lat;
          this.lon = res.coord.lon;
          //console.log(res);
          this.loading = true;
          this.fetchCW();
        })
        .catch(error => {
          this.alert = true;
          console.log(error);
          setTimeout(
            function() {
              this.alert = false;
              this.query = this.prev;
            }.bind(this),
            2500
          );
        });
    }
  },
  mounted() {
    this.fetchLocation();
  }
};
</script>

<style>
@import "./assets/styles/loader.css";
@import "./assets/styles/style.css";
</style>
