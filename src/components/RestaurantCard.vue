<template>
  <div class="restaurant--card">
    <div :style="changeBackground" class="restaurant--image">
      
    </div>
    <div class="restaurant--information">
      <div class="top">
        <p class="name">{{info_restaurant.name}}</p>
        <p class="note">{{info_restaurant.note}}</p>
      </div>
      <p class="time">{{info_restaurant.drive_time}}</p>
      </div>
    
   
  </div>
</template>

<script>
import {computed} from 'vue'
export default {
  name: "Restaurantcard",
  props: { 
    info_restaurant: Object
    },
    setup(props) {
      const changeBackground = computed(() => {
        return {
          backgroundImage: `url(${props.info_restaurant.image})`
        }
      })
      return {
        changeBackground
      }

    }
  }


</script>

<style>
.restaurant--card {
    width: 100%;
   
    }

.restaurant--image {
        height: 300px;
        background-size: cover;
        background-position: center;
        };
p {
  margin: 0px;
  }

.restaurant--information .top {
  margin: 10px 0px;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }
    .time {
      font-size: 0.9 rem;
    }

    .note{
      background-color: #eeeeee;
      height: 30px;
      width: 30px;
      font-size: 0.8rem;
      display: flex;
      justify-content: center;
      align-items: center;
      border-radius: 50%;
    }


</style>