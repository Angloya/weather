<template>
  <div class="meta">
  <h1 class="name">Weather in {{weatherData.name}}, {{weatherData.country}}</h1>
  <h2>{{weatherData.description}}</h2>
  <img :src='img' class="weatherIcon" :alt='weatherData.description'>
  <h2 class="info"> Air temperature <h1>{{weatherData.temp}}°C</h1></h2>
  <h3 class="info"> Clouds: {{weatherData.clouds}}%</h3>
  <h3 class="info"> humidity: {{weatherData.humidity}}% </h3>
  <h3 class="info"> Wind speed: {{weatherData.wind}} meter/sec</h3>
  <div class="sun">
  <img src="../../assets/sunset.png" alt="">
  <h3>Sunrise: {{weatherData.sunrise}} </h3>
  </div>
  <div class="sun">
  <img src="../../assets/sunset.png" alt="">
  <h3>Sunset: {{weatherData.sunset}}</h3>
  </div>
  </div>
</template>

<script>
export default {
  name: 'Weather3hr',
  data () {
    return {
      weatherData: {},
      weather: {},
      img: ''
    }
  },
  created () {
    this.getWeather()
  },
  methods: {
    getWeather () {
      this.$http.get('https://api.openweathermap.org/data/2.5/weather?id=2643743&units=metric&APPID=35fa185aca1299bde6616c1df7e8a4b8').then(response => {
        this.weatherData = response.body
        this.weatherData.country = response.body.sys.country
        this.weather = response.body.weather
        this.weatherData.main = response.body.main
        this.weatherData.humidity = this.weatherData.main.humidity
        this.weatherData.clouds = response.body.clouds.all
        this.weatherData.temp = Math.round(this.weatherData.main.temp)
        this.img = 'https://openweathermap.org/img/w/' + this.weather[0].icon + '.png'
        this.weatherData.description = this.weather[0].description
        this.weatherData.wind = response.body.wind.speed
        var sunriseTime = new Date(response.body.sys.sunrise * 1000)
        this.weatherData.sunrise = sunriseTime.toLocaleTimeString()
        var sunsetTime = new Date(response.body.sys.sunset * 1000)
        this.weatherData.sunset = sunsetTime.toLocaleTimeString()
      }, response => {
        // error callback
      })
      setTimeout(this.getWeather, 600000)
    }
  }
}
</script>

<style scoped>
.meta {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items:center;
}
.sun{
  display: flex;
  flex-direction: row;
  align-items: center
}
.sun img{
height: 30px;
width: 30px;
}
.weatherIcon {
   height: 80px;
  width: 80px;
  margin: -10px
}
h2{
  margin: 0px;
}
</style>
