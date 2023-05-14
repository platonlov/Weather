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
      return "Wind speed: " + this.info.wind.speed
    },
    minTemp() {
      return "Min temperature: " + this.info.main.temp_min
    },
    maxTemp () {
      return "Max temperature: " + this.info.main.temp_max
    }

  }
}
  
</script>

<template> 
  <div class="square">
    <h2>Get weather forecast in: {{ this.city }}</h2>
    <input v-model="city" class="input" type="text" placeholder="Enter the city"> <br>
    <button v-show="city != ''" @click="weather()" class="btn">Show the Temperature</button>
    <div v-if="info != null">
    <p>{{ temp }} ºC</p>
    <p>{{ feel }}ºC </p>
    <p>{{ minTemp }}ºC</p>
    <p>{{ maxTemp }}ºC</p>
    <p>{{ wind }}</p>
  </div>
 
  </div>
</template>

<style>
* {
  font-family: "Roboto";
}
body {
  background: rgb(93,77,16);
  background: linear-gradient(90deg, rgba(93,77,16,1) 0%, rgba(138,128,26,1) 29%, rgba(169,218,7,1) 85%);
  display: flex;
  justify-content: center;
  align-items: center;
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
  border-radius: 15px;
  margin-top: 60px;
  padding: 10px;
  width: 150px;
  padding: 5px;
}
.square .btn {
  border: transparent;
  margin-top: 10px;
  border: 1px solid brown;
}
@font-face {
  font-family: "Roboto";
  src: url('../Roboto-Regular.ttf');
  font-size: normal;
  font-weight: normal;

}
</style>