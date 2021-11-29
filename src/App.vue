<template>
<div id="app">
<main>
<div class="search-box">
<input type="text" class="search-bar" placeholder="Search..." v-model="query" @keypress="fetchWeather" />
</div>
<div class="weather-wrap" v-if="typeof weather.main !='undefined'">
<div class="location-box">
  <div class="location">{{ weather.name }},{{ weather.sys.country }} </div>
  <div class="date">Monday 29 November 2021</div>
</div>

<div class="weather-box">
  <div class="temp">{{ Math.round(weather.main.temp) }}`c</div>
  <div class="weather">{{weather.weather[0].main }}</div>
</div>



</div>



</main>


</div>
</template>

<script>


export default {
  name: 'App',
  data() {
    return {
   api_key:'84c9b68b70c6ff43cdcc1196524391e7',
   url_base:'https://api.openweathermap.org/data/2.5/',
   query: '',
   weather:{}
    }
  },
  methods:{
    fetchWeather (e) {
      if (e.key =="Enter"){
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res =>{
          return res.json();
        }).then(this.setResults);
      }
    },
    setResults(results)
    {
      this.weather = results;
    }
  }
 
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
 
  background-image: url('./assets/v1.jpg');
  background-size: cover;
background-position: bottom;
transition: 0.4s;
}
main{
  min-height: 100vh;
  padding: 25px;
}

*{
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}
.search-box
{
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  color: grey;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background-color:linear-gradient(rgba(0,0,0,.7),rgba(0,0,0,.5));
  border-radius: 0px 16px 0px 16px;
}
.location-box .location{
  color: white;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
}
.location-box .date
{
  color: white;
  font-size:20px ;
  font-weight: 300;
  text-align: center;
  padding: 20px 0px;
}
.weather-box{
  text-align: center;
}
.weather-box .temp{
  display: inline;
  padding: 0px 20px;
  color: #fff;
  font-size: 100px;
  font-weight: 900;
  border-radius: 16px;
  box-shadow: 3px 5px rgba(0,0,0,0.25);
  background-color:rgba(225, 255, 255, 0.25);
}
.weather-box .weather {
  color: white;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  padding: 20px 0px;
}

</style>
