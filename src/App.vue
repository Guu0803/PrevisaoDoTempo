<template>
  <div class="window">
    <div class="main-container ">
      <div class="left-container">
        <div class="search-container">
          <span class="material-symbols-sharp location">
            location_on
          </span>
          <input type="search">
        </div>
        <div>
          <div class="temperature" v-if="weather.current">
            {{weather.current.temperature_2m}}°
           
            <!-- {{ currentTemperature }}° -->
            <div class="type-of-day">
              <div>

              </div>
              <div>
                {{ temperatureMax}}° / {{ temperatureMin}}°
              </div>
            </div>
          </div>
          <div class="square-container">
            <div>
              <div class="title">
                <span class="material-symbols-sharp">
                  device_thermostat
                </span>
                Sensação
              </div>
              <div>
                30º
              </div>
              <div class="info-square">
                Humidity is making it feel warmer
              </div>
            </div>
            <div>
              <div class="title">
                <span class="material-symbols-sharp">
                  water_drop
                </span>
                Precipitation
              </div>
              <div>
                2.3'
              </div>
              <div class="info-square">
                2' expected in next 24h
              </div>
            </div>
            <div>
              <div class="title">
                <span class="material-symbols-sharp">
                  humidity_percentage
                </span>
                Humidity
              </div>
              <div>
                82%
              </div>
              <div class="info-square">
                The dew point is 25° right now
              </div>
            </div>
            <div></div>
          </div>
        </div>
      </div>
      <div class="right-container">
        <div class="forecast">
          <div class="title">
            <span class="material-symbols-sharp">
              schedule
            </span>
            Hourly Forecast
          </div>
          <div class="separation"></div>
          <div class="card-container">
            <div class="hour">
              28°
            </div>
          </div>
        </div>
        <div class="forecast">
          <div class="title">
            <span class="material-symbols-sharp">
              calendar_today
            </span>
            10-Day Forecast
          </div>
          <div class="separation"></div>
          <div class="card-container">
            Today
          </div>
        </div>
        <div class="uv-wind-container">
          <div class="uv-index">
            <div class="title">
              <span class="material-symbols-sharp">
                device_thermostat
              </span>
              UV Index
            </div>
            3 Moderate
          </div>
          <div class="wind">
            <div class="title">
              <span class="material-symbols-sharp">
                air
              </span>
              Wind
            </div>
          </div>
        </div>
      </div>
    </div>
    <button v-on:click="search()">
      clique aqui
    </button>
  </div>
</template>
<script>
export default {
  data() {
    return {
      longitude: 0,
      latitude: 0,
      weather: {},
      currentTemperature: 0,
      temperatureMax: 0,
      temperatureMin: 0
    }
  },
  methods: {
    search() {
      const axios = require('axios')
      let url = 'https://maps.googleapis.com/maps/api/geocode/json?address=jacarei&key=AIzaSyApTY3yOsLuqb67qxHom3TJuKqg3K9snWc'
      let config = {}
      axios.get(url, config).then(response => {
        // console.log(response)
        this.longitude = response.data.results[0].geometry.location.lng
        this.latitude = response.data.results[0].geometry.location.lat
        this.forecast()
      }).catch(error => {
        console.log(error)
      })
    },
    forecast() {
      const axios = require('axios')
      let url = 'https://api.open-meteo.com/v1/forecast?latitude=' + this.latitude + '&longitude=' + this.longitude + '&current=temperature_2m,relativehumidity_2m,apparent_temperature,precipitation,rain,weathercode,cloudcover,windspeed_10m,winddirection_10m,windgusts_10m&hourly=temperature_2m,relativehumidity_2m,apparent_temperature,precipitation_probability,windspeed_10m,winddirection_10m,uv_index&daily=weathercode,temperature_2m_max,temperature_2m_min,apparent_temperature_max,apparent_temperature_min,sunrise,sunset&timezone=America%2FSao_Paulo'
      let config = {}
      axios.get(url, config).then(response => {
        this.weather = response.data
        console.log(this.weather)
        // console.log(this.weather.current.temperature_2m)
        this.currentTemperature = response.data.current.temperature_2m
        // this.temperatureMax = response.data.daily.temperature_2m_max[0]
        // this.temperatureMin = response.data.daily.temperature_2m_min[0]
        // localStorage.setItem('weather', JSON.stringify(this.weather))
      }).catch(error => {
        console.log(error)
      })
    }
  },
  beforeCreated(){
    console.Console('estou funcionando')
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
  padding: 3vw;
  box-sizing: border-box;
  background-image: url('@/assets/weather-wallpaper.jpg');
  background-size: cover;
  overflow: hidden;
}

.main-container {
  height: 88vh;
  width: 100%;
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
  border-radius: 20px;
  background-color: #424242;
  border: none;
}

.search-container {
  position: relative;
  display: flex;
  align-items: center;
}

.location {
  position: absolute;
  left: 1vw;
  color: white;
}

.temperature {
  color: white;
  display: flex;
  font-size: 4em;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 40vh;
  gap: 1vh;
}

.type-of-day {
  font-size: 0.5em;
}

.info-day {
  font-size: 0.15em;
  text-align: center;
}

.square-container {
  margin: 0 2vw;
  display: flex;
  gap: 1vw;
  flex-wrap: wrap;
}

.square-container>div {
  width: 15vw;
  height: 15vh;
  border-radius: 15px;
  padding: 1vh 0.3vh;
  color: white;
  font-size: 2em;
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
  font-size: 3vh;
  font-weight: 500;
}

.info-square {
  font-size: 0.3em;
  text-align: center;
}

.right-container {
  width: 58%;
  display: flex;
  flex-direction: column;
  gap: 1vh;
  padding: 1vh;
  box-sizing: border-box;
}

.forecast {
  height: 27vh;
  border-radius: 20px;
  padding: 1vh 1vw;
  box-sizing: border-box;
  background-color: rgba(0, 0, 0, 0.788);

}

.uv-wind-container {
  height: 27vh;
  display: flex;
  justify-content: space-between;

}

.separation {
  border-bottom: 1px solid rgba(59, 58, 58, 0.76);
  width: 100%;
  margin-top: 1vh;
}

.card-container {
  height: 18vh;
  overflow-x: scroll;
  display: flex;
  color: white;
}

.uv-index,
.wind {
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
