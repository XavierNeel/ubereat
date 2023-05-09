<template>
<div class="restaurantRow">
    <h2 class="title">nos restaurants</h2>
</div>
<div class="wrapperCard" >
    <RouterLink class="restaurant--wrapper" v-for="(restaurant, index) in three_restaurant" :key="index" :to="{name: 'Restaurant', params: {name: restaurant.name} }">
        <RestaurantCard :info_restaurant="restaurant"/>
    </RouterLink>
</div>

</template>

<script>
import RestaurantCard from './RestaurantCard.vue'
export default {
name: "RestaurantRow",
components:{
    RestaurantCard,
},
props:{
    three_restaurant: Array
}
}
</script>

<style>

.restaurant--wrapper {
    width: 30%;
    text-decoration: none !important;
}
.wrapperCard {
    display: flex;
    align-items: center;
    justify-content: space-between;

}
.title {
    font-size: 2rem;
}
</style>