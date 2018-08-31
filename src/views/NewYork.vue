<template>
<div class="main">
  <div class="right">
    <h1>Today's weather</h1>
    <h1 class="time">{{date}}</h1>
    <newYork3hr class="city"/>
    </div>
    <div class="left">
    <newYork5day class="city"/>
    </div>
  </div>
  </template>

<script>
// @ is an alias to /src
import newYork3hr from '@/components/3hr/NewYork3hr.vue'
import newYork5day from '@/components/5day/NewYork5day.vue'
export default {
  name: 'NewYork',
  components: {
    newYork3hr,
    newYork5day
  },
  data () {
    return {
      date: '',
      show: true
    }
  },
  created () {
    this.isDate()
  },
  methods: {
    isDate () {
      let date = new Date()
      this.date = date.toLocaleTimeString() + ' ' + date.toDateString()
      setTimeout(this.isDate, 1000)
    }
  }
}
</script>
<style scoped>
h3 {
  padding: 5px;
}
.right{
  width: 20%;
  padding: 20px;
  border-right: 1px solid black;
    height: 650px;
  position: sticky;
  top: 0;
}
.left{
  width: 80%;
  padding: 20px;
  font-size: 15px;
  margin-top: -50px;
}
.time {
  font-size: 15px;
  padding: 10px
}
.main{
  display: flex;
  justify-content:space-around;
  padding: 20px;
}
.right h1 {
  padding-bottom: 10px;
}
.meta {
  background: none
}
@media screen and (max-width: 980px)
{
.main {
  display: flex;
  flex-direction: column;
  justify-content:space-around;
  padding: 20px;
}
.right{
  width: 100%;
  padding: 5px;
  border-right: none;
  border-bottom: 1px solid black
}
.left{
  width: 100%;
  padding: 0px;
  font-size: 15px;
  margin-top: 0px;
}
}
</style>
