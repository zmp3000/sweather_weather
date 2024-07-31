<template>
  <div class="wrapper">
    <h1>Погодное приложение</h1>
    <p>Узнать погоду в {{ city == "" ? "в вашем городе" :  cityName }}</p>
    <input type="text" v-model="city"  placeholder="Введите город">
    <button v-if="city!=''" @click="getWeather()">Получить погоду</button>
    <button disabled v-else>Введите название города</button>
    <p class="error">{{ error }}</p>
    <p v-if="info!=null">{{ info }}</p>
  </div>
</template>

<script>
import axios from 'axios';
export default{
  data(){
    return{
      city: "",
      error: "",
      info: null,
    }
  },
  computed: {
    cityName(){
      return "." + this.city + "."
    }
  },
  methods: {
    getWeather(){
     if(this.city.trim().length < 2){
      this.error="Больше одного символа"
      return false;
     }
     this.error=''
     axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metrik&appid=774a6452b6c6387ddfca137414a1781e`) 
      .then(res=>(this.info=res.data.weather))
     

    }
  }
}
</script>

<style scoped>
.error{
  color: #d03939;
  font-family: Arial, sans-serif;
}

.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  background: rgb(2,0,36);
  background: linear-gradient(90deg, rgba(2,0,36,1) 0%, rgba(20,189,86,1) 0%, rgba(9,119,121,0.3881885517879027) 56%, rgba(0,212,255,1) 100%); 
  text-align: center;
  color: #fff;
}

.wrapper h1{
margin-top: 50px;
font-family: Arial, sans-serif;
}

.wrapper p{
  margin-top: 20px;
  font-family: Arial, sans-serif;
}

.wrapper input{
  margin-top: 30px;
  background: transparent;
  border: 0;
  border-bottom: 2px solid #110813;
  color: #fcfcfc;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
}

.wrapper button:disabled{
  background: #9e8230;
  width: 150px;
  color: #fff;
  border-radius: 10px;
  border: 2px solid #9e8230;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}

.wrapper button{
  background: #e3bc4b;
  width: 150px;
  color: #fff;
  border-radius: 10px;
  border: 2px solid #b99935;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}

.wrapper button:hover{
  transform: scale(1.1) translateY(-5px);
}
</style>
