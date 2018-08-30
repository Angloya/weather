<template>
  <div class="meta">
 <h1 id="title">Hourly weather and forecasts in for <em>5</em> days {{weatherData.name}}, {{weatherData.country}} </h1>
 <ul class="weather5day">
     <li v-for="(item,index) in weatherDay" :key="index" class="day">
         <p>{{isDate(item.dt)}}</p>
         <p>{{isTime(item.dt)}} </p>
         <img :src='"http://openweathermap.org/img/w/" + item.weather[0].icon + ".png"' :alt='item.weather[0].description'>
         <h2>{{isRound(item.main.temp)}}°C</h2>
     </li>
 </ul>
 <ul class="weather5">
     <li v-for="(day,index) in weatherData.list" :key="index" class="item">
        <h2>{{isDate(day.dt)}}</h2>
         <h2>{{isTime(day.dt)}}</h2>
         <ul>
        <li>
            <img :src='"http://openweathermap.org/img/w/" + day.weather[0].icon + ".png"' :alt='day.weather[0].description'>
            <h2>{{day.weather[0].description}}</h2>
            <h1>{{isRound(day.main.temp)}}°C</h1>
            <div class='weather5'>
            <h3>clouds: {{day.clouds.all}}%</h3>
            <h3>humidity: {{day.main.humidity}}%</h3>
            <h3>wind: {{day.wind.speed}}, m/s</h3>
            </div>
        </li>
         </ul>

     </li>
 </ul>
  </div>
</template>

<script>
export default {
  name: 'Weather5day',
  data () {
    return {
      weatherData: {},
      weatherDay: {}
    }
  },
  created () {
    this.getWeather()
  },
  methods: {
    getWeather () {
      this.$http.get('http://api.openweathermap.org/data/2.5/forecast?id=524901&units=metric&APPID=35fa185aca1299bde6616c1df7e8a4b8').then(response => {
        this.weatherData = response.body
        this.weatherData.list = response.body.list
        this.weatherData.name = this.weatherData.city.name
        this.weatherData.country = this.weatherData.city.country
        this.weatherDay = response.body.list.slice(0, 5)
      }, response => {
        // error callback
      })
      setTimeout(this.getWeather, 6000000)
    },
    isTime (time) {
      var Hour = new Date(time * 1000)
      return Hour.toLocaleTimeString()
    },
    isDate (date) {
      var Time = new Date(date * 1000)
      return Time.toDateString()
    },
    isRound (temp) {
      return Math.round(temp)
    }
  }
}
</script>

<style scoped>
h1 em {
 font-size: 35px;
 font-style: normal
}
#title{
padding-bottom: 10px;
}
li {
  list-style-type: none
}
.weather5 {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}
.item{
    border: 1px solid black;
    width: 250px;
    height: 250px;
    margin-bottom: 20px;
    background: rgba(255, 255, 255, 0.1);
}
.item:hover {
  background: rgba(255, 255, 255, 0.7);
  -webkit-transform: scale(1.1);
  -ms-transform: scale(1.1);
  transform: scale(1.1);
  transition:0.5s;
transform-style: preserve-3d;
}
h2{
    padding: 0px
}
.weather5day{
 display: flex;
  flex-wrap: wrap;
  align-items: baseline;
  margin-bottom: 40px;
}
.day {
    padding: 10px;
}
.day p{
    font-weight: bold;
    font-size: 15px;
}
@media screen and (max-width: 980px) {
 .weather5day{
 display: flex;
  flex-wrap: nowrap;
  align-content: center;
  margin-bottom: 40px;
}
.day p{
    font-weight: bold;
    font-size: 12px;
}
}
@media screen and (max-width: 350px) {
.day p{
    font-weight: bold;
    font-size: 10px;
}
.day{
  padding: 5px
}
}
</style>
