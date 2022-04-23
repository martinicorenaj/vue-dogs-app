<script setup>

import {ref,watch} from 'vue'


const breedsList= ref(null)
const breedSearch=ref('')
const filteredBreeds=ref('')
const selectedBreed=ref('')
const emit = defineEmits(['chooseBreed'])



async function fetchData() {
  const response = await fetch('https://dog.ceo/api/breeds/list/all')
  const data=await response.json()
  breedsList.value = Object.keys(data.message)
  
}

fetchData()

async function filterBreeds() {
  let res = await fetchData()
  filteredBreeds.value=breedsList.value.filter((d)=>d.includes(breedSearch.value))
  
}
filterBreeds()

watch(breedSearch,filterBreeds)

const selectBreed=(breed)=>{
  selectedBreed.value=breed
  emit('chooseBreed', selectedBreed.value)
  breedSearch.value=''
}


</script>

<template>

<div id="app"
       class="ui container">
    
<h3>DOG FILTER</h3>
      <input v-model="breedSearch">
      <ul v-if='filteredBreeds.length<10'>
        <li  v-for="dogBreed in filteredBreeds" :key="dogBreed">{{dogBreed}}
        <button @click="selectBreed(dogBreed)" />
        </li>
      </ul>
      <p v-else>Especificar busqueda</p>
    </div>
    
</template>

