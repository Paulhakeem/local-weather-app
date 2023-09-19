<script setup>
import { ref, watch, onMounted } from 'vue'

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
        // console.log(cities.value)
        }
        }, 1000)
        
       //input.value = ""
       }
       catch(err) {
        alert(err.message)

       }
    }
    watch(input, (newValue, _) => {
        if(newValue) {
            getCities(newValue)
        }
    })
   
   onMounted(() => {
    getCities()
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
                class=" list absolute text-white
                w-full py-2 top-[66px] bg-weather-secondary text-center items-center">
               
             <li
                v-for="city in cities" 
                :key="city.id">
                <p class="justify-center text-2xl font-semibold ml-2 mr-2 pt-6">
                    <i class="fa-solid fa-location-dot fa-1x"></i> 
                    Today's Highlights in {{ city.name }}, {{ city.sys.country }}
                </p>
                 <div 
                 class="gap-6 pt-6"> 
                    <div class=" px-4 flex items-center justify-center">
                    <i class="fa-solid fa-cloud-sun fa-7x text-white mb-4"></i>
                    <div>
                        <h3 class="text-center text-lg italic text-white">Temperature</h3>
                    <p class="text-xl text-center mb-4 text-white">
                        <span class="text-6xl font-bold">{{ Math.round(city.main.temp) - 273}}</span>&#176C
                    </p>
                    </div>
                  
                    </div>
                   
                 </div>

                 <!-- modification -->

                 <div class="flex flex-wrap justify-evenly gap-4 mt-4 mb-8 mx-2">
        
                    <div class="px-4 bg-white rounded-md h-34">
                    <i class="fa-solid fa-gauge text-6xl text-weather-primary mt-2"></i>
                    <h3 class="text-center text-lg italic text-weather-primary">Wind Speed</h3>
                    <p class="text-xl text-center text-weather-primary">
                        <span class="text-2xl">{{ city.wind.speed}}</span>m/s 
                    </p>
                    </div>

                    
                    <div class="px-4 bg-white rounded-md h-34">
                    <i class="fa-solid fa-cloud-showers-heavy text-6xl text-weather-primary mt-2"></i>
                    <h3 class="text-center text-lg italic text-weather-primary">Rainfall</h3>
                    <p class="text-xl text-center text-weather-primary">
                       <span v-if="city.rain" class="text-2xl">{{ city?.rain["1h"] }}m&#x33a5</span>
                       <span v-else>No Rain</span>
                    </p>
                   
                    </div>


                    <div  class="px-4 bg-white rounded-md h-34">
                    <i class="fa-solid fa-face-grin-beam-sweat text-6xl text-weather-primary mt-2"></i>
                    <h3 class="text-center text-lg italic text-weather-primary">Feels Like</h3>
                    <p class="text-xl text-center text-weather-primary">
                        <span class="text-2xl">{{ Math.round(city.main.temp) - 273}}</span>
                        &degC
                    </p>
                    </div>

                    <div class="px-4 bg-white rounded-md h-34">
                    <i class="fa-solid fa-droplet text-weather-primary text-6xl mt-2"></i>
                    <h3 class="text-center text-lg italic text-weather-primary">Humidity</h3>
                    <p class="text-xl text-center text-weather-primary">
                    <span class="text-2xl">{{ city.main.humidity}}%</span>
                    </p>
                    </div>


                    <div class="bg-white rounded-md h-34">
                    <i class="fa-solid fa-cloud text-weather-primary text-6xl mt-2"></i>
                    <h3 class="text-center text-lg italic text-weather-primary">Clouds</h3>
                    <p class="text-xl text-center text-weather-primary ml-2 mr-2">
                    <span class="text-lg">{{ city.weather[0].description }}</span>
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