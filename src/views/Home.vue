<template>
  <div class="main">
    <h1>Today's weather</h1>
    <h1 class="time">{{date}}</h1>
    <div class="home">
    <router-link to="/london"><london3hr class="city"/></router-link>
    <router-link to="/moscow"><moscow3hr class="city"/></router-link>
    <router-link to="/vladimir"><vladimir3hr class="city"/></router-link>
    <router-link to="/newYork"><newYork3hr class="city"/></router-link>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import london3hr from '@/components/3hr/London3hr.vue'
import moscow3hr from '@/components/3hr/Moscow3hr.vue'
import newYork3hr from '@/components/3hr/NewYork3hr.vue'
import vladimir3hr from '@/components/3hr/Vladimir3hr.vue'

export default {
  name: 'home',
  components: {
    moscow3hr,
    london3hr,
    newYork3hr,
    vladimir3hr
  },
  data () {
    return {
      date: ''
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
.main{
  height: 100%;
}
.meta:hover {
  background: rgba(255, 255, 255, 0.9);
  -webkit-transform: scale(1.1);
  -ms-transform: scale(1.1);
  transform: scale(1.1);
  transition:0.4s;
transform-style: preserve-3d;
}
.meta {
  background: rgba(255, 255, 255, 0.3)
}
.home{
  display: flex;
  justify-content:space-around;
  flex-wrap: wrap;
  padding: 20px;
  padding-bottom: 100px;
}
.city {
  border: 1px solid black;
  padding: 20px;
  width: 300px;
}
.main h1 {
  padding-bottom: 10px;
}
@media screen and (max-width: 980px)
{
.home {
  display: flex;
  flex-direction: column;
   align-items:center;
  padding: 20px;
}
.time {
  font-size: 20px
}
}
@media screen and (max-width: 350px){
  .home {
  display: flex;
  flex-direction: column;
  align-items:center;
  padding: 0px;
  }
  .city {
  padding: 10px;
  width: 250px;
}
}
</style>
