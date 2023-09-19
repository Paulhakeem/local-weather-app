<script setup>
import { ref } from 'vue';
import { RouterLink, useRoute, useRouter } from 'vue-router'
import BaseModal from './BaseModal.vue';
import { uid } from 'uid'

const route = useRoute()
const router = useRouter()
const savedCity = ref([])
console.log(savedCity)

const saveCity = () => {
  if(localStorage.getItem('savedCity')) {
    savedCity.value = JSON.parse(
      localStorage.getItem('savedCity')
    )
  }
  const locationObj = {
    id: uid(),
    state: route.params.state,
    city: route.params.city,
    coord: {
      lat: route.query.lat,
      lng: route.query.lng,
    }
  }
 savedCity.value.push(locationObj)
 localStorage.setItem(
  'savedCity', JSON.stringify(savedCity.value)
 )
 let query = Object.assign({}, route.query)
 delete query.preview
 router.replace({query})
}

const modalActive = ref(null)
const toggleModal = () => {
modalActive.value = !modalActive.value
}
</script>
<template>
 <header class=" shadow-lg bg-cover">
    <nav class="container flex flex-col sm:flex-row items-center gap-4 text-white py-6">
      <RouterLink :to="{name: 'home'}">
        <div class="flex items-center gap-3">
        <i class="fa-solid fa-sun text-2xl"></i>
        <p class="text-2xl">The Local Weather App</p>
      </div>
      </RouterLink>
      <div class="flex gap-3 flex-1 justify-end">
        <i @click="toggleModal"
        class="fa-solid fa-circle-info text-2xl hover:text-weather-secondary duration-150 cursor-pointer"></i>
        <i @click="saveCity"
        class="fa-solid fa-plus text-2xl hover:text-weather-secondary duration-150 cursor-pointer"></i>
      </div>

      <BaseModal 
      :modalActive="modalActive"
      @close-modal="toggleModal">
      <div class="text-black">
      <h2 class="text-xl font-semibold mb-1">About:</h2>
      <p class="mb-4">
        The local weather allows you to track the current
        and the future weather of the cities you choose
        </p>
        <h2 class="text-xl font-semibold mb-1">How it works:</h2>
        <ol class="list-decimal list-inside mb-4">
        <li>
          Search your city by entering the name into the search bar.
        </li>
        <li>
          Select a city within the result, this will take you to the current weather for your selection.
        </li>
        <li>
          track the city by clicking on the plus icon " + " in the top right.
          This will save the city to view at a later time on the home page.
        </li>
        </ol>
        <h2 class="text-xl font-semibold mb-1">How to Remove a city:</h2>
      </div>
      </BaseModal>
    
    </nav>
 </header>
</template>