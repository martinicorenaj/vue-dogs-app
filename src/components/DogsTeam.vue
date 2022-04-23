<script setup>
import {ref,watch} from 'vue'

const props=defineProps({
    'myTeam':Array
})
</script>

<template>
    <div>
       <h2>My team!</h2>
       <ul>
       <li v-for='myDog in props.myTeam' :key='myDog.photo'>
       <img :src='myDog.photo' alt="dog img" width='200' height='200' />
       <p>{{myDog.breed}}</p>
       </li>
       </ul>

    </div>
</template>
