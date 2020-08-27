<template>
  <div id="app" :class="typeof weather.main != 'undefined' ? weather.weather[0].main : ''">
    <main>
      <div class="searchBox">
        <input type="text" class="searchBar" placeholder="Search" v-model="query" @keyup.enter="fetchWeather" />
      </div>

      <div class="weather" v-if="typeof weather.main != 'undefined'">
        <div class="locationBox">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date">{{ dateBuilder() }}</div>
        </div>

        <div class="weatherBox">
          <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
          <div class="status">{{ weather.weather[0].main }}</div>
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
      apiKey: '136676396935f57b623ea3782fab43f1',
      url: 'https://api.openweathermap.org/data/2.5/weather',
      query: '',
      weather: {}
    }
  },
  methods: {
    fetchWeather() {
        fetch(`${this.url}?q=${this.query}&units=metric&appid=${this.apiKey}`)
        .then(res => {
          return res.json();
        })
        .then(this.setResults);
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
}

#app {
  background-image: url('./assets/Clear.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

#app.Clouds {
  background-image: url('./assets/Clouds.jpg');
}

#app.Clear {
  background-image: url('./assets/Clear.jpg');
}

#app.Clouds {
  background-image: url('./assets/Clouds.jpg');
}

#app.Drizzle {
  background-image: url('./assets/Drizzle.jpg');
}

#app.Rain {
  background-image: url('./assets/Rain.jpg');
}

#app.Snow {
  background-image: url('./assets/Snow.jpg');
}

#app.Thunderstorm {
  background-image: url('./assets/Thunderstorm.jpg');
}

main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0 ,0 ,0 ,0.75));
}

.searchBox {
  width: 100%;
  margin-bottom: 30px;
  text-align: center;
}

.searchBox .searchBar {
  display: box;
  width: 50%;
  padding: 20px;
  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 0px 10px 0px 10px;
  transition: 0.4s;
}

.searchBox .searchBar:focus {
  box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.9);
  border-radius: 10px 0px 10px 0px;
}

.locationBox .location {
  color: #FFF;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px, 3px, rgba(0, 0, 0, 0.25);
}

.locationBox .date {
  color: #FFF;
  font-size: 20px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px, 3px, rgba(0, 0, 0, 0.25);
}

.weatherBox {
  text-align: center;
}

.weatherBox {
  text-align: center;
}

.weatherBox .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #FFF;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 10px;
  margin: 30px 0px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weatherBox .status {
  color: #FFF;
  font-size: 48px;
  font-weight: 700;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>