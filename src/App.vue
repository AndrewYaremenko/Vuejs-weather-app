<script>
export default {
  data() {
    return {
      city: "",
    }
  }
}
</script>

<template>
  <div class="wrapper">
    <h1>Weather App on Vue.js</h1>
    <p>Check the weather in {{ city == "" ? "your city" : city}}</p>
    <input type="text" v-model="city" placeholder="Enter city...">
    <button>Get weather</button>
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

.wrapper button {
  background: #16956d;
  color: white;
  border-radius: 10px;
  border: 2px solid #0c4f39;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}

.wrapper button:hover {
  transform: scale(1.1);
}
</style>
