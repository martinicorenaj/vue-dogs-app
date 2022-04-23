<script setup>
import { ref,watch} from 'vue'
import pagination from './utils/pagination.vue'



const props=defineProps({

    'selectedBreed':String
})
const emit = defineEmits(['dogSelection'])
const breedPhotos=ref([])
 
async function fetchData() {
  
  const response = await fetch(`https://dog.ceo/api/breed/${props.selectedBreed}/images`)
  const data=await response.json()
  //de todo el array de fotos solamente recorto 10 para que no cargue tantas, deberia ir paginado.
  breedPhotos.value = data.message.slice(0,10)
  //breedPhotos.value = data.message
  
}

fetchData()

watch(props,fetchData)

const myTeam=ref([])

const addDog=(dog)=>{
    const dogObject={
        
        photo:dog,
        breed:props.selectedBreed,

    }
    myTeam.value=myTeam.value.concat(dogObject)
    emit('dogSelection', myTeam.value)
}

</script>
<template>
    <div  >
    <h2 >{{props.selectedBreed}}</h2>
        <ul>
            <li v-for='d in breedPhotos' :key='d'>
        <div>
        <img :src='d' alt="dog img" width='200' height='200' />
        <button @click='addDog(d)' >add dog</button>
        </div>
            </li>
        </ul>
        
          
            
        
            
        
    </div>
</template>