<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''">
    <main>
      <div class="header">
        <img src="https://openweathermap.org/themes/openweathermap/assets/img/logo_white_cropped.png" alt="OpenWeather logo">
        <p> Type in CITY name to get real time weather with date from OPENWEATHER api</p>
      </div>
      <div class="search-box">
        <input
            type="text"
            class="search-bar"
            placeholder="Search..."
            v-model="query"
            @keypress="fetchWeather"
        />
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date">{{ dateBuilder() }}</div>
        </div>

        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      api_key: 'cdead8fc7115cdab28d9facf9c11444d',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
  methods: {
    fetchWeather (e) {
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
            .then(res => {
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
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background: #1abc9c;
}
.header {
  padding: 10px;
  color: white;
  text-align: center;
  font-size: 30px;
}
p{
  color : aliceblue;
  font-size: 24px;
  font-weight: 500;
  text-align: center;
  margin-bottom: auto;
  text-shadow: 1px 2px rgba(0,0,0,0.25);
}
.search-box {
  width: 100%;
  margin-bottom: 30px;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 8px rgba(0,0,0,0.25);
  background-color: rgba(255,255,255, 0.5);
  border-radius: 16px;
  transition: 0.4s;
}
.location-box .location {
  color : aliceblue;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 2px rgba(0,0,0,0.25);
}
.location-box .date{
  color : aliceblue;
  font-size: 25px;
  text-align: center;
  text-shadow: 1px 2px rgba(0,0,0,0.25);
}
.weather-box{
  text-align: center;
  padding: 10px 25px;
  color: aliceblue;
  font-size: 40px;
  text-shadow: 1px 2px rgba(0,0,0,0.25);
}

</style>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  background: #1abc9c;
}
.header {
  padding: 10px;
  color: white;
  text-align: center;
  font-size: 30px;
}
p{
  color : aliceblue;
  font-size: 24px;
  font-weight: 500;
  text-align: center;
  margin-bottom: auto;
  text-shadow: 1px 2px rgba(0,0,0,0.25);
}
.search-box {
  width: 100%;
  margin-bottom: 30px;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 8px rgba(0,0,0,0.25);
  background-color: rgba(255,255,255, 0.5);
  border-radius: 16px;
  transition: 0.4s;
}
.location-box .location {
  color : aliceblue;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 2px rgba(0,0,0,0.25);
}
.location-box .date{
  color : aliceblue;
  font-size: 25px;
  text-align: center;
  text-shadow: 1px 2px rgba(0,0,0,0.25);
}
.weather-box{
  text-align: center;
  padding: 10px 25px;
  color: aliceblue;
  font-size: 40px;
  text-shadow: 1px 2px rgba(0,0,0,0.25);
}

</style>
