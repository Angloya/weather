<template>
<div class="main">
  <div class="right">
    <h1>Today's weather</h1>
    <h1 class="time">{{date}}</h1>
    <london3hr class="city"/>
    </div>
    <div class="left">
    <london5day class="city"/>
    </div>
  </div>
  </template>

<script>
// @ is an alias to /src
import london3hr from '@/components/3hr/London3hr.vue'
import london5day from '@/components/5day/London5day.vue'
export default {
  name: 'London',
  components: {
    london3hr,
    london5day
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
  top: 20px;
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
  border-bottom: 1px solid black;
  position:static;
  top: 0px;
  padding-bottom: 40px;
}
.left{
  width: 100%;
  padding: 0px;
  font-size: 15px;
  margin-top: 0px;
}
}
</style>
