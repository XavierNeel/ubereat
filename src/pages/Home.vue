<template>
  <div class="home">
    <div class="header">
        <img src="https://d3i4yxtzktqr9n.cloudfront.net/web-eats-v2/ee037401cb5d31b23cf780808ee4ec1f.svg" alt="" srcset="">
        <div class="wrapperInput">
            <input v-model="user_search_restaurant" type="text" placeholder="de quoi avez vous envie?">
            <div class="search">
                <router-link v-for="(restaurant, i) in search_restaurant" :key="i" :to="{name:'Restaurant', params: {name: restaurant.name} }">
                      <div  class="containerRestaurantSearch">
                    <div class="wrapperImage">
                        <img :src="restaurant.image" alt="">
                    </div>
                    <p>{{restaurant.name}}</p>
                </div>
                </router-link>
              
            </div>
        </div>
        
    </div>
    <div class="banner"></div>

    <RestaurantRow v-for="(data, i) in data_restaurant" :key="i" :three_restaurant="data"/>
  </div>
</template>

<script>
//import
import BDD from '../BDD'


//components
import RestaurantRow from '../components/RestaurantRow.vue'
import {onMounted, ref, watch} from 'vue'
export default {
    name: 'Home',
     components: {
        RestaurantRow
    },
    setup(){
         class Restaurant{
            constructor (name, note, image, drive_time) {
                this.name = name
                this.note = note
                this.image = image
                this.drive_time = drive_time

            }
        }
        let data_restaurant = ref( [] );
        let all_restaurant =[];
        const MakeDataRestaurant = () => {
             let three_restaurant = [];
            for(const restaurant of BDD){
                const new_restaurant = new Restaurant(restaurant.name, restaurant.note, restaurant.image , restaurant.drive_time)
                //makeAllRestaurant array
                all_restaurant.push(new_restaurant);
                if (three_restaurant.length ===2){
                    three_restaurant.push(new_restaurant)
                    data_restaurant.value.push(three_restaurant)
                    three_restaurant =[];

                }else{
                    three_restaurant.push(new_restaurant)
                }
                }
               
        }
        onMounted(MakeDataRestaurant);
        
        //user search restaurant
        let user_search_restaurant = ref('');
        let search_restaurant = ref([])
        watch(user_search_restaurant, new_value =>{
            let regex = RegExp(new_value.toLowerCase());
            let new_search_restaurant = all_restaurant.filter(restaurant => regex.test(restaurant.name.toLowerCase()))
            if (new_value == 0) {
                search_restaurant.value = []
            }else{
                search_restaurant.value = new_search_restaurant;
            }
            
            

        })
        //

        //return
        //
        return {
            data_restaurant,
            user_search_restaurant,
            search_restaurant
        }
    }
    }
   
</script>

<style>
.header {
    height:120px;
    width:100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
}
img{
    width:200px;
}
input {
    background-color: #f6f6f6;
    border:none;
    height:60px;
    width:400px;
    outline:none;
    padding-left: 20px;
}
.banner {
    height:200px;
    width:100%;
    background-image:url("../assets/banLogo.png");
    background-position: center center;
    background-size: cover;
    }
.wrapperInput{
    position: relative;
}
.search{
    position: absolute;
    top:100%;
    width: 100%;
    background-color: #ffffff;
    }
.containerRestaurantSearch{
    display: flex;
    align-items: center;
    padding:10px;
    
}
.containerRestaurantSearch:hover{
    background: #f6f6f6;
}
.wrapperImage{
    height:60px;
    width:60px;
    margin-right: 25px;
    border-radius: 50%;
    overflow: hidden;
}
.wrapperImage img {
    height:40px;
    width: auto;
}


</style>