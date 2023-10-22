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
          <div class="temperature">
            28°
            <div class="type-of-day">
              Rainy Day
            </div>
            <div class="info-day">
              Today, expect a rainy day with a temperatures reaching a maximum of 28°C. Make sure to grab your umbrella
              and
              raincoat before heading out.
            </div>
          </div>
          <div class="square-container">
            <div>
              <div class="title">
                <span class="material-symbols-sharp">
                  device_thermostat
                </span>
                Fells like
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
  </div>
</template>

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
.separation{
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
.uv-index, .wind {
  height: 100%;
  width: 48%;
  border-radius: 20px;
  background-color: rgba(0, 0, 0, 0.788);
  padding: 1vh;
  box-sizing: border-box;
  color: white;
}
</style>
