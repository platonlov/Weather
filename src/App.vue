<script>
import axios from 'axios'
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
    <h2 v-if="this.city != ''"> Get weather forecast in {{ this.city }}</h2>
    <h2 v-else>Get weather forecast in your city  </h2>
    <form action="" @submit.prevent>
      <input v-model="city" class="input" type="text" placeholder="Enter the city"> <br>
      <button v-show="city != ''" @click="weather()" class="btn">GET</button>
    </form>
    
    <div v-if="info != null" class="show">
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
  background: rgb(213,62,62);
background: linear-gradient(90deg, rgba(213,62,62,1) 0%, rgba(198,159,36,1) 35%, rgba(198,100,36,1) 82%);
  display: flex;
  justify-content: center;
  align-items: center;
}
.citycolor {
  color:red;
}
.show {
  opacity: 0;
  animation: ani 2.5s forwards;
  margin-top: 35px;
}
@keyframes ani {
  0% {opacity: 0;}
  100% {opacity: 1;}
}
.square {
  width: 900px;
  height: 500px;
  background: rgba(0, 0, 0, 0.652);
  border-radius: 23px;
  padding: 20px;
  text-align: center;
  color: white;
}
.square h2 {
  margin-top: 100px;
}
.square .input {
  border: transparent;
  border-radius: 5px;
  margin-top: 13px;
  padding: 7px;
  width: 190px;
  text-align: center;
}
.square .btn {
  border: transparent;
  margin-top: 15px;
  background-color: white;
  color: black;
  font-family: "Nanum";
  font-size: 100%;
  

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