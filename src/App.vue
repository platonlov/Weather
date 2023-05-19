<script>
import axios from 'axios'
import { resolveDirective } from 'vue'
export default {
  data() {
    return {
      city: '',
      info: null,




    }
  },
  methods: {
    weather() {
      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=9dd09e43be21c568fbb328edc231cafa`)
      .then(res => (this.info = res.data))
      this.city = ''
    }
  },
  computed: {
    temp() {
      return "Temperature: " + this.info.main.temp 
    },
    feel() {
      return "Feels like: " + this.info.main.feels_like
    },
    wind() {
      return "Wind speed: " + this.info.wind.speed + " m/s"
    },
    minTemp() {
      return "Min temperature: " + this.info.main.temp_min
    },
    maxTemp () {
      return "Max temperature: " + this.info.main.temp_max
    },

  }
}
  
</script>

<template> 
  <div class="square">

    <img class="cloud" src="https://img.icons8.com/material-outlined/384/cloud--v1.png" alt="Weather">
    <h2 class="text" v-if="this.city != ''"> Get weather forecast in: {{ this.city }}</h2>
    <h2 class="text" v-else>Get weather forecast in your city  </h2>

    <form action="" @submit.prevent>
      <input v-model="city" class="input" type="text" placeholder="Enter the city"> <br>
      <button v-show="city != ''" @click="weather()" class="btn">GET</button>
    </form>
    
    

    
    <div v-if="info != null" class="show">
    <b>Weather forecast for today:</b>
    <p>{{ temp }} ºC</p>
    <p>{{ feel }} ºC </p>
    <p>{{ minTemp }} ºC</p>
    <p>{{ maxTemp }} ºC</p>
    <p>{{ wind }}</p>
  </div>
 
  </div>
</template>

<style>
* {
  font-family: "Roboto";
  opacity: 0;
  animation: ani 0.5s forwards;
}
body {

  background: rgb(62,213,164);
  background: linear-gradient(90deg, rgba(62,213,164,1) 0%, rgba(36,198,181,1) 53%, rgba(28,156,215,1) 82%);

  display: flex;
  justify-content: center;
  align-items: center;
}

.cloud {
  width: 75px;
  height: 75px;
  top: 25px;
  

}
.show {
  opacity: 0;
  animation: ani 2.5s forwards;
  position: relative;
  top: -55px;
  margin:10px;
}
@keyframes ani {
  0% {opacity: 0;}
  100% {opacity: 1;}
}
.text {
  position: relative;
  top: -75px;
}

.square {
  width: 250px;
  height: 500px;
  background-color: rgba(205, 205, 205, 0.652);
  border-radius: 23px;
  padding: 20px;
  text-align: center;
  color: black;
}
.square h2 {
  margin-top: 100px;
}
.square .input {

  border-radius: 3px;
  border: none;
  padding: 10px;
  position: relative;
  top: -70px;


}
.square .btn {
  border:none;
  font-family: 'Nanum';
  background-color: white;
  padding: 7px;
  margin: 5px;
  position: relative;
  top: -65px;
  font-size: medium;

  

}
@font-face {
  font-family: "Roboto";
  src: url('../Roboto-Regular.ttf');
  font-size: normal;
  font-weight: normal;

}
@font-face {
  font-family: "Nanum";
  src: url('https://fonts.google.com/share?selection.family=Nanum%20Gothic%20Coding');
}

</style>