<template>
  <div class="weather">
    <h1 class="head">WEATHER</h1>
    <Form @onSubmit="handleSubmit" />
    <div class="temp">
      <h1> {{temp}}°С </h1>
      <p>{{status}}</p>
      <p class="place">{{name}}</p>
      <div class="temps">
        <div class="max-temp">
          <h5>Humidity</h5>
          <p>{{humidity}}</p>
        </div>
        <div class="min-temp">
          <h5>Pressure</h5>
          <p>{{pressure}}</p>
        </div>
      </div>
      <div class="icon">
        <img :src="icn" alt="">
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from '@vue/reactivity';
import Form from './components/Form.vue';

export default {
  name: 'App',
  components: {
    Form
  },
  setup(){
    let temp = ref('');
    let humidity = ref('');
    let pressure = ref('');
    let name = ref('');
    let icn = ref('');
    let status = ref('');
    const getData = (place = "Srinagar") => {
      fetch(`http://api.weatherapi.com/v1/current.json?key=b7993fbeccba47158bf164910221901&q=${place}&aqi=no`)
      .then(res => res.json())
      .then(data => {
        temp.value = data.current.temp_c;
        status.value = data.current.condition.text;
        icn.value = data.current.condition.icon;
        name.value = data.location.name;
        humidity.value = data.current.humidity;
        pressure.value= data.current.pressure_in;
      })
    };
    const handleSubmit = place => getData(place);
    getData();
      return {
        temp,
        status,
        icn,
        name,
        humidity,
        pressure,
        handleSubmit
      };
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body{
  background: #ccc;
  height: 100vh;
  display: grid;
  place-items: center;
}
.weather{
  width: 300px;
  border-radius: 10px;
  background: #fff;
  padding: 20px;
  text-align: center;
  box-shadow: 10px 5px 10px rgba(0, 0, 0, 0.5);
}
.weather .temp{
  position: relative;
  width: 150px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 10px;
  margin: 30px auto;
  text-align: center;
}
.weather .temp .place{
  color: orangered;
  font-weight: bold;
}
.weather .temp p{
  margin-top: 8px;
}
.weather .temp .temps{
  display: flex;
  justify-content: space-around;
  align-items: center;
  gap: 5px;
  margin-top: 20px;
}
.weather .temp .temps div h5{
  color: rgb(25, 25, 167);
}
.weather .temp .temps div p{
  margin-top: 8px;
}
.weather .temp .icon{
  position: absolute;
  top: -20px;
  left: -20px;
  background: #ccc;
  border-radius: 50%;
  width: 50px;
  height: 50px;
}
.weather .temp .icon img{
  width: 100%;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
