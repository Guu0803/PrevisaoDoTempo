<template>
  <div class="window">
    <div class="main-container">
      <div class="left-container">
        <div class="search-container">
          <span class="material-symbols-sharp location">
            location_on
          </span>
          <input type="search" placeholder="Inserir Local" v-model="city" v-on:keyup.enter="search()">
        </div>
        <div class="temperature-container">
          <div class="temperature">
            {{ weather.results.temp }}°
            <img
              :src="'https://assets.hgbrasil.com/weather/icons/conditions/' + this.weather.results.condition_slug + '.svg'"
              class="icon-weather">
          </div>
          <div class="type-of-day">
            {{ weather.results.description }}
          </div>
        </div>
        <div class="local-container">
          <div class="local">
            <span class="material-symbols-sharp icon-local">
              location_on
            </span>
            <div class="city">
              {{ weather.results.city }}
            </div>
          </div>
          <div class="date">
            {{ weather.results.date }}
          </div>
        </div>
      </div>
      <div class="right-container">
        <div class="forecast">
          <div class="title">
            <span class="material-symbols-sharp">
              calendar_today
            </span>
            Previsão para 10 dias
          </div>
          <div class="separation"></div>
          <div class="card-container">
            <div v-for="forecast in weather.results.forecast" :key="forecast">
              <div class="card">
                <div class="forecast-weekday">
                  {{ forecast.weekday }}
                </div>
                <div class="forecast-date">
                  {{ forecast.date }}
                </div>
                <div>
                  {{ forecast.max }}° - {{ forecast.min }}°
                </div>
                <img :src="'https://assets.hgbrasil.com/weather/icons/conditions/' + forecast.condition + '.svg'"
                  class="icon-forecast">
              </div>
            </div>
          </div>
        </div>
        <div class="other-data">
          <div>
            <div class="title">
              <span class="material-symbols-sharp">
                device_thermostat
              </span>
              Máx / Min
            </div>
            <div class="separation"></div>
            <div class="data">
              {{ weather.results.forecast[0].max }}° - {{ weather.results.forecast[0].min }}°
            </div>
          </div>
          <div>
            <div class="title">
              <span class="material-symbols-sharp">
                water_drop
              </span>
              Precipitação
            </div>
            <div class="separation"></div>
            <div class="data">
              {{ weather.results.forecast[0].rain_probability }} %
            </div>
          </div>
          <div>
            <div class="title">
              <span class="material-symbols-sharp">
                humidity_percentage
              </span>
              Umidade
            </div>
            <div class="separation"></div>
            <div class="data">
              {{ weather.results.humidity }} %
            </div>
          </div>
          <div>
            <div class="title">
              <span class="material-symbols-sharp">
                air
              </span>
              Vento
            </div>
            <div class="separation"></div>
            <div class="data">
              <div>
                {{ weather.results.wind_cardinal }}
                <span class="material-symbols-sharp">
                  explore
                </span>
              </div>
              <div>
                {{ weather.results.wind_speedy }}
                <span class="material-icons">
                  speed
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      city: '',
      weather: {},
      linkConditionIcon: ''
    }
  },
  methods: {
    search() {
      const axios = require('axios')
      let url = 'https://api.hgbrasil.com/weather?format=json-cors&key=b4c4e12d&city_name=' + this.city
      let config = {}
      axios.get(url, config).then(response => {
        this.weather = response.data
        localStorage.setItem('weather', JSON.stringify(this.weather))
      }).catch(error => {
        console.log(error)
      })
    }
  },
  created() {
    let weather = localStorage.getItem('weather')
    weather = JSON.parse(weather)
    if (weather) {
      this.weather = weather
    }
  }
}
</script>
<style>
body {
  margin: 0;
  font-family: 'Montserrat', sans-serif;
}

.window {
  max-width: 100vw;
  height: 100vh;
  box-sizing: border-box;
  background-image: url('@/assets/weather-wallpaper.jpg');
  background-size: cover;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}

.main-container {
  height: 75vh;
  width: 50%;
  border-radius: 25px;
  background-color: #ffffff10;
  backdrop-filter: blur(5px);
  padding: 4vh 1vw;
  box-sizing: border-box;
  display: flex;
  gap: 1vw;
}

.left-container {
  height: 100%;
  width: 40%;
  box-sizing: border-box;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

input {
  width: 100%;
  height: 5vh;
  background-color: rgba(0, 0, 0, 0.788);
  border: none;
  border-radius: 20px;
  padding-left: 4vw;
  color: white;
}

::placeholder {
  color: #807e7e;
  font-size: 2.2vh;
}

.search-container {
  position: relative;
  display: flex;
  align-items: center;
}

.location {
  color: white;
  position: absolute;
  font-size: 3vh;
  left: 1vw;
}

.temperature-container {
  color: white;
  font-size: 7vh;
  height: 15vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1vh;
}

.temperature {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1vh;
}

.icon-weather {
  height: 8vh;
}

.type-of-day {
  font-size: 3vh;
  color: white;
}
.local-container {
  margin:0 0 2vh 1vw;
}
.local {
  font-size: 2.5vh;
  align-items: center;
  display: flex;
  gap: 1vh;
  color: #b9b9b9;
}

.date {
  font-size: 1.7vh;
  color: #b9b9b9;
  margin: 0.5vh 0  0 1.5vw ;
}

.icon-local {
  font-size: 2vh;
}

.right-container {
  width: 58%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 2vh;
  box-sizing: border-box;
}

.forecast {
  height: 30vh;
  border-radius: 20px;
  padding: 2vh 1vw;
  box-sizing: border-box;
  background-color: rgba(0, 0, 0, 0.788);
}

.other-data {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1vw;
  flex-wrap: wrap;
  width: 100%;
}

.other-data>div {
  width: 12.4vw;
  height: 13vh;
  border-radius: 15px;
  padding: 1.5vh 1vh;
  color: white;
  font-size: 3vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: rgba(0, 0, 0, 0.788);
}

.title {
  color: rgb(74, 74, 124);
  display: flex;
  gap: 1vh;
  align-items: center;
  justify-content: center;
  font-size: 2.5vh;
  font-weight: 700;
}

.data {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 0.5vh;
  font-size: 2.7vh;
  height: 10vh;

}

.data>div {
  display: flex;
  align-items: center;
  gap: 1vh;
}

.uv-wind-container {
  height: 30vh;
  display: flex;
  justify-content: space-between;
}

.separation {
  border-bottom: 1px solid rgba(59, 58, 58, 0.76);
  width: 100%;
  margin: 1vh 0;
}

.card-container {
  height: 20vh;
  overflow-x: scroll;
  color: white;
}

.card-container {
  display: flex;
  gap: 1vh;
}

.card {
  width: 8vw;
  height: 18vh;
  color: white;
  display: flex;
  gap: 1vh;
  box-sizing: border-box;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  border-radius: 15px;
  cursor: pointer;
}

.card:hover {
  background-color: #292727;
}

.forecast-weekday {
  color: rgb(74, 74, 124);
  font-size: 2vh;
  font-weight: 700;
}

.forecast-date {
  font-size: 2vh;
  color: #747272;
  font-weight: 500;
}

.icon-forecast {
  height: 6vh;
}

.uv-index {
  height: 100%;
  width: 48%;
  border-radius: 20px;
  background-color: rgba(0, 0, 0, 0.788);
  padding: 2vh 1vw;
  box-sizing: border-box;
  color: white;
}

.sunrise-container {
  display: flex;
  flex-direction: column;
  gap: 2vh;
  align-items: center;
  justify-content: center;
  border: 1px solid red;
  height: 15vh;
  margin-top: 2vh;
}

::-webkit-scrollbar {
  height: 1vh;
  width: 1vh;
}

::-webkit-scrollbar-track {
  background-color: transparent;
  border-radius: 5px;
}

::-webkit-scrollbar-thumb {
  background-color: #424242;
}

::-webkit-scrollbar-thumb:hover {
  background-color: #5a5959;
}
</style>
