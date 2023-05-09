<template>
    <router-link to="/">
        <div id="return">Accueil</div>
    </router-link>
    <div>
        <img :src="restaurant.image" alt="">
    </div>
        
   
    
  <p>{{restaurant.name}}</p>
  <p>note du restaurant: {{restaurant.note}}</p>
  <p>temps de livraison: {{restaurant.drive_time}}</p>
</template>

<script>
import BDD from '../BDD'
import {useRoute} from 'vue-router'
export default {
   name: 'Restaurant',
   setup() {
    const route = useRoute()
    const restaurant = BDD.find((restaurant => restaurant.name === route.params.name))
    return {
        restaurant
    }
  
   }
   

}
</script>

<style >
#return {
    margin: 25px 45px;
    font-weight: 400;
    cursor:pointer;
    pointer-events: none;
    text-decoration: none !important;
    text-decoration: none;
    color: #000;
   
}
#return:hover {
    font-weight: 900;
}



</style>