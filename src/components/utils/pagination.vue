<script setup>
const Pagination = ({breedPerPage,totalBreed, paginate})=> {
   const pageNumbers=[];
   for (let i=1;i<=Math.ceil(totalBreed/breedPerPage);i++) {
    pageNumbers.push(i);
   }
}
</script>

<template>
        <nav>
            <ul className="pagination">
                
                   <li v-for='number in pageNumbers' :key='number' className='page-item'>
                       <a @click='paginate(number)' href='!#'>
                           {{number}}
                       </a>
                   </li>
                
            </ul>

         </nav>   
    
    
</template>