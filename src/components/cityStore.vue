<script setup></script>
<template>
    <div>
        
        <div class="bg-weather-primary shadow-xl rounded-md px-4 inline-grid">
                    <h3 class="text-center py-6 text-lg italic">Wind Speed</h3>
                    <i class="fa-solid fa-wind fa-7x mb-4 text-white"></i>
                    <p class="text-xl text-center mb-4">
                        <span class="text-3xl">{{ city.wind.speed}}</span>m/s 
                    </p>
                    </div>

                    
                    <div class="bg-weather-primary shadow-lg rounded-md px-4 inline-grid">
                    <h3 class="text-center py-6 text-lg italic">Rainfall (cubic)</h3>
                    <i class="fa-solid fa-cloud-showers-heavy fa-7x pb-4" 
                    style="color: #ffffff;"></i>
                    <p class="text-xl text-center mb-4">
                       <span v-if="city.rain" class="text-3xl">{{ city?.rain["1h"] }}m&#x33a5</span>
                       <span v-else>No Rain</span>
                    </p>
                   
                    </div>


                    <div  class="bg-weather-primary shadow-lg rounded-md px-4 inline-grid">
                    <h3 class="text-center py-6 text-lg italic">Feels Like</h3>
                    <i class="fa-solid fa-face-grin-beam-sweat fa-7x text-white mb-4"></i>
                    <p class="text-xl text-center mb-4">
                        <span class="text-3xl">{{ Math.round(city.main.temp) - 273}}</span>
                        &degC
                    </p>
                    </div>

                    <div  class="bg-weather-primary shadow-lg rounded-md px-4 inline-grid">
                    <h3 class="text-center py-6 text-lg italic">Humidity</h3>
                    <i class="fa-solid fa-droplet text-white fa-7x mb-4"></i>
                    <p class="text-xl text-center mb-4">
                        <span class="text-3xl">{{ city.main.humidity}}%</span>
                    </p>
                    </div>


                    <div  class="bg-weather-primary shadow-lg rounded-md px-4 inline-grid h-64">
                    <h3 class="text-center py-6 text-lg italic">Clouds</h3>
                    <i class="fa-solid fa-cloud text-white fa-6x mb-4"></i>
                    <p class="text-xl text-center mb-4">
                        <span class="text-2xl">{{ city.weather[0].description }}</span>
                    </p>
                    </div>


                    <div  class="px-4 inline-grid pl-16 w-64">
                    <h3 class="text-center py-6 text-lg italic">Coordinates</h3>
                    <i class="fa-solid fa-earth-africa fa-7x mb-4"></i>
                    <p class="text-xl text-center mb-4">
                        <span class="text-xl">Latitude: {{ city.coord.lat }}</span>
                    </p>
                    <p class="text-xl text-center mb-4">
                        <span class="text-xl">Longitude: {{ city.coord.lon}}</span>
                    </p>
                    </div>
    </div>
</template>
