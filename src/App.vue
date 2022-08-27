<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? warm=true && 'warm' : warm=false && 'cold' ">
<main>
      <div class="search-box">
        <input 
        type="text" 
        class="search-bar" 
        placeholder="Search..."
        v-model = "query"
        @keypress = "fetchWeather"
        />
      </div>
      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location"> {{ weather.name }}, {{ weather.sys.country}}</div>
          <div class="date">{{ dateBuilder() }}</div>
        </div>

        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp) }} °C</div>
          <div class ="feeling" v-if = "warm" > Hot in there 🥵 </div>
          <div class ="feeling" v-else > It's pretty cold, what you think? 🥶 </div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      api_key: 'f58f58b6f41dd93092842f42a0750665',
      url_base:'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {},
      warm: false,
    }
  },

  methods: {
    fetchWeather (e) {
      if (e.key == "Enter") {
      fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`).then(res => {
        return res.json();
      }).then(this.setResults);
    }

  },
  setResults (results) {
    this.weather = results;
  },

  dateBuilder () {
    let d = new Date();
    let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
    let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"];

    let day = days[d.getDay()];
    let date = d.getDate();
    let month = months[d.getMonth()];
    let year = d.getFullYear();

    return `${day} ${date} ${month} ${year}`
  }
}
}
</script>

<style lang="scss" >
@import 'style.scss';

</style>
