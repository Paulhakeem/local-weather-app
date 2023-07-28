<script setup>
import { ref, watch } from 'vue'

const input = ref("")
const cities = ref([])
const timeout = ref([])


// Get a list of cities that match the user's input
    const getCities = (city) => {
       try{
        clearTimeout(timeout.value)
        timeout.value = setTimeout( async() => {
        const response = await fetch
        (`https://api.openweathermap.org/data/2.5/find?q=${city}&appid=f2eca4d4b657ee27eac21b7a41a0b4aa`)
        const {list} = await response.json()
        
        if(list) {
        cities.value = list
        console.log(cities.value)
        }
        }, 1000)
        
       //input.value = ""
       }
       catch(err) {
        console.log(err.message)

       }
    }
    watch(input, (newValue, _) => {
        if(newValue) {
            getCities(newValue)
        }
    })
   
</script>
<template>
    <main class="container text-white">
        <div class="pt-4 mb-8 relative">
            <div
            class="flex">
            <input
            v-model="input"
            @keyup.enter="getCities"
            type="text" 
            placeholder="search for city or state"
            class="py-2 px-1 w-full bg-transparent border-b 
            focus:border-weather-secondary focus:outline-none focus:shadow-[0px_1px_0_0_#004E71]">
            </div>
            
            
            <ul
                class="absolute text-white
                w-full py-2 top-[66px] bg-weather-secondary text-center items-center">
               
                <li
                v-for="city in cities" 
                :key="city.id">
                <p class="justify-center text-2xl font-semibold ml-2 mr-2 pt-6">
                    <i class="fa-solid fa-location-dot fa-1x"></i> 
                    Today's Highlights in {{ city.name }}, {{ city.sys.country }}
                </p>
                 <div 
                 class="gap-6 pt-6 pl-2 mb-6 grid grid-cols-2 items-center sm:grid-cols-2 md:grid-cols-4 ml-4 mr-4"> 
                    <div class="bg-weather-primary shadow-lg rounded-md px-4 inline-grid">
                        <h3 class="text-center py-6 text-lg">Temperature</h3>
                        <i class="fa-solid fa-temperature-low fa-7x text-white mb-4"></i>
                    <p class="text-xl text-center mb-4">
                        <span class="text-3xl">{{ Math.round(city.main.temp) - 273}}</span>&#176C
                    </p>
                    </div>
                   
                    <div  class="bg-weather-primary shadow-xl rounded-md px-4 inline-grid">
                    <h3 class="text-center py-6 text-lg">Wind Speed</h3>
                    <i class="fa-solid fa-wind fa-7x mb-4 text-white"></i>
                    <p class="text-xl text-center mb-4">
                        <span class="text-3xl">{{ city.wind.speed}}</span>m/s 
                    </p>
                    </div>

                    
                    <div class="bg-weather-primary shadow-lg rounded-md px-4 inline-grid">
                    <h3 class="text-center py-6 text-lg">Rainfall (cubic)</h3>
                    <i class="fa-solid fa-cloud-showers-heavy fa-7x pb-4" 
                    style="color: #ffffff;"></i>
                    <p class="text-xl text-center mb-4">
                       <span v-if="city.rain" class="text-3xl">{{ city?.rain["1h"] }}m&#x33a5</span>
                       <span v-else>No Rain</span>
                    </p>
                   
                    </div>


                    <div  class="bg-weather-primary shadow-lg rounded-md px-4 inline-grid">
                    <h3 class="text-center py-6 text-lg">Feels Like</h3>
                    <i class="fa-solid fa-face-grin-beam-sweat fa-7x text-white mb-4"></i>
                    <p class="text-xl text-center mb-4">
                        <span class="text-3xl">{{ Math.round(city.main.temp) - 273}}</span>
                        &degC
                    </p>
                    </div>

                    <div  class="bg-weather-primary shadow-lg rounded-md px-4 inline-grid">
                    <h3 class="text-center py-6 text-lg">Humidity</h3>
                    <i class="fa-solid fa-droplet text-white fa-7x mb-4"></i>
                    <p class="text-xl text-center mb-4">
                        <span class="text-3xl">{{ city.main.humidity}}%</span>
                    </p>
                    </div>


                    <div  class="bg-weather-primary shadow-lg rounded-md px-4 inline-grid h-64">
                    <h3 class="text-center py-6 text-lg">Clouds</h3>
                    <i class="fa-solid fa-cloud text-white fa-6x mb-4"></i>
                    <p class="text-xl text-center mb-4">
                        <span class="text-2xl">{{ city.weather[0].description }}</span>
                    </p>
                    </div>


                    <div  class="px-4 inline-grid pl-16 w-64">
                    <h3 class="text-center py-6 text-lg">Coordinates</h3>
                    <i class="fa-solid fa-earth-africa fa-10x mb-4"></i>
                    <p class="text-xl text-center mb-4">
                        <span class="text-xl">Latitude: {{ city.coord.lat }}</span>
                    </p>
                    <p class="text-xl text-center mb-4">
                        <span class="text-xl">Longitude: {{ city.coord.lon}}</span>
                    </p>
                    </div>
                 </div>
                </li>
                <div class="bg-gradient-to-r from-weather-primary to-weather-secondary rounded-6xl">
                    <p class="font-light">Designed With 
                    <i class="fa-solid fa-heart-circle-check text-red-500 text-xl py-2 "></i>
                    By CodeWithPaul
                </p>
                </div>
                
            </ul>
        </div>

 
    </main>
</template>