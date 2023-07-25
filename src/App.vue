<script>
import axios from 'axios';

export default {
  data() {
    return {
      city: "",
      info: {},
      error: "",
    }
  },
  computed: {
    cityName() {
      return "\"" + this.city + "\"";
    },
    showTemp() {
      return "temperature: " + this.info.main.temp;
    },
    showFeelsLike() {
      return "feels like: " + this.info.main.feels_like;
    },
    showMinTemp() {
      return "min temperature: " + this.info.main.temp_min;
    },
    showMaxTemp() {
      return "max temperature: " + this.info.main.temp_max;
    }
  },
  methods: {
    getWeather() {
      if (this.city.trim().length < 2) {
        this.error = "Title too short";
        return false;
      }

      this.error = "";

      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=${import.meta.env.VITE_API_KEY}`)
      .then(res => (this.info = res.data))
      .catch(error => (this.error = "Unknown locality", this.info = {}));

      return true;
    }
  }
}
</script>

<template>
  <div class="wrapper">
    <h1>Weather App on Vue.js</h1>
    <p>Check the weather in {{ city == "" ? "your city" : cityName }}</p>
    <input type="text" v-model="city" placeholder="Enter city...">
    <button v-if="city != ''" @click="getWeather()" class="activeBtn">Get weather</button>
    <button disabled v-else class="disableBtn">Enter city</button>
    <p v-show="error" class="error">{{ error }}</p>
    <p v-if="info.main">{{ showTemp }}</p>
    <p v-if="info.main">{{ showFeelsLike }}</p>
    <p v-if="info.main">{{ showMinTemp }}</p>
    <p v-if="info.main">{{ showMaxTemp }}</p>
  </div>
</template>

<style scoped>
.wrapper {
  width: 900px;
  height: 500px;
  padding: 20px;
  border-radius: 50px;
  background: darkslategray;
  color: white;
  text-align: center;
}

.wrapper h1 {
  margin-top: 50px;
}

.wrapper p {
  margin-top: 20px;
}

.wrapper input {
  margin: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid rgb(36, 114, 90);
  color: white;
  padding: 5px 8px;
  outline: none;
}

.wrapper input:focus {
  border-bottom-color: rgba(63, 203, 159, 1);
}

.wrapper .activeBtn {
  background: #16956d;
  color: white;
  border-radius: 10px;
  border: 2px solid #0c4f39;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}

.wrapper .activeBtn:hover {
  transform: scale(1.1);
}

.wrapper .disableBtn {
  background: #0e6046;
  color: white;
  border-radius: 10px;
  border: 2px solid #093929;
  padding: 10px 24px;
  margin-left: 20px;
  cursor: not-allowed;
}

.error {
  color: red;
}
</style>
