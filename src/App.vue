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
        <div>
          <div class="temperature">
            {{ weather.results.temp }}°
            <div class="type-of-day">
              {{ weather.results.description }}
            </div>
          </div>
          <div class="square-container">
            <div>
              <div class="title">
                <span class="material-symbols-sharp">
                  device_thermostat
                </span>
                Máx / Min
              </div>
              <div>
                {{ weather.results.forecast[0].max }}° / {{ weather.results.forecast[0].min }}°
              </div>
            </div>
            <div>
              <div class="title">
                <span class="material-symbols-sharp">
                  water_drop
                </span>
                Precipitação
              </div>
              <div>
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
              <div>
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
              <div class="wind">
                <div>
                  {{ weather.results.wind_cardinal }}
                </div>
                {{ weather.results.wind_speedy }}
              </div>
            </div>
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
                <div>
                  {{ forecast.weekday }}
                </div>
                {{ forecast.date }}
                <div>
                  {{ forecast.max }}° / {{ forecast.min }}°
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="uv-wind-container">
          <div class="uv-index">
            <div class="title">
              <span class="material-symbols-sharp">
                device_thermostat
              </span>
              Índice UV
            </div>
            <!-- {{ weather.daily.uv_index_max[0] }} -->
          </div>
          <div class="wind">
            <div class="title">
              <span class="material-icons">
                wb_twilight
              </span>
              Nascer/Pôr do Sol
            </div>
            <div>
              Nascer do Sol: {{ weather.results.sunrise }}
              Pôr do Sol {{ weather.results.sunset }}
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
  height: 80vh;
  width: 80%;
  border-radius: 25px;
  background-color: #000000be;
  padding: 1vw;
  box-sizing: border-box;
  display: flex;
  gap: 1vw;
}

.left-container {
  height: 100%;
  width: 40%;
  box-sizing: border-box;
  padding: 0.5vh;
  border-radius: 20px;
}

input {
  width: 100%;
  height: 5vh;
  background-color: #424242;
  border: none;
  border-radius: 20px;
  padding-left: 4vw;
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
  left: 1vw;
}

.temperature {
  color: white;
  display: flex;
  font-size: 10vh;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 35vh;
  gap: 1vh;
}

.type-of-day {
  font-size: 3vh;
}

.square-container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 1vw;
  flex-wrap: wrap;
  width: 100%;
}

.square-container>div {
  width: 13vw;
  height: 13vh;
  border-radius: 15px;
  padding: 1vh;
  color: white;
  font-size: 3vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1vh;
  background-color: rgba(0, 0, 0, 0.788);
}

.title {
  color: rgb(74, 74, 124);
  display: flex;
  gap: 1vh;
  align-items: center;
  justify-content: center;
  font-size: 3.5vh;
  font-weight: 700;
}

.wind {
  display: flex;
  flex-direction: column;
  gap: 1vh;
  font-size: 2.5vh;
}

.right-container {
  width: 58%;
  display: flex;
  flex-direction: column;
  gap: 2vh;
  padding: 1vh;
  box-sizing: border-box;
}

.forecast {
  height: 30vh;
  border-radius: 20px;
  padding: 2vh 1vw;
  box-sizing: border-box;
  background-color: rgba(0, 0, 0, 0.788);
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

.uv-index {
  height: 100%;
  width: 48%;
  border-radius: 20px;
  background-color: rgba(0, 0, 0, 0.788);
  padding: 1vh;
  box-sizing: border-box;
  color: white;
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
