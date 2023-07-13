<template>
  <div class=" text-center container  py-3">
    <div class="mb-3">
      <h2>Weather Forecast</h2>
      <label for="" class="px-2 "><h3>Cities</h3></label>
      <select id="" class="custom-select" style="width: 100%; height: 35px; background-color: beige; " name="" v-model="name" @change="getUrl(name)" >
        <option selected>Select one</option>
        <option :value="city.name" v-for="(city,index) in cities.data.data" :key="index">{{city.name}}</option>
      </select>
    </div>
    <div v-if="pending">
      <img src="~assets/loading.gif" alt="">

    </div>
    <div v-else class="d-flex justify-content-center">
      <div class="text-center">
        <!-- weather head -->
     <h3>{{weather.weather[0].main}}</h3>
 
     <!-- weather gif -->
     <div>
       <img src="~assets/cloudy.gif" style="width: 250px; height: 250px;" alt="" v-if="weather.weather[0].main =='Clouds'">
       <img src="~assets/sunny.gif" alt="" style="width: 250px; height: 250px;" v-if="weather.weather[0].main == 'Clear'">
       <img src="~assets/thunder.gif" alt="" style="width: 250px; height: 250px;" v-if="weather.weather[0].main == 'Rain'">
     </div>
 
     <!-- weather description -->
     <div>{{weather.weather[0].description}}</div>
 
     <!-- weather temp -->
     <h3>Current Temp:{{weather.main.temp}}°C</h3>
 
     <!-- weather feels_like -->
     <div>Feels like: {{weather.main.feels_like}}°C</div>
 
     <!-- wind speed -->
     <div>Wind Speed: {{weather.wind.speed}}Km/hr</div>
    
     </div>
    </div>
  </div>
  <div class="container d-flex justify-content-end">
    <h5>
     Designed By: Anjila_Tg
    </h5>
    </div>
</template>


<script setup>
  let name =ref("Dharan");
  const url= ref (`https://api.openweathermap.org/data/2.5/weather?q=Dharan&appid=382456452ecd209b533f2f66f79ae052&units=metric`);

  const {data: cities}=await useFetch("https://nepallocation.com.np/api/v1/city/list", {headers: {'Authorization' :"Bearer VoxyPyN-MExP0-tnxeMz0MPk"}});
  
  const {data : weather,pending} = useFetch(url, { refetch: true});
  function getUrl(weather) {
    url.value =`https://api.openweathermap.org/data/2.5/weather?q=${weather}&appid=382456452ecd209b533f2f66f79ae052&units=metric`
  }
</script> 
<style scoped>

</style>
