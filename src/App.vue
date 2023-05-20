
<script>
import './style.css'

export default{
  name: 'app',
  data(){
    return{
      api_key: '6ce99c2e52be65aa40de618bb02677c8',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
  methods: {
    fetchWeather(e){
      if (e.key == "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res => {
            return res.json();
          }).then(this.setResults);
      }
    },
    setResults(results){
      this.weather = results;
    },
    dateBuilder () {
      let d = new Date();
      let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
      let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    }
  }
}
</script>

<!-- .firtscolumn{
  /* min-height: 100vh;
  padding: 25px;
  display: flex;  
  flex-direction: column;
  align-content: center;
  place-items: center;
  text-align: left; */
} -->

<template>
  <div id='app' class="flex flex-col h-screen text-slate-700 font-serif">

    <div class="search-box flex justify-center items-center w-full max-w-[900px] mt-10 mx-auto px-5 drop-shadow-md shadow-gray-800 ">
        <input 
        type="text" 
        class="search-bar rounded-md text-slate-black py-3 px-5 w-full bg-slate-100 focus:bg-white" 
        placeholder="Buenos Aires, London, Tokyo..."
        v-model= "query"
        @keypress = "fetchWeather"
        />
      </div>

    <main class="flex gap-20 justify-center mt-20">
        <section class="w-fit weather-wrap  p-5 flex flex-col gap-5 place-items-left text-left w-[500px] text-4xl" v-if="typeof weather.main != 'undefined'">
          <div class="location-box ">
            <div class="location text-5xl">{{ weather.name }}, {{weather.sys.country}}</div>
            <div class="date italic">{{ dateBuilder() }}</div>
          </div>

          <div class="weather-box mt-7">
            <div class="temp text-8xl drop-shadow-md">{{ Math.round(weather.main.temp)}}°C</div>
            <div class="weather text-5xl mt-5">{{ weather.weather[0].main }}</div>
          </div>
        </section>
      <!--<section>
        <section>
          <p class="temp text-5xl">{{ weather.weather[0].description }}</p>
          <p class="temp text-5xl">{{ weather.pressure }}</p>. 
        </section>
      </section>-->

    </main>
  </div>
</template>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body{
  font-family: 'montserrat', sans-serif;
}

#app{
  background-image: url('/background-clouds.jpg');
  background-size: cover;
  background-position: center center;
  transition: 0.4s;
}



/* .search-box{
  display: flex;
  justify-content: center;
  margin: 1rem auto;
  width: 80%;
}

.search-box .search-bar{ 
  display: block;
  width: 100%;
  padding: 15px;

  color: #313131;
  font-size: 1rem;

  appearance: none;
  border: none;
  outline: none;
  background: none;

  box-shadow: 0px 0px 2px 1px  rgba(0,0,0,0.25);
  background-color: rgba(255,255,255,0.5);
  border-radius: 1rem;
  transition: 0.4s
}

.search-box .search-bar:focus{
  box-shadow: 0px 0px 16px rgba(0,0,0,0.25);
  background-color: rgba(255, 255, 255, 0.617);
  border-radius: 1rem;
}

.location-box .location{
  color: #fafafa;
  font-size: 32px;
  font-weight: 500;
  text-shadow: 1px 2px rgba(0,0,0,0.25);
}

.location-box .date{
  color: #fafafa;
  font-size: 20px;
  font-weight: lighter;
  font-style: italic;
}

.weather-box{

}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #fafafa;
  font-size: 102px;
  font-weight: 900;
  
  text-shadow: 3px 6px rgba(0,0,0,0.25);
  background-color: rgba(255,255,255,0.25);
  border-radius: 16px;
  margin: 36px 0;
}

.weather-box .weather{
  color: #fafafa;
  font-size: 48px;
  font-weight: 700;
  text-shadow: 1px 3px rgba(0,0,0,0.25);
}

.weather-wrap{
  display: block;
  margin: 10rem 0;
} */
</style>
