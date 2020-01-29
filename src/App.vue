<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''">
    <main>
      <div class="container">
        <div class="header">
          <img src="./assets/logo.png" alt="logo">
          <h1>Weather App</h1>
        </div>
        <div class="search-box">
          <input 
            type="text" 
            class="search-bar" 
            placeholder="Search city or country..." 
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
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'app',
  data () {
    return {
      api_key: '01976620939682e4bc518d4ec4f3177c',
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

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: sans-serif;
  background-color: #313131;
}

#app {
  background-image: url('./assets/cold.jpg');
  background-size: cover;
  width: 100%;
  max-width: 768px;
  margin: 0 auto;
  transition: .4s;
}
#app.warm {
  background-image: url('./assets/warm.jpg');
}

main {
  min-height: 100vh;
  margin: 0 auto;
  padding: 20px;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));

  .container {
    margin: 5vh 0;
  }

  .header {
    text-align: center;
    color: #fff;
    margin: 30px 0;
    img {
      margin-bottom: 10px;
    }
    h1 {
      text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
    }
  }

  .search-box {
    width: 90%;
    display: block;
    margin: 0 auto 30px auto;

    .search-bar {
      display: block;
      width: 100%;
      padding: 15px;
      color: #212529;
      font-size: 20px;
      text-transform: capitalize;
      text-align: center;
      appearance: none;
      outline: none;
      background: none;
      border: none;

      box-shadow: 0 0 8px rgba(0, 0, 0, 0.25);
      background-color: rgba(255, 255, 255, 0.8);
      border-radius: 1rem;
      transition: .4s;

      &:focus {
        box-shadow: 0 0 16px rgba(0, 0, 0, 0.25);
        background-color: rgba(255, 255, 255, 1);
        border-radius: .25rem;
      }
    }
  }
  .weather-wrap {
    .location-box {
      text-align: center;
      .location {
        color: #fff;
        font-size: 32px;
        font-weight: 500;
        text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
      }
      .date {
        color: #fff;
        font-size: 20px;
        font-weight: 300;
        text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
      }
    }
    .weather-box {
      text-align: center;
      .temp {
        display: inline-block;
        padding: 10px 25px;
        color: #fff;
        font-size: 102px;
        font-weight: 900;
        text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
        background-color: rgba(255, 255, 255, 0.25);
        border-radius: 16px;
        margin: 30px 0;
      }
      .weather {
        color: #fff;
        font-size: 48px;
        font-weight: 700;
        text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
      }
    }
  }
}
</style>
