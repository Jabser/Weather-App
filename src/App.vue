<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input 
          type="text" 
          class="search-bar" 
          placeholder="Search..." 
        />
      </div>
      <div class="weather-wrap">
        <div class="location-box">
          <div class="location">Aarhus, DK</div>
          <div class="date">Monday 20 January 2020</div>
        </div>
        <div class="weather-box">
          <div class="temp">9°c</div>
          <div class="weather">Rain</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'app'
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'montserrat', sans-serif;
}

#app {
  background-image: url('./assets/cold-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: .4s;
}

main {
  min-height: 100vh;
  padding: 20px;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.25), rgba(0, 0, 0, 0.75));

  .search-box {
    width: 100%;
    margin-bottom: 30px;

    .search-bar {
      display: block;
      width: 100%;
      padding: 15px;

      color: #313131;
      font-size: 20px;

      appearance: none;
      border: none;
      outline: none;
      background: none;

      box-shadow: 0 0 8px rgba(0, 0, 0, 0.25);
      background-color: rgba(255, 255, 255, 0.5);
      border-radius: 0 16px 0 16px;
      transition: .4s;

      &:focus {
        box-shadow: 0 0 16px rgba(0, 0, 0, 0.25);
        background-color: rgba(255, 255, 255, 0.75);
        border-radius: 16px 0 16px 0;
      }
    }
  }
  .weather-wrap {
    .location-box {
      .location {
        color: #fff;
        font-size: 32px;
        font-weight: 500;
        text-align: center;
        text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
      }
      .date {
        color: #fff;
        font-size: 20px;
        font-weight: 300;
        font-style: italic;
        text-align: center;
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

        text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
        background-color: rgba(255, 255, 255, 0.25);
        border-radius: 16px;
        margin: 30px 0;

        box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
      }
      .weather {
        color: #fff;
        font-size: 48px;
        font-weight: 700;
        font-style: italic;
        text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
      }
    }
  }
}
</style>
